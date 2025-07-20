# Data Arch Labs - Base de Datos con Docker

## 🗄️ Configuración de Base de Datos

### 🚀 Ejecutar Solo la Base de Datos

```bash
# Construir y ejecutar PostgreSQL + pgAdmin
docker-compose up -d

# Ver logs
docker-compose logs -f

# Detener servicios
docker-compose down

# Detener y eliminar datos
docker-compose down -v
```

### 🌐 URLs de Acceso

| Servicio | URL | Credenciales |
|----------|-----|--------------|
| **pgAdmin** | http://localhost:8080 | admin@dataarchlabs.com / admin123 |
| **PostgreSQL** | localhost:5432 | postgres / postgres123 |

### 🔧 Configurar Conexión en pgAdmin

1. **Abre pgAdmin:** http://localhost:8080
2. **Inicia sesión:**
   - **Email:** admin@dataarchlabs.com
   - **Contraseña:** admin123

3. **Agregar Servidor PostgreSQL:**
   - Clic derecho en "Servers" → "Register" → "Server"
   - **General Tab:**
     - **Name:** Data Arch Labs
   - **Connection Tab:**
     - **Host:** postgres
     - **Port:** 5432
     - **Maintenance database:** data_arch_labs
     - **Username:** postgres
     - **Password:** postgres123

### 📊 Verificar Base de Datos

Una vez conectado, puedes ejecutar estas consultas:

```sql
-- Ver todas las tablas
SELECT table_name FROM information_schema.tables 
WHERE table_schema = 'public';

-- Ver usuarios (cuando el backend cree las tablas)
SELECT * FROM users;

-- Ver el administrador
SELECT * FROM users WHERE role = 'admin';
```

### 🔗 Conectar desde tu Backend Local

Actualiza tu archivo `backend_DataArch/.env`:

```env
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=postgres123
DATABASE_NAME=data_arch_labs
```

### 🛠️ Comandos Útiles

```bash
# Ver contenedores en ejecución
docker ps

# Acceder directamente a PostgreSQL
docker exec -it data_arch_postgres psql -U postgres -d data_arch_labs

# Ver logs de PostgreSQL
docker-compose logs postgres

# Ver logs de pgAdmin
docker-compose logs pgadmin

# Reiniciar solo PostgreSQL
docker-compose restart postgres

# Backup de la base de datos
docker exec data_arch_postgres pg_dump -U postgres data_arch_labs > backup.sql

# Restaurar backup
docker exec -i data_arch_postgres psql -U postgres data_arch_labs < backup.sql
```

### 🔄 Desarrollo

- **Persistencia:** Los datos se guardan en volúmenes Docker
- **Acceso externo:** Puedes conectarte desde cualquier cliente SQL
- **Hot reload:** Compatible con tu backend local

### 🛠️ Solución de Problemas

1. **Puerto 5432 ocupado:**
   ```bash
   # Cambiar puerto en docker-compose.yml
   ports:
     - "5433:5432"  # Usar puerto 5433 en lugar de 5432
   ```

2. **Puerto 8080 ocupado:**
   ```bash
   # Cambiar puerto de pgAdmin
   ports:
     - "8081:80"  # Usar puerto 8081
   ```

3. **Problemas de permisos:**
   ```bash
   sudo docker-compose up -d
   ```

4. **Limpiar todo:**
   ```bash
   docker-compose down -v
   docker system prune -a
   ```

### 📝 Notas

- PostgreSQL estará disponible en `localhost:5432`
- pgAdmin estará disponible en `http://localhost:8080`
- Los datos persisten entre reinicios
- Compatible con tu backend ejecutándose localmente