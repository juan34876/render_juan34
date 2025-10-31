Paso 1: Crear la Base de Datos PostgreSQL

Accede a tu panel principal en Render Dashboard
.

Haz clic en “New +” y selecciona “PostgreSQL”.

Llena los datos de configuración de la siguiente manera:

Campo	Valor
Name	odoo-db
Database	odoo
User	odoo_user
Plan	Free
Region	Frankfurt (o la misma zona donde crearás el servicio web)

Guarda y espera a que Render finalice la creación del servicio de base de datos.

Paso 2: Crear el Servicio Web de Odoo

En el mismo panel de Render, pulsa “New +” → “Web Service”.

Conecta tu cuenta de GitHub y elige el repositorio TheOneHerrera/OdooTests.

Configura los siguientes parámetros:

Configuración	Valor
Name	odoo-app
Environment	Docker
Region	Igual que la base de datos
Plan	Free

Render identificará automáticamente el archivo Dockerfile y comenzará a construir la imagen.
Este proceso inicial puede tardar varios minutos.

⚙️ Paso 3: Definir las Variables de Entorno

En tu servicio web odoo-app, sigue estos pasos:

Dirígete a la pestaña Environment.

Agrega las siguientes variables con sus respectivos valores:

# Configuración de la base de datos
DB_HOST=tu-host-postgres.render.com
DB_PORT=5432
DB_NAME=odoo
DB_USER=odoo_user
DB_PASSWORD=tu_password_postgres

# Configuración de Odoo
ADMIN_PASSWORD=Admin123!  # cámbiala por una contraseña segura
PGDATABASE=odoo
PGUSER=odoo_user
PGPASSWORD=tu_password_postgres
PGHOST=tu-host-postgres.render.com
PGPORT=5432


💡 Sugerencia: aprovecha la función de variables secretas en Render para ocultar tus credenciales sensibles.

🔑 Paso 4: Obtener los Datos de Conexión de PostgreSQL

Abre el servicio PostgreSQL (odoo-db) que creaste.

En la sección Connections, copia las credenciales de conexión proporcionadas.

Comprueba que el nombre del host termine correctamente en .render.com.

Ejemplo de conexión completa:

postgresql://odoo_user:password@dpg-d3ts1mogjchc73fgin9g-a.oregon-postgres.render.com:5432/odoo


Por lo tanto, tus variables quedarían así:

DB_HOST=dpg-d3ts1mogjchc73fgin9g-a.oregon-postgres.render.com
DB_PORT=5432
DB_NAME=odoo
DB_USER=odoo_user
DB_PASSWORD=password

🔍 Paso 5: Verificar el Despliegue

Ingresa al servicio odoo-app dentro de Render.

En la pestaña Logs, revisa el progreso del despliegue y los mensajes del contenedor.

Espera entre 5 y 10 minutos hasta que Render complete la construcción y el arranque.

Obtendrás una URL pública (por ejemplo: https://odoo-app.onrender.com).

Al acceder a esa dirección:

Verás la pantalla de bienvenida de Odoo.

Desde ahí podrás crear tu base de datos inicial e iniciar sesión en tu instancia.

✅ Comprobación Final

Para confirmar que todo funciona correctamente:

Asegúrate de que las variables de entorno estén correctamente escritas.

Verifica que la base de datos y el servicio web estén en la misma región.

Confirma que el servicio de PostgreSQL esté activo (Render pausa servicios gratuitos si no se usan).
