# Definido limites de recurso para um Namespace

~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su

# Criando namespace
kubectl create namespace low-usage-limit

# Verifique o namescpace que acabamos de criar
kubectl get namespace
~~~

> Definindo limetes de recursos

~~~txt
apiVersion: v1
kind: LimitRange
metadata:
    name: low-resource-range
spec:
    limits:
    - default:
        cpu: 1
        memory: 500Mi
      defaultRequest:
        cpu: 0.5
        memory: 100Mi
      type: Container
~~~


~~~sh
kubectl --namespace=low-usage-limit \
    create -f low-resource-range.yaml

kubectl get LimitRange
    No resources found in default namespace.

kubectl get LimitRange --all-namespaces
NAMESPACE         NAME                 CREATED AT
low-usage-limit   low-resource-range   2020-04-14T00:31:45Z

# Criar deplymento defindo namespace
kubectl -n low-usage-limit \
    create deployment limited-hog --image vish/stress

# Visualizar deply
kubectl get deployments --all-namespaces

# Visualizar pod do namespace
kubectl -n low-usage-limit get pods

# Yaml config
kubectl -n low-usage-limit \
    get pod limited-hog-2556092078-wnpnv -o yaml

cp hog.yaml hog2.yaml
~~~

> Definindo namespace via YAML

~~~txt
    ...
    namespace: low-usage-limit
    ...
~~~

~~~sh
kubectl create -f hog2.yaml

kubectl get deployments --all-namespaces

# Vamos limpar tudo
kubectl -n low-usage-limit delete deployment hog
kubectl delete deployment hog
kubectl -n low-usage-limit delete deployment limited-hog
~~~