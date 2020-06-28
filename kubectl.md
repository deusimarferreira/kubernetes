# Kubectl
Você irá encontrar as dicas aqui apresentadas e outras em [Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/), na prova de certificação somente a documentação oficial poderá ser consulta.

## Instalação
https://kubernetes.io/docs/tasks/tools/install-kubectl/

> Dica: O comando **kubectl** será executado por diversas vezes, para facilitar você pode ativa o preencimendo automátio do bash.  
~~~sh
$ sudo apt-get install bash-completion -y
$ source <(kubectl completion bash)
$ echo "source <(kubectl completion bash)" >> ~/.bashrc
~~~

## JSON
~~~bash
# Output configs to JSON format
$ kubectl get pods -o json

# Output configs to JSON format with JSONPATH
$ kubectl get pods -A -o=jsonpath='{.items[0].spec.containers[0].image}'
$ kubectl get pods -A -o=jsonpath='{.items[0].spec.containers[0].name}{"\n"}{.items[0].spec.containers[0].image}'

# Output configs to JSON format with JSONPATH + function range
$ kubectl get nodes -A -o=jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.capacity.cpu}{"\n"}{end}'

# Custom columns
$ kubectl get nodes -o=custom-columns=NODE:.metadata.name ,CPU:.status.capacity.cpu
~~~

[Clique aqui](/json.md) para mas dicas sobre JSON PATH.

## Sort By

~~~bash
$ kubectl get nodes --sort-by=.metadata.name
$ kubectl get nodes --sort-by=.status.capacity.cpu
~~~
