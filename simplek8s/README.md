```
minikube start

kubectl apply -f client-pod.yaml
kubectl apply -f client-node-port.yaml

minkube ip
http://192.168.49.2:31515/

kubectl set image deployment/client-deployment client=stephengrider/multi-client:v5
eval $(minikube docker-env)
kubectl logs client-deployment-sdfsf242
kubectl exec -it client-deployment-sdfsf242 sh
```
