# Data Arch Labs - Configuración Local

## Requisitos Previos

1. **Node.js** (versión 18 o superior)
2. **PostgreSQL** (versión 12 o superior)
3. **Git**

## Configuración de Base de Datos

1. Instala PostgreSQL en tu sistema
2. Crea una base de datos llamada `data_arch_labs`:
   ```sql
   CREATE DATABASE data_arch_labs;
   ```
3. Asegúrate de que PostgreSQL esté ejecutándose en el puerto 5432

## Configuración del Backend

1. Navega al directorio del backend:
   ```bash
   cd backend_DataArch
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. El archivo `.env` ya está configurado con tus credenciales

4. Inicia el servidor de desarrollo:
   ```bash
   npm run start:dev
   ```

El backend estará disponible en: `http://localhost:3001`

## Configuración del Frontend

1. Navega al directorio del frontend:
   ```bash
   cd frontend_DataArch
   ```

2. Instala las dependencias:
   ```bash
   npm install
   ```

3. El archivo `.env` ya está configurado para conectar con el backend local

4. Inicia el servidor de desarrollo:
   ```bash
   npm run dev
   ```

El frontend estará disponible en: `http://localhost:5173`

## Configuración de Google OAuth

Para que la autenticación funcione correctamente, necesitas configurar las URLs de redirección en Google Cloud Console:

1. Ve a [Google Cloud Console](https://console.cloud.google.com/)
2. Selecciona tu proyecto
3. Ve a "APIs & Services" > "Credentials"
4. Edita tu OAuth 2.0 Client ID
5. Agrega estas URLs autorizadas:
   - **JavaScript origins**: `http://localhost:5173`
   - **Redirect URIs**: `http://localhost:3001/api/auth/google/callback`

## Verificación

1. Abre `http://localhost:5173` en tu navegador
2. El frontend debería cargar correctamente
3. Verifica que el backend responda en `http://localhost:3001/api`
4. Prueba el login con Google

## Estructura de Archivos de Configuración

```
backend_DataArch/
├── .env                 # Variables de entorno del backend
└── ...

frontend_DataArch/
├── .env                 # Variables de entorno del frontend
└── ...
```

## Comandos Útiles

### Backend
```bash
# Desarrollo
npm run start:dev

# Producción
npm run build
npm run start:prod

# Linting
npm run lint
```

### Frontend
```bash
# Desarrollo
npm run dev

# Build para producción
npm run build

# Preview del build
npm run preview
```

## Solución de Problemas

### Error de conexión a la base de datos
- Verifica que PostgreSQL esté ejecutándose
- Confirma las credenciales en el archivo `.env`
- Asegúrate de que la base de datos `data_arch_labs` exista

### Error de CORS
- Verifica que `FRONTEND_URL` en el backend apunte a `http://localhost:5173`
- Confirma que `VITE_API_URL` en el frontend apunte a `http://localhost:3001/api`

### Error de autenticación Google
- Verifica las URLs de redirección en Google Cloud Console
- Confirma que `GOOGLE_CLIENT_ID` y `GOOGLE_CLIENT_SECRET` sean correctos