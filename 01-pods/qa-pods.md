# Day 2 — Pods Q&A (Basic to Advanced)

## Q1. What is a Pod?
**Definition:** Smallest deployable unit, group of 1+ containers sharing network and storage.
**Chai:** Steel tray carrying pots together.

## Q2. Can a Pod span two Nodes?
**Definition:** No. A Pod is atomic and scheduled to one Node.
**Chai:** One tray cannot be on two stalls.

## Q3. How do containers in same Pod communicate?
**Definition:** Via localhost and shared volumes because they share network namespace.
**Chai:** Pots on same tray slide sugar across the table.

## Q4. What happens when you delete a Pod?
**Definition:** All containers terminate, IP released, emptyDir lost. No auto-recreate.
**Chai:** Tray thrown in sink. Stall stays open.

## Q5. Difference between Pod and Deployment?
**Definition:** Pod is single instance. Deployment is controller that maintains desired number of Pods.
**Chai:** Tray vs shift manager who keeps 3 trays ready.

## Q6. What are init containers used for?
**Definition:** Setup tasks that must complete before app starts.
**Chai:** Heating water before brewing.

## Q7. Explain liveness vs readiness.
**Definition:** Liveness restarts container on failure. Readiness removes Pod from Service traffic.
**Chai:** Liveness = replace dead cook. Readiness = stop serving unfinished chai.

## Q8. What is Pod IP lifecycle?
**Definition:** Assigned on creation, released on deletion. New Pod gets new IP.
**Chai:** Table number given when tray placed, freed when cleared.

## Q9. Can two containers in same Pod use same port?
**Definition:** No. They share port space, conflict occurs.
**Chai:** Two pots cannot occupy same spot on tray.

## Q10. What are requests vs limits?
**Definition:** Requests guarantee resources, limits cap usage.
**Chai:** Booked table space vs max gas allowed.

## Q11. What is QoS Guaranteed?
**Definition:** Every container has equal requests and limits for CPU and memory.
**Chai:** VIP reservation with fixed stall and gas.

## Q12. How to troubleshoot a CrashLoopBackOff Pod?
**Definition:** Check `describe` for events, `logs --previous` for crash reason, verify probes and resources.
**Chai:** Check ticket, taste last failed chai, see if cook ran out of gas.

## Q13. What is a static Pod?
**Definition:** Pod defined in kubelet manifest directory, not via API server.
**Chai:** Cook's personal recipe not in head office.

## Q14. Why are Pods immutable?
**Definition:** Ensures predictable scheduling and state. Changes require new Pod.
**Chai:** Cannot resize tray mid-service.

## Q15. How does graceful termination work?
**Definition:** SIGTERM, preStop hook, grace period, then SIGKILL.
**Chai:** Last call bell, finish cup, then clear.
