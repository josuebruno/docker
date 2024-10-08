# Comandos Docker 
### Listar contêineres em execução
	docker container ls

### Listar todos os contêineres (em execução e parados)
	docker container ls -a

### Executar um contêiner interativo com TTY

	docker container run -ti <id>

	Docker container attach <id>

### Rodar um contêiner em segundo plano (daemon)
	docker run -d nginx

### Acessar um contêiner em execução e abrir um shell

	docker container exec -ti <id_container> bash

	Docker container stop <id>

	Docker container start <id>

	Docker container restart <id> 

	Docker container pause <id>

	Docker container unpause <id>


### inspecionar.

	Docker container inspect <id>

### ver logs 
	Docker container logs -f  <id>

### matar container 

	Docker container rm -f <id>

### recurssos 

	Docker container stats <id>
	Docker container top <id>

### update do container 

	Docker container updade 

### Criando uma Imagem Docker com Dockerfile

Um Dockerfile é um script de texto simples que contém uma coleção de instruções para construir uma imagem Docker. Aqui estão as principais etapas e instruções para criar uma imagem Docker usando um Dockerfile:

Estrutura Básica de um Dockerfile

FROM: Define a imagem base que será usada para construir a nova imagem. É o ponto de partida da sua imagem.

dockerfile
Copiar código
FROM ubuntu:20.04
LABEL: Adiciona metadados à imagem, como informações de manutenção ou versão.

dockerfile
Copiar código
LABEL maintainer="seu-email@exemplo.com"
RUN: Executa comandos durante a construção da imagem, como instalar pacotes ou configurar o sistema.

dockerfile
Copiar código
RUN apt-get update && apt-get install -y nginx
COPY ou ADD: Copia arquivos ou diretórios do sistema de arquivos do host para o sistema de arquivos da imagem.

dockerfile
Copiar código
COPY ./arquivo-local /diretorio-no-container
WORKDIR: Define o diretório de trabalho para os comandos seguintes.

dockerfile
Copiar código
WORKDIR /app
ENV: Define variáveis de ambiente.

dockerfile
Copiar código
ENV PORT 8080
EXPOSE: Expõe uma porta que será utilizada pelo contêiner em execução.

dockerfile
Copiar código
EXPOSE 80
CMD: Especifica o comando que será executado quando o contêiner iniciar. Apenas um comando CMD pode estar presente, sendo o último CMD encontrado o que será usado.

dockerfile
Copiar código
CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT: Define o executável padrão que será iniciado quando o contêiner rodar. Pode ser usado em conjunto com CMD para fornecer argumentos.

dockerfile
Copiar código
ENTRYPOINT ["python3"]
CMD ["app.py"]
Exemplo de Dockerfile
dockerfile
Copiar código

### Imagem base
FROM ubuntu:20.04

### Metadados
LABEL maintainer="seu-email@exemplo.com"

### Atualiza o sistema e instala o Nginx
RUN apt-get update && apt-get install -y nginx

### Copia arquivos para o contêiner
COPY . /usr/share/nginx/html

### Define o diretório de trabalho
WORKDIR /usr/share/nginx/html

### Define uma variável de ambiente
ENV ENV_VAR_EXEMPLO valor

### Expõe a porta 80
EXPOSE 80

### Comando a ser executado quando o contêiner inicia


	CMD ["nginx", "-g", "daemon off;"]
Construindo a Imagem
Para construir uma imagem a partir de um Dockerfile, navegue até o diretório onde o Dockerfile está localizado e execute o seguinte comando:

#### Copiar código
	docker build -t nome-da-imagem:tag .
-t nome-da-imagem:tag: Define o nome e a tag da imagem (a tag é opcional, mas útil para versionamento).
.: Especifica o contexto de construção, que geralmente é o diretório atual.
Verificando a Imagem Criada
Após a construção, você pode listar todas as imagens Docker no seu sistema com:

#### Copiar código
	docker images
Executando um Contêiner da Imagem


#### Para criar e iniciar um contêiner a partir da imagem que você acabou de criar:


	docker run -d -p 80:80 nome-da-imagem:tag
-d: Executa o contêiner em modo desanexado (em segundo plano).
-p 80:80: Mapeia a porta 80 do contêiner para a porta 80 do host.
nome-da-imagem:tag: Especifica a imagem e a tag para criar o contêiner.

Considerações Finais
Certifique-se de manter seus Dockerfiles simples e reutilizáveis.
Sempre use versões específicas de imagens base para garantir consistência.
Evite adicionar arquivos desnecessários ao contêiner para reduzir o tamanho da imagem.


### docker volumes

#### Comando para iniciar um contêiner Docker

O comando abaixo é utilizado para iniciar um contêiner Docker utilizando a imagem `ubuntu`. Ele também monta um diretório do sistema de arquivos host dentro do contêiner.

	docker run -ti --mount type=bind,src=/home/josue/opt/volumebindo,dst=/novobindo ubuntu 
 
### Explicação

- **`docker run`**: Inicia um novo contêiner.

- **`-ti`**: Executa o contêiner em modo interativo (`-i`) e aloca um terminal TTY (`-t`), permitindo que você interaja com o contêiner através da linha de comando.

- **`--mount type=bind,src=/home/josue/opt/volumebindo,dst=/novobindo`**: Monta um diretório do sistema de arquivos host dentro do contêiner.

  - **`type=bind`**: Define o tipo de montagem como `bind`, o que significa que o diretório do host é montado no contêiner.
  - **`src=/home/josue/opt/volumebindo`**: Especifica o caminho do diretório no host que será montado.
  - **`dst=/novobindo`**: Define o caminho de destino dentro do contêiner onde o diretório do host será montado.

- **`ubuntu`**: Especifica a imagem do Docker a ser utilizada para criar o contêiner. Neste caso, a imagem é baseada no sistema operacional Ubuntu.

## Comando para iniciar um contêiner Docker com volume

O comando abaixo é utilizado para iniciar um contêiner Docker utilizando a imagem `ubuntu`. Ele também monta um volume Docker dentro do contêiner.

	
	docker run -ti --mount type=volume,src=teste,dst=/novobindo ubuntu
## Explicação

- **`docker run`**: Inicia um novo contêiner.

- **`-ti`**: Executa o contêiner em modo interativo (`-i`) e aloca um terminal TTY (`-t`), permitindo que você interaja com o contêiner através da linha de comando.

- **`--mount type=volume,src=teste,dst=/novobindo`**: Monta um volume Docker dentro do contêiner.

  - **`type=volume`**: Define o tipo de montagem como volume. Volumes são utilizados para persistência de dados, permitindo que os dados sejam armazenados fora do ciclo de vida do contêiner.
  - **`src=teste`**: Especifica o nome do volume a ser utilizado. Se o volume não existir, ele será criado automaticamente.
  - **`dst=/novobindo`**: Define o caminho de destino dentro do contêiner onde o volume será montado.

- **`ubuntu`**: Especifica a imagem do Docker a ser utilizada para criar o contêiner. Neste caso, a imagem é baseada no sistema operacional Ubuntu.

## Criando um volume Docker

No Docker, existem dois tipos principais de volumes: **Bind** e **Volume**. Cada tipo de volume serve a diferentes propósitos e oferece diferentes funcionalidades.

## Tipos de Volumes

### Bind Mount

- **Descrição**: Liga diretamente um diretório do sistema de arquivos do host a um diretório dentro do contêiner.
- **Exemplo**: 

  ```bash
  docker run -ti --mount type=bind,src=/home/josue/opt/volumebindo,dst=/novobindo ubuntu

## Volumes no Docker

Volumes são uma das formas mais eficazes de gerenciar dados persistentes no Docker. Eles são gerenciados pelo Docker e armazenados em um local padrão no sistema de arquivos do host, sendo ideais para a persistência de dados e para garantir que as informações não sejam perdidas quando o contêiner é removido.

### Características dos Volumes

- **Persistência**: Volumes armazenam dados fora do ciclo de vida dos contêineres, garantindo que as informações persistam mesmo após a remoção do contêiner.
- **Gerenciamento**: São gerenciados diretamente pelo Docker, facilitando tarefas como criação, remoção e inspeção.
- **Portabilidade**: Volumes são mais portáveis do que Bind Mounts, pois não dependem da estrutura de diretórios do host.

### Criando e Utilizando um Volume

Antes de usar um volume em um contêiner, é necessário criá-lo. A seguir, são apresentados os passos para criar e usar um volume chamado `volume1`.

#### Criação do Volume

Para criar um volume, use o comando:
	
	docker volume create volume1 


Depois de criar o volume, ele pode ser montado em um contêiner:

	docker run -ti --mount type=volume,src=volume1,dst=/dados ubuntu
