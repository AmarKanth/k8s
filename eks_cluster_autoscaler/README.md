eksctl create cluster -f eks-cluster.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml
(if default config doent work create override cluster-autoscaler service account with autoslacing policies)

kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"
kubectl -n kube-system edit deployment.apps/cluster-autoscaler
kubectl -n kube-system describe deployment cluster-autoscaler

kubectl apply -f nginx-deployment.yml
kubectl scale --replicas=30 deployment/test-autoscaler
kubectl -n kube-system logs -f deployment.apps/cluster-autoscaler
eksctl delete cluster -f eks-cluster.yaml