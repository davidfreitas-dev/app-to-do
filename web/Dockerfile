# obtém a versão mais atual e estável do NodeJS 
FROM node:lts-alpine

# define o diretorio principal
WORKDIR /app

# faz uma cópia para o diretorio principal
COPY package.json ./

# instala as dependências do projeto
RUN npm install

# instala as dependências Vue Cli
RUN npm install -g @vue/cli