```
eksctl create cluster -f eks-cluster.yaml
```

```
kubectl create namespace ns-eks-course
kubectl patch storageclass gp2 -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

```
kubectl apply -f pvcs.yaml --namespace=ns-eks-course
```

```
kubectl create secret generic mysql-pass --from-literal=password=eks-course-mysql-pw --namespace=ns-eks-course
kubectl apply -f deploy-mysql.yaml --namespace=ns-eks-course
```

```
eksctl delete cluster -f eks-cluster.yaml
```