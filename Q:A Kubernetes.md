# Kubernetes with Chai — Day 1: Kubernetes Fundamentals

> Repo: https://github.com/rahul7528/kubernetes-with-chai
> Format: Definition first, then Chai analogy

---

## BASIC QUESTIONS — Day 1

### Q1. What is Kubernetes?
**Definition:** An open-source container orchestration platform that automates deployment, scaling, and management of containerized applications. -m
**Chai:** The franchise operating manual. It tells every stall how to make chai the same way, how many trays to keep ready, and what to do if a cook is sick.

### Q2. What is a cluster?
**Definition:** A set of Nodes (machines) managed by a control plane that work together to run containerized workloads. -m
**Chai:** Your whole chai chain — head office plus all stalls across the city.

### Q3. Name the 4 main control plane components.
**Definition:** API server, etcd, scheduler, controller-manager.
**Chai:** Head office staff: receptionist (API), ledger book (etcd), floor manager (scheduler), shift supervisors (controllers).

### Q4. What does etcd do?
**Definition:** A consistent distributed key-value store that holds all cluster state and configuration.
**Chai:** The master ledger where every order, recipe change, and stall status is written. If the ledger is lost, the shop forgets everything.

### Q5. What does kube-scheduler do?
**Definition:** Watches for unscheduled Pods and binds them to a suitable Node based on resources and constraints.
**Chai:** Manager who looks at all stalls and decides which free stall gets the next tray.

### Q6. What is a Node?
**Definition:** A worker machine that runs Pods, containing kubelet, kube-proxy, and a container runtime.
**Chai:** One physical chai stall with gas, counter, and a cook.

### Q7. What runs on a worker Node?
**Definition:** kubelet, kube-proxy, container runtime.
**Chai:** The cook, the cashier who routes customers, and the stove.

### Q8. What does kubelet do?
**Definition:** Agent on each Node that ensures the containers in PodSpecs are running and healthy.
**Chai:** The stall cook who reads the order slip and actually brews.

### Q9. How do you create a local cluster?
**Definition:** Use tools like kind, minikube, or k3d to run a cluster in Docker.
**Chai:** Set up a practice kitchen in your garage before opening real stalls.

### Q10. What is the difference between control plane and worker?
**Definition:** Control plane makes decisions, workers execute workloads.
**Chai:** Head office plans, stalls cook.

---
