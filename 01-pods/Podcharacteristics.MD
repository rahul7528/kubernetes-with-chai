A Pod is a group of one or more containers that are:

co-scheduled
co-located
share the same network namespace
share storage volumes
run together as a single unit

Now understand what those words actually mean.

Co-scheduled

All containers inside a Pod are scheduled onto the same node.

Kubernetes does not split containers of a Pod across different machines.

If a Pod has:

app container
logging sidecar
monitoring agent

all of them go to the same worker node.

Co-located

Containers run close together on the same machine.

This allows:

fast communication
shared localhost networking
shared filesystem volumes

One container can call another using:

localhost

because they share the same network namespace.

Shared Network

Containers inside a Pod:

share IP address
share port space

Meaning:

If one container listens on port 8080,
another container inside the same Pod can access it via:

localhost:8080
Shared Storage

Containers can mount the same Kubernetes Volume.

Example:

app writes logs
sidecar reads logs

Both access same shared storage.

The Mental Model

A Pod is NOT “a container.”

A Pod is:

the smallest deployable unit in Kubernetes.

Containers inside a Pod are treated like tightly coupled roommates sharing:

house
WiFi
storage
electricity

That’s why sidecar architecture works so well in Kubernetes.
