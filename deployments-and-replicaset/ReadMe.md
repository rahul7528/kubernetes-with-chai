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
