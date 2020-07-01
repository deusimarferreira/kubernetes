# Trabalhando com Restrições de CPU/Memória

## Instalação ``stress``
~~~sh
# Observação: Nesta sessão todos os comandos precisam ser executados com usuário não root/su

kubectl create deployment hog --image vish/stress

kubectl get deployments

kubectl describe deployment hog

kubectl get deployment hog -o yaml > hog.yaml
vim hog.yaml
~~~

> Definindo limetes de Memória

~~~txt
    ...
    resources:
        limits:
            memory: "2Gi"
        requests:
            memory: "250Mi"
    ...
~~~


~~~sh
# Atualiza configurações do pod
kubectl replace -f hog.yaml

# Visualizar container hog
kubectl get po

# Analizar logs
kubectl logs hog-5d7b54959f-hmgvz

vim hog.yaml
~~~

> Definindo limetes de CPU e Memória

~~~txt
    ...
    resources:
        limits:
            cpu: "4"
            memory: "4Gi"
        requests:
            cpu: "0.5"
            memory: "500Mi"
        args:
        - -cpus
        - "2"
        - -mem-total
        - "950Mi"
        - -mem-alloc-size
        - "100Mi"
        - -mem-alloc-sleep
        - "1s"
    ...
~~~

~~~sh
kubectl delete deployment hog

kubectl create -f hog.yaml
~~~