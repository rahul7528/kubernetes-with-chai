# Kubernetes with Chai Example

> Learn Kubernetes without the headache. Every concept is explained twice: once properly, once with chai.

## What is Kubernetes?

Kubernetes is an open-source system that automatically runs, scales, and fixes your applications when they are packaged as containers.

Think of it as the manager for a food court. You don't tell it how to boil water. You just say "keep 3 chai stalls open" and it makes it happen.

## Why was it created?

1. **Before containers:** one app per big server. Wasteful and slow.
2. **Docker (2013):** solved packaging. Now you could ship your app as a lightweight box.
3. **New problem:** who starts 100 boxes, replaces dead ones, balances load, updates without downtime?
4. **Google had this problem for 10 years** running Gmail and Search with a tool called Borg.
5. **2014:** Google open-sourced the idea as Kubernetes.

Docker gave us the shipping container. Kubernetes gave us the entire port, cranes, and traffic control.

## Why is it called k8s?

Kubernetes is long to type. Count the letters between K and s:

K **ubernete** s → 8 letters

So K8s = Kubernetes. Same trick as i18n for internationalization.

---

## Core Terminology

| Term | Real Definition | Chai Shop Example |
| --- | --- | --- |
| **Image** | A read-only template with your app and dependencies. | A sealed masala packet with printed recipe. |
| **Container** | A running instance of an image, isolated with its own filesystem and process. | A pot on the stove actively brewing chai from that packet. Not the cup, the pot. |
| **Pod** | Smallest unit Kubernetes manages. Usually holds 1 container, gets one IP. | A steel tray that carries the pot. If you need a frother, it rides on the same tray. |
| **Node** | A worker machine (VM or physical) that runs Pods. | One stall in the food court with gas and counter space. |
| **Cluster** | A group of Nodes managed together. | The entire food court with many stalls. |
| **Control Plane** | The brain: API Server, etcd, Scheduler, Controller Manager. Keeps desired state. | Head office upstairs with ledger, phone, and whiteboard. Doesn't make chai, decides everything. |
| **kubectl** | Command-line tool to talk to the API Server. | Your phone to call head office. |
| **Manifest** | YAML or JSON file describing what you want. | The written order slip: "3 trays, recipe v1". |
| **Deployment** | Controller that ensures a desired number of Pods stay running and updates them safely. | Shift supervisor whose job is "always keep 3 trays running, roll out new recipe one by one". |
| **ReplicaSet** | Maintains exact Pod count for a Deployment. | Supervisor's clipboard: "wanted 3, have 2, make 1 more". |
| **Service** | Stable network endpoint that load-balances to a set of Pods. | Permanent signboard "CHAI COUNTER". Customers use the sign, not tray numbers. |
| **Namespace** | Virtual cluster to isolate teams or environments. | Separate halls: Veg Hall, Non-Veg Hall, Staff Only. Same building, different spaces. |
| **ConfigMap** | Stores non-secret configuration. | Board with prices: chai = 20, open = 8am. |
| **Secret** | Stores sensitive data, base64 encoded. | Locked box with UPI PIN and supplier password. |
| **Ingress** | Manages external HTTP/HTTPS access to Services. | Main gate with directions: chai.college.in → Chai Counter. |

---

## How it works in one sentence

You write what you want in a manifest, send it with kubectl, the control plane stores it, the Deployment keeps the right number of Pods alive on Nodes, and a Service gives them a stable address.

---

## Next Steps

1. Read `/architecture/ARCHITECTURE.md` for a visual breakdown of control plane vs nodes.
2. Try Day 2: create your first Deployment and Service locally with kind or minikube.
3. Contribute your own analogies via pull request.

Made for beginners, by a beginner. PRs welcome.
