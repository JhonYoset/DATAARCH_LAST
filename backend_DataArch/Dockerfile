# Dockerfile para Backend (NestJS)
FROM node:18-alpine

# Establecer directorio de trabajo
WORKDIR /app

# Copiar archivos de dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm ci

# Copiar código fuente
COPY . .

# Exponer puerto
EXPOSE 3001

# Comando por defecto (se sobrescribe en docker-compose)
CMD ["npm", "run", "start:dev"]