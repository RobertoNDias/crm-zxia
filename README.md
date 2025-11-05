# CRM ZXIA

Este repositório contém a stack do CRM ZXIA com:

- Backend Node.js (Whaticket modificado) com modo demo (`DISABLE_WHATSAPP=true`).
- Frontend estático servido por Nginx, com variáveis de branding.
- Arquivo `docker-stack.yml` para orquestração em Swarm/Traefik.

## Estrutura

- `backend/Dockerfile`: imagem do backend baseada em `node:18-alpine` rodando `dist/server.js`.
- `frontend/Dockerfile`: imagem do frontend baseada em `nginx:alpine` servindo `build/` com `envsubst`.
- `docker-stack.yml`: serviços `backend`, `frontend`, `mysql` e `redis` prontos para deploy.

## Build local das imagens

Backend:
```
docker build -t produtosdigitaisrd/crm-zxia-backend:dev backend
```
Frontend:
```
docker build -t produtosdigitaisrd/crm-zxia-frontend:dev frontend
```

## Push para Docker Hub

1. Faça login: `docker login`
2. Suba as imagens:
```
docker push produtosdigitaisrd/crm-zxia-backend:dev
docker push produtosdigitaisrd/crm-zxia-frontend:dev
```

## Deploy com docker stack

Edite `docker-stack.yml` substituindo as imagens pelo repositório desejado (Docker Hub) e aplique:
```
docker stack deploy -c docker-stack.yml crm-zxia
```

> Observação: Em modo demo (`DISABLE_WHATSAPP=true`), rotas `/whatsapp` são liberadas para evitar erros 401, mantendo autenticação normal nas demais rotas.
