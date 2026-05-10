# Day 2 — Pod Commands Cheatsheet

## Create and inspect
kubectl apply -f pod.yaml              # create Pod from YAML
kubectl get pods                       # list Pods
kubectl get pods -o wide               # see Node and IP
kubectl get pod chai-pod -o yaml       # full spec and status
kubectl describe pod chai-pod          # events and conditions

## Interact
kubectl logs chai-pod                  # logs of first container
kubectl logs chai-pod -c logger        # logs of sidecar
kubectl logs -f chai-pod               # follow logs
kubectl exec -it chai-pod -- sh        # shell into Pod
kubectl exec -it chai-pod -c brewer -- bash

## Debug
kubectl debug -it chai-pod --image=busybox --target=brewer  # ephemeral container
kubectl port-forward pod/chai-pod 8080:80   # access Pod locally
kubectl cp chai-pod:/var/log/app.log ./app.log

## Lifecycle
kubectl delete pod chai-pod            # delete Pod
kubectl delete -f pod.yaml
kubectl replace --force -f pod.yaml    # recreate

## Advanced
kubectl set resources pod chai-pod --requests=cpu=100m,memory=128Mi
kubectl label pod chai-pod env=dev
kubectl annotate pod chai-pod owner=rahul
kubectl get pods --field-selector=status.phase=Running
kubectl get pods -l app=chai
