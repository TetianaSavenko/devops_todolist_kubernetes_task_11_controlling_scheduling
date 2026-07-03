# Validation Instructions

## 1. Check Taint on nodes
kubectl describe nodes | grep -A5 Taints

## 2. Check that MySQL pods are only on mysql nodes
kubectl get pods -l app=mysql -o wide

## 3. Check that MySQL is not on the same node (Anti-Affinity)
kubectl get pods -l app=mysql -o wide | awk '{print $7}'

## 4. Check Node Affinity for todoapp
kubectl get pods -l app=todoapp -o wide

## 5. Check scheduler events
kubectl describe pod <pod-name> | grep -A10 Events