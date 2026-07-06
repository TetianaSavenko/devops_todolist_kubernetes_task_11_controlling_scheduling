# Validation Instructions

## 1. Check for labels and Taints on nodes
kubectl get nodes --show-labels
kubectl describe nodes | grep -A5 "Taints"

## 2. Check that MySQL pods are on nodes with the label app=mysql
kubectl get pods -l app=mysql -n todoapp -o wide
# The NODE column should only show nodes with the label app=mysql

## 3. Check that MySQL pods are NOT on the same node (Anti-Affinity)
kubectl get pods -l app=mysql -n todoapp -o wide | awk '{print $1, $7}'
# Each pod should be on a separate node

## 4. Check that the todoapp Pod has started
kubectl get pod todoapp -n todoapp -o wide
# Check the NODE column — there should be a node with the label app=todoapp (if any)

## 5. Check that the todoapp Deployment pods are on the correct nodes
kubectl get pods -l app=todoapp -n todoapp -o wide
# Pods should be on nodes with app=todoapp or others (preferred — not required)

## 6. Check Anti-Affinity for todoapp (different nodes)
kubectl get pods -l app=todoapp -n todoapp -o wide | awk '{print $1, $7}'
# None of the pods should be on the same node

## 7. Detailed check of pod affinity rules
kubectl describe pod todoapp -n todoapp | grep -A20 "Node-Selectors\|Tolerations\|Affinity"

## 8. Check Scheduler Events
kubectl describe pod todoapp -n todoapp | grep -A10 "Events"