# ETAPA 1: Construcción del sitio
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# ETAPA 2: Servidor de Producción (Nginx)
FROM nginx:alpine
# Copiamos solo los archivos estáticos listos para el navegador
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
