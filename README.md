# Docker: Investigación

## 1. ¿Qué es Docker?

Docker es una plataforma de código abierto que permite desarrollar, enviar y ejecutar aplicaciones dentro de contenedores. Estos contenedores son entornos aislados que contienen todo lo necesario para que una aplicación funcione: código, bibliotecas, dependencias y configuraciones.

## 2. ¿Para qué sirve Docker?

Docker se utiliza para:

- **Portabilidad**: Los contenedores pueden ejecutarse en cualquier sistema que tenga Docker instalado, independientemente del entorno.
- **Eficiencia**: Los contenedores son más ligeros y rápidos que las máquinas virtuales tradicionales.
- **Escalabilidad**: Facilita el despliegue y escalado de aplicaciones en entornos de producción.

## 3. Instalación de Docker en Ubuntu

### Requisitos previos
Ubuntu 22.04 o superior. Se necesitan permisos de administrador (sudo).

### Pasos para instalar Docker:

```bash
# Actualizar paquetes del sistema
sudo apt update
sudo apt upgrade

# Instalar paquetes necesarios
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Agregar la clave GPG de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Agregar el repositorio de Docker
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

# Actualizar el índice de paquetes
sudo apt update

# Instalar Docker
sudo apt install docker-ce

# Verificar que Docker esté activo
sudo systemctl status docker
```

## 4. Comandos más utilizados: 

docker run -> Ejecuta un contenedor desde una imagen  
docker ps -> Lista los contenedores en ejecución  
docker ps -a -> Lista todos los contenedores (activos/inactivos)  
docker images -> Muestra las imágenes descargadas  
docker pull imagen -> Descarga una imagen desde Docker Hub  
docker build -> Construye una imagen a partir de un Dockerfile  
docker exec -> Ejecuta un comando en un contenedor activo  
docker stop id -> Detiene un contenedor  
docker rm id -> Elimina un contenedor  
docker rmi imagen -> Elimina una imagen  

## Instalación y Ejecución de un Contenedor Interesante

### Contenedor Seleccionado: Apache HTTP Server (`httpd`)

#### ¿Porqué Apache?

Antes de elegir el contenedor, revisé varias opciones en Docker Hub. Me decidí por Apache (httpd) principalmente porque ya había realizado un trabajo anterior sobre este servidor web, lo cual me facilita entender mejor su funcionamiento en un entorno diferente como Docker. Además, la mayoría de los servidores web tradicionales, especialmente en hostings compartidos, utilizan Apache, por lo que consideré útil profundizar en su instalación y uso dentro de un contenedor.

#### Pasos seguidos

1. **Buscar la imagen oficial de Apache en Docker Hub**  
   Ingresé a https://hub.docker.com/_/httpd y verifiqué que `httpd` corresponde a la imagen oficial del servidor Apache mantenida por Docker.

2. **Descargar la imagen con Docker**  
   Desde la terminal, ejecuté el siguiente comando para descargar la imagen:

   ```bash
   docker pull httpd
   ```
3. **Ejecutar el contenedor Apache**  
   Una vez descargada la imagen, ejecutar el contenedor con el siguiente comando:

   ```bash
   docker run --name servidor-apache -p 8080:80 -d httpd
   ```

  Este comando hace lo siguiente:

  --name servidor-apache: asigna un nombre identificable al contenedor.
  
  -p 8080:80: expone el puerto 80 del contenedor (donde escucha Apache) al puerto 8080 del host local.
  
  -d: ejecuta el contenedor en segundo plano (modo "detached").
  
  httpd: indica la imagen que se usará.

4. **Verificar que el contenedor funciona correctamente**  
   Abrir el navegador y acceder a: http://localhost:8080


5. **Detener el contenedor (cuando no se necesita)**  
Para detener la ejecución del contenedor:

```bash
docker stop servidor-apache
```
## Contenedor desde Cero

### Pasos para crearlo

#### 1. Crear el directorio del proyecto

  ```bash
mkdir mi-app-node
cd mi-app-node
```
#### 2. Crear un archivo principal app.js con el siguiente contenido:

```bash
const http = require('http');

const hostname = '0.0.0.0';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('¡Hola desde mi primer contenedor Docker!');
});

server.listen(port, hostname, () => {
  console.log(`Servidor corriendo en http://${hostname}:${port}/`);
});
```
#### 3. Crear un archivo package.json

```bash {
  "name": "mi-app-node",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {}
}
```

#### 4. Crear el Dockerfile

El **Dockerfile** es un archivo de texto que contiene instrucciones para construir una imagen Docker personalizada. Cada línea define una acción para configurar el entorno y preparar la aplicación.

Este es el contenido del Dockerfile que puedes probar:

```Dockerfile
FROM node:14

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["node", "app.js"]
```

#### 5. Construir la imagen Docker

Para crear la imagen a partir del Dockerfile, ejecute:

```bash
docker build -t mi-app-node .
```

Este proceso toma el Dockerfile, descarga la imagen base (node:14), copia los archivos, instala dependencias y genera una imagen lista para usar.

#### 6. Ejecutar contenedor 

Para ejecutar la imagen recién creada y levantar la aplicación dentro de un contenedor, use:

```bash
docker run -p 3000:3000 mi-app-node
```

#### 7. Verificación

Finalmente, abrí un navegador web y visitar: http://localhost:3000


