# Data Arch Labs - Configuración con Docker

## 🐳 Ejecutar con Docker

### Requisitos Previos
- Docker
- Docker Compose

### 🚀 Comandos para Ejecutar

1. **Construir y ejecutar todos los servicios:**
   ```bash
   docker-compose up --build
   ```

2. **Ejecutar en segundo plano:**
   ```bash
   docker-compose up -d --build
   ```

3. **Ver logs:**
   ```bash
   docker-compose logs -f
   ```

4. **Detener servicios:**
   ```bash
   docker-compose down
   ```

5. **Detener y eliminar volúmenes:**
   ```bash
   docker-compose down -v
   ```

### 🌐 URLs de Acceso

| Servicio | URL | Descripción |
|----------|-----|-------------|
| **Frontend** | http://localhost:3000 | Aplicación React |
| **Backend API** | http://localhost:3001 | API NestJS |
| **pgAdmin** | http://localhost:8080 | Administrador de Base de Datos |
| **PostgreSQL** | localhost:5432 | Base de datos (acceso directo) |

### 🗄️ Acceso a pgAdmin

1. **URL:** http://localhost:8080
2. **Credenciales:**
   - **Email:** admin@dataarchlabs.com
   - **Contraseña:** admin123

3. **Configurar conexión a PostgreSQL:**
   - **Host:** postgres
   - **Puerto:** 5432
   - **Usuario:** postgres
   - **Contraseña:** postgres123
   - **Base de datos:** data_arch_labs

### 📊 Verificar Base de Datos

Una vez en pgAdmin, puedes ejecutar estas consultas:

```sql
-- Ver todos los usuarios
SELECT * FROM users;

-- Ver el administrador
SELECT * FROM users WHERE role = 'admin';

-- Ver todas las tablas
SELECT table_name FROM information_schema.tables 
WHERE table_schema = 'public';
```

### 🔧 Comandos Útiles

```bash
# Ver contenedores en ejecución
docker ps

# Acceder al contenedor del backend
docker exec -it data_arch_backend sh

# Acceder al contenedor de PostgreSQL
docker exec -it data_arch_postgres psql -U postgres -d data_arch_labs

# Ver logs específicos
docker-compose logs backend
docker-compose logs frontend
docker-compose logs postgres

# Reconstruir solo un servicio
docker-compose up --build backend

# Reiniciar un servicio
docker-compose restart backend
```

### 🔄 Desarrollo

Para desarrollo, los volúmenes están configurados para:
- **Hot reload** en el frontend
- **Nodemon** en el backend
- **Persistencia** de datos en PostgreSQL

### 🛠️ Solución de Problemas

1. **Error de puerto ocupado:**
   ```bash
   # Cambiar puertos en docker-compose.yml
   ports:
     - "3001:3001"  # cambiar el primer número
   ```

2. **Problemas de permisos:**
   ```bash
   sudo docker-compose up --build
   ```

3. **Limpiar todo y empezar de nuevo:**
   ```bash
   docker-compose down -v
   docker system prune -a
   docker-compose up --build
   ```

4. **Ver logs detallados:**
   ```bash
   docker-compose logs -f --tail=100
   ```

### 📝 Notas Importantes

- Los datos de PostgreSQL se persisten en un volumen Docker
- pgAdmin también tiene persistencia de configuración
- El backend espera a que PostgreSQL esté listo antes de iniciar
- Los archivos `.env.docker` contienen las variables específicas para Docker