# ============================================
# Imagen base
# ============================================
# Utilizamos Node.js 22 como sistema operativo
# donde se ejecutará nuestra aplicación.
FROM node:22

# ============================================
# Directorio de trabajo
# ============================================
# Todo lo que haga Docker ocurrirá dentro
# de la carpeta /app del contenedor.
WORKDIR /app

# ============================================
# Copiar archivos de dependencias
# ============================================
# Primero copiamos únicamente package.json
# y package-lock.json para aprovechar la
# caché de Docker.
COPY package*.json ./

# ============================================
# Instalar dependencias
# ============================================
# Instala todas las dependencias del proyecto.
RUN npm install

# ============================================
# Copiar el proyecto
# ============================================
# Ahora copiamos todo el código fuente
# al contenedor.
COPY . .

# ============================================
# Generar Prisma Client
# ============================================
# Prisma crea el cliente que utilizará
# nuestra aplicación para conectarse a la BD.
RUN npx prisma generate

# ============================================
# Compilar TypeScript
# ============================================
# Convierte todo el proyecto de TypeScript
# a JavaScript y genera la carpeta dist/.
RUN npm run build

# ============================================
# Puerto de Express
# ============================================
# Indicamos que nuestra aplicación utilizará
# el puerto 3000.
EXPOSE 3000

# ============================================
# Inicio de la aplicación
# ============================================
# En producción ya no usamos ts-node-dev.
# Ejecutamos directamente la versión compilada.
CMD ["npm", "start"]