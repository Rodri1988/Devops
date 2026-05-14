# ETAPA 1: Construcción (Build)
# Usamos node:18-alpine para una imagen de construcción ligera
FROM node:18-alpine AS build
WORKDIR /app

# Copiamos archivos de dependencias para aprovechar el caché de capas
COPY package*.json ./
RUN npm install

# Copiamos el resto del código y construimos la app
COPY . .
RUN npm run build

# ETAPA 2: Producción (Servidor Web)
# Usamos nginx:alpine para que la imagen final sea extremadamente pequeña y segura
FROM nginx:alpine

# Copiamos el resultado del 'build' anterior a la carpeta que sirve Nginx
# Nota: Si tu carpeta de salida es 'build' en lugar de 'dist', cambia /app/dist por /app/build
COPY --from=build /app/dist /usr/share/nginx/html

# Exponemos el puerto 80 para el tráfico HTTP
EXPOSE 80

# Comando para ejecutar Nginx en primer plano
CMD ["nginx", "-g", "daemon off;"]
