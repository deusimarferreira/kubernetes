# APIs e Acessos

~~~sh
kubectl auth can-i create deployments
kubectl auth can-i create deployments --as bob
kubectl auth can-i create deployments --as bob --namespace developer

# Annotations
kubectl annotate pods --all description='Production Pods' -n pod
kubectl annotate --overwrite pods description='Old Production Pods' -n pod
kubectl annotate pods foo description- -n pod

kubectl --v=10 get pods firstpod
~~~