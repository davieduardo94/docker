> # *[My Gists](https://gist.github.com/davieduardo94) |  [Repos](https://github.com/davieduardo94?tab=repositories)*

# Criação de contaiers
### 1 - Criação de container
 - O comando é enviado ao DOCKERD(Docker Deamon) e verifica se existe localmente, caso não encontre, ele solicita ao DockerHub.com e baixa a imagem.
```code
docker container run <image_name>
```
### 1.1 - Criando container e definindo nome do container
```
docker container run --name <container_name> <image_name>
```
  >EX:  docker container run --name meu_container ubunto

### 1.2 - Criando container no modo interativo
- Cria o container e ativa o shell do container criado
```
docker container run -it <image_name> <shell_location>
```
 >EX:  docker container run -it ubunto /bin/bash


### 1.3 - Container temporario ou executado e excluido:
- Cria o container, executa a ação dentro do contaier e o remove.
```
docker container run --name <id_container | container_name> --rm <image_name>
```
>EX: docker container run --name meu_container --rm ubunto

# Gerenciamento de containers
### 2 -  Listar todos containers criados
```
docker container ls -a
```
### 3 - Iniciar a execução de um container
```
docker container start <container_name>
```
### 3.1 - Parar execução de um container
```
docker container stop <id_container | container_name>
```
### 4 - Removendo container
```
docker container rm <id_container | contairner_name>
```
### 4.1 - Remoção forçada
 - Utilizado quando o container está em execução
 ```
 docker container rm -f <id_container | container_name>
 ```
### 5 - Executar comandos dentro do container
- Utilizado para containers em execução
```
docker container exec -it <id_container | container_name> <shell_location>
```
> EX: docker container exec -it meu_container /bin/bash

### 6 - Redirecionamento de portas (Port Binding)
```
docker container run -d -p <local_port>:<container_port> <image_name>
-d: detach mod
-p: port binding
```
>EX: docker container run -d -p 8080:80 nginx

# Troubleshooting
### 6 - Verificar a execução do container
```
docker container inspect <id_contaier | container_name>
```

### 7 - Verificar os logs de um container
```
docker container logs <id_container | container_name>
```
- Para limitar a quantidade de logs
```
docker container logs -n <log_quantitiy> <id_container | container_name>
```
> EX: docker container logs -n 5 meu_container
- Para seguir toda a execução do container e apresentar a cada atualização
```
docker container logs -f <id_container | container_name>
```
> EX: docker container logs -f meu_container
- Para apresentar a data e hora do log
```
docker container logs -t <id_container | container_name>
```
> EX: docker container logs -t meu_container

# Criação de imagens
- Imagens são um template para criar um container
- Nela são inseridos todos os elementos para criação do container
- Docker utiliza o overlay filesystem
- São criadas em camadas de inserção de fileSystem em modo somente leitura, o resultado final dessa junção é a imagem Docker que utilizamos, porem é a camada de Leitura e Escrita
  - Beneficios:
    - É possivel criar varios conteiners a partir de uma mesma imagem
    - Aproveitamento de espaço pois quando criamos um outro container e utilizamos a mesma imagem, o docker faz apenas a referencia dessa imagem, sem necessidade de fazer a copia.
    - Gerenciamento de recursos para cada container
### Formas para criação de Imagem
### Docker commit
  - Não é uma boa pratica, pois os comandos são em "Tempo real" sendo dificil replicar.
  - Cria a imagem baseada em um container
  - Insere as instruções dentro do container para assim, gerar a imagem final a partir do docker Commit
### Dockerfile
 - Modelo mais utilizado por boa pratica.
 - Segue uma "Receita" de instruções para criação de imagem baseado no Dockefile
#### Codigo para criação do Dockerfile
Definindo a origem da imagem
#
> FROM ubunto

Execução de comandos para construção 
Comando para atualização do repositorio Ubunto

> RUN apt-get-update

Comando para instalação do 'curl'

> RUN apt-get-install curl --yes

O arquivo final deve estar dessa forma
```
FROM ubunto
RUN apt-get-update
RUN apt-get-install curl --yes
```




