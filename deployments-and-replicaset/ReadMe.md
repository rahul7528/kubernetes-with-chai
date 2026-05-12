# Day 3 — Deployments & ReplicaSets (Complete)

> Kubernetes with Chai — Definition first, Chai second

## PART A — ReplicaSet

**Definition:** A ReplicaSet is an apps/v1 controller that maintains a stable set of replica Pods running at any given time. It uses a label selector to identify Pods to manage.

**Chai:** The staff roster. It says "always keep 3 trays with label app=chai". If a tray breaks, the roster hires a new cook instantly.

**Technical details:**
- Watches Pods via spec.selector.matchLabels
- Creates/deletes Pods from spec.template
- Adds label pod-template-hash automatically when created by Deployment
- Sets ownerReference on Pods for garbage collection
- Reconciliation loop in kube-controller-manager

**When to use directly:** Almost never in production. Only for learning or custom controllers. Always prefer Deployment.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: chai-rs-example
  labels:
    app: chai
spec:
  replicas: 3
  selector:
    matchLabels:
      app: chai
      tier: frontend
  template:
    metadata:
      labels:
        app: chai
        tier: frontend
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
```

PART B — Deployment
Definition: A Deployment provides declarative updates for Pods and ReplicaSets. You describe desired state, Deployment controller changes actual state gradually.

Chai: The shift manager. You give him "3 trays, ginger recipe v2". He creates a new roster, brings new trays one by one, keeps shop open.

Why it matters: 95% of production workloads use Deployments. Provides self-healing, rolling updates, rollbacks, history.

Key technical fields:

spec.replicas - desired count
spec.selector - IMMUTABLE, must match template labels
spec.template - Pod spec
spec.strategy.type - RollingUpdate or Recreate
spec.strategy.rollingUpdate.maxSurge - extra Pods allowed
spec.strategy.rollingUpdate.maxUnavailable - Pods allowed down
spec.minReadySeconds - wait after Pod ready
spec.progressDeadlineSeconds - timeout for rollout
spec.revisionHistoryLimit - how many old RS to keep


```apiVersion: apps/v1
kind: Deployment
metadata:
  name: chai-deploy-example
spec:
  replicas: 3
  revisionHistoryLimit: 5
  progressDeadlineSeconds: 600
  minReadySeconds: 10
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: chai
  template:
    metadata:
      labels:
        app: chai
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        readinessProbe:
          httpGet:
            path: /
            port: 80
```


PART C — How they work together

You apply Deployment

Deployment controller creates ReplicaSet v1 with pod-template-hash=abc123

ReplicaSet controller creates 3 Pods with ownerReference to RS

You update image to 1.26

Deployment creates RS v2 with hash=def456

RollingUpdate: scale v2 up to 1, wait Ready, scale v1 down to 2, repeat

Old RS v1 scaled to 0, kept for rollback


Chai: Manager writes new roster, supervisor hires new cooks gradually.
