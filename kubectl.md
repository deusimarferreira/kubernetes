# Kubectl
Você irá encontrar as dicas aqui apresentadas e outras em [kubectl CLI](https://kubernetes.io/docs/reference/kubectl/), na prova de certificação somente a documentação oficial poderá ser consulta.

## Instalação
https://kubernetes.io/docs/tasks/tools/install-kubectl/

> Dica: O comando **kubectl** será executado por diversas vezes, para facilitar você pode ativa o preencimendo automátio do bash.  
~~~sh
$ sudo apt-get install bash-completion -y
$ source <(kubectl completion bash)
$ echo "source <(kubectl completion bash)" >> ~/.bashrc
~~~

## Uso
Antes de continuar recomento fazer uma leitura na [kubectl sintaxe](https://kubernetes.io/docs/reference/kubectl/overview/#syntax)

### Comandos
Comandos e operação conforme documentação do Kubernetes são a mesma coisa, a tabela completa pode ser encontrada [aqui](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) ou [aqui](https://kubernetes.io/docs/reference/kubectl/overview/#operations).

~~~sh
$ kubectl get
$ kubectl create
$ kubectl expose
~~~

### Tipos de recursos
Os tipos de recursos suportados pelo ``kubectl`` podem ser consultados nos [docs](https://kubernetes.io/docs/reference/kubectl/overview/#resource-types) ou executando o comando ``kubectl api-resources``.

Um observação interessante é que os recursos podem serem informados no sigular, plural ou alias.

~~~sh
$ kubectl get pod -A # Singular
$ kubectl get pods -A # Plural
$ kubectl get po -A # Alias
~~~

### Saídas
As saídas ou simplismente outputs, auxilia quando desejamos validar alguma configuração ou exporta-lá. Você pode utilizar a flag ``--output`` ou seu alias ``-o`` e definir o tipo de saída ``-o json``, consulte a documentação oficial caso tenha dúvidas sobre a [sintaxe](https://kubernetes.io/docs/reference/kubectl/overview/#syntax-1).

Aqui irei apresentar os mais utilizados no dia-a-dia, para consultar todos [clique aqui](https://kubernetes.io/docs/reference/kubectl/overview/#output-options).

~~~sh
$ kubectl get pods -o json
$ kubectl get pods -o yaml
$ kubectl get pods -o name # Imprime somente nome
$ kubectl get pods -o wide # Imprime uma tabela em plain-text
~~~

#### jsonpath
Vale observa que no Windows o jsonpath irá funcionar somente invertendo os tipos de aspas, ou seja, onde você utilizar aspas simples deverá substituir por aspas duplas e vice-versa.

~~~sh
# Output configs to JSON format with JSONPATH
$ kubectl get pods -A -o jsonpath='{.items[0].spec.containers[0].image}'
$ kubectl get pods -A -o jsonpath='{.items[0].spec.containers[0].name}{"\n"}{.items[0].spec.containers[0].image}'
$ kubectl get pods -o=jsonpath="{.items[*]['metadata.name', 'status.hostIP']}"

# Output configs to JSON format with JSONPATH + function range
$ kubectl get nodes -A -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.capacity.cpu}{"\n"}{end}'

# Usando estrutura de comparação
$ kubectl get pods -o jsonpath='{.items[?(@.kind=="Pod")].spec.containers[?(@.name=="nginx")].volumeMounts[?(@.readOnly==true)].mountPath}'
~~~

[Clique aqui](/json.md) para mas dicas sobre JSON PATH.

#### custom-columns
Para conhecer mais sobre saídas usando ``custom-columns`` [clique aqui](https://kubernetes.io/docs/reference/kubectl/overview/#custom-columns).
~~~sh
# Custom columns
$ kubectl get nodes -o custom-columns=NODE:.metadata.name,CPU:.status.capacity.cpu,HOST:.status.addresses[*].address
~~~

### Sort By

~~~bash
$ kubectl get nodes --sort-by=.metadata.name
$ kubectl get nodes --sort-by=.status.capacity.cpu
~~~
