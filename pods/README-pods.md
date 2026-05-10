# Day 2 — Pods: The Steel Tray

> Kubernetes with Chai | https://github.com/rahul7528/kubernetes-with-chai

This guide covers Pods from basic to advanced. Every concept is **Definition first, then Chai analogy.**

---

## 1. What is a Pod?

**Definition:** The smallest deployable unit in Kubernetes. A Pod is a group of one or more containers with shared storage and network resources, and a specification for how to run the containers. All containers in a Pod are co-located and co-scheduled on the same Node.

**Chai:** The steel tray. You never carry a loose pot through a busy market. The tray ensures the pot, sugar, and spoon arrive together, share the same table, and are cleared together.

## 2. Why Pods exist (not just containers)

**Definition:** Containers alone lack atomic scheduling, shared localhost, and shared lifecycle. Pods provide an abstraction for co-dependent containers.

**Chai:** If masala chai needs a pot and a frother, you put both on one tray so they move as one order.

## 3. Pod vs Container vs Node

**Definition:** Container = single process. Pod = wrapper for 1+ containers sharing IP. Node = machine that runs Pods.

**Chai:** Pot = container. Tray = Pod. Stall = Node.

## 4. Anatomy of a Pod

**Definition:** `metadata` (name, labels), `spec` (containers, volumes, restartPolicy), `status` (phase, conditions, IPs).

**Chai:** Order slip has customer name (metadata), recipe details (spec), and kitchen status (status).

## 5. Lifecycle

**Definition:** Phases: Pending, Running, Succeeded, Failed, Unknown. Container states: Waiting, Running, Terminated. Events: Scheduled, Pulling, Pulled, Created, Started.

**Chai:** Order status: Received → Preparing → Served → Done/Burnt.

## 6. Networking

**Definition:** Each Pod gets a unique cluster IP. All containers share network namespace, so `localhost` works between them. Port conflicts happen inside a Pod.

**Chai:** One table number per tray. Pots on same tray talk across the table, not across the shop.

## 7. Storage

**Definition:** Volumes are mounted into all containers. Types: emptyDir (ephemeral), configMap, secret, persistentVolumeClaim.

**Chai:** Tray liner shared by all pots. emptyDir is thrown away with tray. PVC is a permanent shelf.

## 8. Multi-container patterns

**Definition:** 
- Sidecar: helper container (logging)
- Ambassador: proxy
- Adapter: transforms output

**Chai:** Sidecar = assistant who refills sugar. Ambassador = waiter who takes orders. Adapter = translator for recipe.

## 9. Init Containers

**Definition:** Run to completion before app containers start. Used for setup, migrations, waiting for dependencies.

**Chai:** Heat water before brewing. No chai starts until water is hot.

## 10. Ephemeral Containers

**Definition:** Temporary containers for debugging running Pods, added via `kubectl debug`.

**Chai:** Health inspector jumps onto tray with thermometer, then leaves.

## 11. Probes

**Definition:** 
- Liveness: restart if unhealthy
- Readiness: remove from Service if not ready
- Startup: delay other probes for slow starts

**Chai:** Liveness = is cook alive. Readiness = is chai ready to serve. Startup = give extra time for first boil.

## 12. Resources and QoS

**Definition:** `requests` = guaranteed minimum. `limits` = maximum. QoS classes: Guaranteed, Burstable, BestEffort.

**Chai:** Request = table space you book. Limit = max gas you can use. Guaranteed = reserved stall.

## 13. Scheduling controls

**Definition:** nodeSelector, nodeAffinity, podAffinity, tolerations, taints.

**Chai:** "Put this tray only on gas stalls" or "keep dessert trays away from chai trays."

## 14. Security

**Definition:** securityContext (runAsUser, readOnlyRootFilesystem), serviceAccount for API access.

**Chai:** ID badge for cook, locked knife drawer.

## 15. Labels and Annotations

**Definition:** Labels = identifying key/value for selection. Annotations = non-identifying metadata.

**Chai:** Label = "masala" sticker for sorting. Annotation = "made by Rahul at 5pm" note.

## 16. Immutability

**Definition:** Most Pod fields cannot be changed after creation. You delete and recreate.

**Chai:** You cannot change tray size mid-service, you make a new tray.

## 17. Termination

**Definition:** SIGTERM sent, then grace period, then SIGKILL. preStop hook runs first.

**Chai:** "Last orders" bell, finish current cup, then clear table.

## 18. Static Pods

**Definition:** Pods managed directly by kubelet via manifest files, not API server.

**Chai:** Cook's personal recipe kept at stall, not in head office ledger.

## 19. Troubleshooting

**Definition:** Use `describe` for events, `logs` for output, `exec` for shell, `get -o yaml` for spec.

**Chai:** Check ticket, taste chai, ask cook, read recipe.

## 20. Best Practices

1. One main container per Pod unless tightly coupled
2. Always set requests/limits
3. Always add readiness probe
4. Never use bare Pods in production — use Deployments
5. Use labels consistently

---

Next: Day 3 — Deployments (why Pods need a manager)
