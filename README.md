
# Desplegar MinIO Localmente y Configurar Talend

A continuación se detallan los pasos para levantar una instancia local de MinIO utilizando Docker, configurar usuarios y acceder al panel de administración, así como los pasos para integrar MinIO con Talend.

## Paso 1: Levantar una Instancia de MinIO

MinIO es una solución de almacenamiento compatible con la API de S3. Para levantarlo localmente usando Docker, ejecuta el siguiente comando en tu terminal. Esto iniciará un contenedor MinIO y expondrá el servicio en los puertos 9000 y 9090.

```bash
docker run -d --name minio-server \
  -p 9000:9000 -p 9090:9090 \
  -e "MINIO_ROOT_USER=admin" \
  -e "MINIO_ROOT_PASSWORD=admin123" \
  -v C:\path\to\data:/data \
  -v C:\path\to\config:/root/.minio \
  minio/minio server /data --console-address ":9090"
```

**Explicación del comando:**

- `-d`: Ejecuta el contenedor en segundo plano.
- `--name minio-server`: Asigna un nombre al contenedor.
- `-p 9000:9000`: Expone el puerto 9000 (para la API de S3).
- `-p 9090:9090`: Expone el puerto 9090 (para el panel de administración).
- `-e "MINIO_ROOT_USER=admin"`: Define el usuario root para MinIO.
- `-e "MINIO_ROOT_PASSWORD=admin123"`: Define la contraseña para el usuario root.
- `-v C:\path\to\data:/data`: Mapea el directorio de datos en tu máquina local al contenedor.
- `-v C:\path\to\config:/root/.minio`: Mapea el directorio de configuración en tu máquina local al contenedor.
- `minio/minio server /data --console-address ":9090"`: Inicia MinIO con la ruta `/data` para el almacenamiento y el panel de administración en `localhost:9090`.

## Paso 2: Acceder al Panel de Administración de MinIO

1. Abre tu navegador y navega a `http://localhost:9090`.
2. Ingresa con las credenciales que definiste en el comando de Docker:
   - **Usuario**: `admin`
   - **Contraseña**: `admin123`

## Paso 3: Crear un Usuario en MinIO

1. Una vez dentro del panel de administración, haz clic en **Administrator** en la barra lateral.
2. Dirígete a la sección **Users**.
3. Haz clic en el botón **Create User**.
4. Define un **Access Key** y un **Secret Key** para el nuevo usuario.
5. Guarda las claves para usarlas más tarde en Talend.

## Paso 4: Configuración en Talend

Ahora que tienes MinIO funcionando y un usuario creado, puedes configurar Talend para interactuar con MinIO.
