# Day 2 — Pod Commands Cheatsheet

## Create and inspect
kubectl apply -f pod.yaml     &emsp;&emsp; &emsp;&emsp;    # create Pod from YAML <br>
kubectl get pods             &emsp;&emsp; &emsp;&emsp;       # list Pods <br>
kubectl get pods -o wide         &emsp;&emsp; &emsp;&emsp;   # see Node and IP <br>
kubectl get pod chai-pod -o yaml   &emsp;&emsp; &emsp;&emsp;    # full spec and status <br>
kubectl describe pod chai-pod     &emsp;&emsp; &emsp;&emsp;     # events and conditions <br>
<br> <br>
## Interact
kubectl logs chai-pod             &emsp;&emsp; &emsp;&emsp;    # logs of first container <br>
kubectl logs chai-pod -c logger   &emsp;&emsp; &emsp;&emsp;     # logs of sidecar <br>
kubectl logs -f chai-pod          &emsp;&emsp; &emsp;&emsp;     # follow logs <br>
kubectl exec -it chai-pod -- sh   &emsp;&emsp; &emsp;&emsp;    # shell into Pod<br> 
kubectl exec -it chai-pod -c brewer -- bash <br>
<br><br>
## Debug
kubectl debug -it chai-pod --image=busybox --target=brewer &emsp;&emsp; &emsp;&emsp; # ephemeral container<br>
kubectl port-forward pod/chai-pod 8080:80  &emsp;&emsp; &emsp;&emsp; # access Pod locally<br>
kubectl cp chai-pod:/var/log/app.log ./app.log<br>
<br><br>
## Lifecycle
kubectl delete pod chai-pod      &emsp;&emsp; &emsp;&emsp;      # delete Pod<br>
kubectl delete -f pod.yaml<br>
kubectl replace --force -f pod.yaml  &emsp;&emsp; &emsp;&emsp;  # recreate<br>
<br><br>
## Advanced
kubectl set resources pod chai-pod --requests=cpu=100m,memory=128Mi<br>
kubectl label pod chai-pod env=dev<br>
kubectl annotate pod chai-pod owner=rahul<br>
kubectl get pods --field-selector=status.phase=Running<br>
kubectl get pods -l app=chai<br>
