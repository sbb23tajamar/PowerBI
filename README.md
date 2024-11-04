
# Levantar un flujo analítico sencillo con estos servicios: Hadoop + YARN + Hive + PowerBI.

### Paso 1: Clonar y Configurar el Repositorio
Primero, clona el repositorio que contiene un contenedor de Hive:

```bash 
git clone big-data-europe/docker-hive 
cd docker-hive 
docker-compose up -d
```
Este paso puede llevar un tiempo, ya que Docker descargará todas las imágenes y configurará Hive. Para verificar que los contenedores se están ejecutando, usa:
```bash 
docker container ps
```

### Paso 2: Cargar y Consultar Datos en Hive

Accede al contenedor de nombre hive-server:
```bash 
docker-compose exec hive-server bash
```
Esto abre una terminal en el contenedor de Hive, desde donde puedes ejecutar comandos de Hive usando Beeline, el cliente JDBC de Hive.

Inicia beeline:
```bash 
# /opt/hive/bin/beeline -u jdbc:hive2://localhost:10000
```

### Paso 3: Crear la base de datos

```bash 
> CREATE TABLE pokes (foo INT, bar STRING);
> LOAD DATA LOCAL INPATH '/opt/hive/examples/files/kv1.txt' OVERWRITE INTO TABLE pokes;
```
### Paso 4: Instalación PowerBI
Descarga Power BI Desktop desde la tienda de Microsoft. Instala la aplicación y accede a ella.

### Paso 5: Configuración de Power BI

Acepta todas las configuraciones por defecto al iniciar la aplicación. En la página principal, ve a la sección de "Obtener datos" y selecciona "Otros orígenes". Elige "Hive LLAP" y haz clic en "Conectar".

**Hive LLAP**
- **Servidor:** localhost:10000 
- **Base de datos:** default 
- **Protocolo de transporte:** Thrift estándar 
- **Modo de conectividad:** Importar

### Conectar el servidor

- **Nombre de usuario:** root 
- **Contraseña:** root

Haz clic en "Aceptar" para confirmar.

### Pasos finales

Selecciona la base de datos que quieres cargar (en este caso, "pokes") y haz clic en "Cargar". Ya tienes Hive conectado con Power BI.

### Caso de prueba 
En la sección de datos a la derecha, despliega la tabla "pokes" y arrastra los datos a un gráfico para visualizarlos. 

¡Y listo! Ya puedes usar Power BI con tus datos de Hive. 😎
