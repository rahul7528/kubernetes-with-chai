# Kubernetes Architecture

## High Level

```
+---------------------+        +-----------------------------+
|   Control Plane     |        |        Worker Nodes         |
| (Head Office)       |        | (Stalls)                    |
|                     |        |                             |
|  API Server -------+--------> kubelet (captain on stall)   |
|  etcd (ledger)      |        | containerd (hands)          |
|  Scheduler          |        | kube-proxy (runner)         |
|  Controller Manager |        |                             |
+---------------------+        +-----------------------------+
```

## Control Plane Components

1. **API Server** — front desk. All kubectl requests go here.
2. **etcd** — the single source of truth. Stores cluster state.
3. **Scheduler** — picks best Node for an unscheduled Pod based on resources.
4. **Controller Manager** — runs control loops. Ensures Deployments match desired replicas.
5. **Cloud Controller Manager** — talks to cloud provider for load balancers and disks.

## Node Components

1. **kubelet** — agent that talks to API Server and starts containers.
2. **Container Runtime (containerd)** — actually runs the containers.
3. **kube-proxy** — maintains networking rules for Services.

## Request Flow Example

1. You apply Deployment manifest for 3 replicas.
2. API Server validates and writes to etcd.
3. Controller creates 3 Pod objects.
4. Scheduler assigns each Pod to a Node.
5. Each kubelet pulls image and starts container.
6. Service selects Pods by label and programs kube-proxy.

If a Node dies, Controller notices missing heartbeats, deletes Pods, Scheduler places them elsewhere. No human needed.

See the official docs for deep dive: kubernetes.io/docs/concepts/overview/components/
