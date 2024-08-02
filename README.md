############## Comandos Docker ##################

# Listar contêineres em execução
docker container ls

# Listar todos os contêineres (em execução e parados)
docker container ls -a

# Executar um contêiner interativo com TTY
docker container run -ti ubuntu
Docker container attach <id>

# Rodar um contêiner em segundo plano (daemon)
docker run -d nginx

# Acessar um contêiner em execução e abrir um shell
docker container exec -ti <id_container> bash


Docker container stop <id>
Docker container start <id>
Docker container restart <id> 
Docker container pause <id>
Docker container unpause <id>


#inspecionar.

	Docker container inspect <id>

#ver logs 
	Docker container logs -f  <id>

#matar container 

	Docker container rm -f <id>

#recurssos 

	Docker container stats <id>
	Docker container top <id>

#update do container 

	Docker container updade 

Criando uma Imagem Docker com Dockerfile
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
# Imagem base
FROM ubuntu:20.04

# Metadados
LABEL maintainer="seu-email@exemplo.com"

# Atualiza o sistema e instala o Nginx
RUN apt-get update && apt-get install -y nginx

# Copia arquivos para o contêiner
COPY . /usr/share/nginx/html

# Define o diretório de trabalho
WORKDIR /usr/share/nginx/html

# Define uma variável de ambiente
ENV ENV_VAR_EXEMPLO valor

# Expõe a porta 80
EXPOSE 80

# Comando a ser executado quando o contêiner inicia
CMD ["nginx", "-g", "daemon off;"]
Construindo a Imagem
Para construir uma imagem a partir de um Dockerfile, navegue até o diretório onde o Dockerfile está localizado e execute o seguinte comando:

bash
Copiar código
docker build -t nome-da-imagem:tag .
-t nome-da-imagem:tag: Define o nome e a tag da imagem (a tag é opcional, mas útil para versionamento).
.: Especifica o contexto de construção, que geralmente é o diretório atual.
Verificando a Imagem Criada
Após a construção, você pode listar todas as imagens Docker no seu sistema com:

bash
Copiar código
docker images
Executando um Contêiner da Imagem
Para criar e iniciar um contêiner a partir da imagem que você acabou de criar:

bash
Copiar código
docker run -d -p 80:80 nome-da-imagem:tag
-d: Executa o contêiner em modo desanexado (em segundo plano).
-p 80:80: Mapeia a porta 80 do contêiner para a porta 80 do host.
nome-da-imagem:tag: Especifica a imagem e a tag para criar o contêiner.
Considerações Finais
Certifique-se de manter seus Dockerfiles simples e reutilizáveis.
Sempre use versões específicas de imagens base para garantir consistência.
Evite adicionar arquivos desnecessários ao contêiner para reduzir o tamanho da imagem.


