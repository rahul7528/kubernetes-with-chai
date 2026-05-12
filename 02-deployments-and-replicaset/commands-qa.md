# Commands for ReplicaSet and Deployment <br><br>
<br>
# REPLICA SET<br>
kubectl apply -f rs.yaml<br>
kubectl get rs<br>
kubectl describe rs rs-basic<br>
kubectl get pods -l app=rs-demo<br>
kubectl scale rs rs-basic --replicas=5<br>
kubectl delete rs rs-basic<br>
<br><br>
# DEPLOYMENT<br>
kubectl apply -f deploy.yaml<br>
kubectl get deploy,rs,pods -l app=deploy-demo<br>
kubectl describe deploy deploy-basic<br>
kubectl rollout status deploy/deploy-basic<br>
kubectl set image deploy/deploy-basic web=nginx:1.26<br>
kubectl rollout history deploy/deploy-basic<br>
kubectl rollout undo deploy/deploy-basic<br>
kubectl rollout pause deploy/deploy-basic<br>
kubectl rollout resume deploy/deploy-basic<br>
<br><br>
# Q&A<br>
<br><br>
Q1: What is ReplicaSet?<br>
Definition: Controller that maintains Pod replicas via selector.<br>
Chai: Roster keeping 3 trays ready.<br>
<br>
Q2: What is Deployment?<br>
Definition: Manages ReplicaSets for rollouts and rollbacks.<br>
Chai: Shift manager swapping recipes.<br>
<br>
Q3: Why does Deployment create new ReplicaSet on change?<br>
Definition: Pod template hash changes, Pods immutable.<br>
Chai: New recipe needs new roster.<br>
<br>
Q4: Delete Pod in Deployment?<br>
Definition: ReplicaSet recreates immediately.<br>
Chai: Tray falls, manager replaces.<br>
<br>
Q5: Difference between RS and Deployment in production?<br>
Definition: Use Deployment always, RS is implementation detail.<br>
Chai: Talk to manager, not roster directly.<br>
