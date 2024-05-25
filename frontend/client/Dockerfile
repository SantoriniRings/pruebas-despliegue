# Usa una imagen base de Node.js
FROM node:16-alpine

# Establece el directorio de trabajo en /app-frontend
WORKDIR /app-frontend

# Copia el package.json y el package-lock.json (si existe)
COPY package*.json ./

# Instala las dependencias de npm
RUN npm install

# Copia el resto del código del front-end
COPY . .

# Construye la aplicación de React
RUN npm run build

# Usa una imagen ligera de servidor web para servir la aplicación estática
FROM nginx:alpine
COPY --from=0 /app-frontend/dist /usr/share/nginx/html

# Expone el puerto 80
EXPOSE 80

# Comando para ejecutar nginx
CMD ["nginx", "-g", "daemon off;"]
