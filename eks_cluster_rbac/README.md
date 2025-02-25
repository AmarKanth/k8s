### Adding Admin User

+ Updating the AWS Auth ConfigMap
> The aws-auth ConfigMap in the kube-system namespace controls IAM authentication 
> for your Kubernetes cluster.
```
kubectl -n kube-system get configmap aws-auth -o yaml > aws-auth-configmap.yaml

mapUsers: |
    - userarn: arn:aws:iam::058264205719:user/k8s-cluster-admin
      username: k8s-cluster-admin
      groups: 
        - system:masters

kubectl apply -f aws-auth-configmap.yaml -n kube-system
```

+ Configuring AWS CLI for the Admin User
```
subl ~/.aws/credentials

[clusteradmin]
aws_access_key_id = *****
aws_secret_access_key = ****
region = ap-south-1

export AWS_PROFILE="clusteradmin"
aws sts get-caller-identity
```

+ Verifying Cluster Access
```
kubectl get nodes
```

### Adding Read-Only User