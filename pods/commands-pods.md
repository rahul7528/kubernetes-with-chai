# Day 2 — Pod Commands Cheatsheet

## Create and inspect
kubectl apply -f pod.yaml     &emsp;&emsp;      # create Pod from YAML <br>
kubectl get pods             &nbsp;&nbsp;          # list Pods <br>
kubectl get pods -o wide          &nbsp;&nbsp;     # see Node and IP <br>
kubectl get pod chai-pod -o yaml   &nbsp;&nbsp;    # full spec and status <br>
kubectl describe pod chai-pod     &nbsp;&nbsp;     # events and conditions <br>
<br> <br>
## Interact
kubectl logs chai-pod             &nbsp;&nbsp;     # logs of first container <br>
kubectl logs chai-pod -c logger   &nbsp;&nbsp;     # logs of sidecar <br>
kubectl logs -f chai-pod          &nbsp;&nbsp;     # follow logs <br>
kubectl exec -it chai-pod -- sh   &nbsp;&nbsp;     # shell into Pod<br> 
kubectl exec -it chai-pod -c brewer -- bash <br>
<br><br>
## Debug
kubectl debug -it chai-pod --image=busybox --target=brewer &nbsp;&nbsp; # ephemeral container<br>
kubectl port-forward pod/chai-pod 8080:80  &nbsp;&nbsp; # access Pod locally<br>
kubectl cp chai-pod:/var/log/app.log ./app.log<br>
<br><br>
## Lifecycle
kubectl delete pod chai-pod      &nbsp;&nbsp;      # delete Pod<br>
kubectl delete -f pod.yaml<br>
kubectl replace --force -f pod.yaml  &nbsp;&nbsp;  # recreate<br>
<br><br>
## Advanced
kubectl set resources pod chai-pod --requests=cpu=100m,memory=128Mi<br>
kubectl label pod chai-pod env=dev<br>
kubectl annotate pod chai-pod owner=rahul<br>
kubectl get pods --field-selector=status.phase=Running<br>
kubectl get pods -l app=chai<br>
