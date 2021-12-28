
### 1: DESARROLLAR, DISTRIBUIR Y EJECUTAR CON DOCKER

#### Problems when building:
- Development dependencies (packages)
- Runtime versions
- Equivalence of development environments (code sharing)
- Equivalence of production environments(go to production)
- Versions / compatibility(integration of other services e.g.: databases)
#### Problems when distributing:
- Different build generations
- Access to production servers
- Native vs. distributed execution
- Serverless
#### Problems when executing:
- Application dependencies
- Operating System Compatibility
- Availability of external services
- Hardware Resources
#### Docker allows: Build, distribute and run your code anywhere without worrying.

- Version de docker instalada
```console
docker --version
```
- Información de docker
```console
docker info
```

### COMANDOS
- Ejecutar un contenedor a partir de una imagen
```console
docker run <image>
docker run --name <container-name> <image>  <-- (--name) para especificar un nombre al contenedor
docker run -it <image>  <-- (-it) para ejecutar en modo interactivo
docker run -itd <image>  <-- (-d) para ejecutar en modo detach: no se vincula la I/O estandar con la CLI, sino vinculada en background
```
- Ver los contenedores que están corriendo
```console
docker ps
docker ps -a  <-- (-a) para tambien listar los contenedores detenidos
```
- Detener un contenedor
```console
docker stop <container-id-or-name>
```
- Eliminar contenedores
```console
docker rm <container-id-or-name>  <-- elimina contenedores que estan detenidos
docker rm -f <container-id-or-name>  <-- forza la eliminacion de contenedores que estan corriendo
docker container prune  <-- elimina todos los contenedores
docker run --rm -p <image>  <-- eliminar un contenedor una vez que se detenga
```
- Inspeccionar un contenedor
```console
docker inspect <container-id-or-name>
```
- Renombrar un contenedor
```console
docker rename <initial-container-name> <target-container-name>
```
No se permite tener dos contenedores con el mismo nombre

### CICLO DE VIDA DE UN CONTENEDOR
Un contenedor se mantiene activo si el proceso principal (command) esté corriendo: por ejemplo ejecutar el bash de ubuntu en modo interactivo, si lo detenemos con "exit", se termina el bash y por ende el contenedor se detiene.
- Correr un contenedor sobrescribiendo el comando principal bash para que el contenedor permanezca levantado y en modo detach
```console
docker run --name <container-name> -d <image> tail -f <main-command>
docker run --name always-up -d ubuntu tail -f /dev/null  <-- aqui un contenedor de ubuntu se crea y se ejecuta pero se sobreescribe el proceso principal, el contenedor se mantiene levantado
```
- Ejecutar un comando en un contenedor existente y que está corriendo
```console
docker exec -it <container-[name,id]> <command>
docker exec -it always-up bash   <— aquí bash no es el proceso principal, asi que se lo puede terminar pero el contenedor ahorab ya no va a terminar
```
- Inspeccionar el process id principal del contenedor
```console
docker inspect --format '{{.State.Pid}}' <container-name>
```
Cada contenedor tiene su propio Stack de networking (su propia interfaz de red virtual)
- Exponer un puerto del contenedor (-p)
```console
docker run -d --name <container-name> -p <exposed-port>:<container-port> <image>
docker run -d --name proxy -p 8080:80 proxy  <-- aqui se expone el puerto 80 del contenedor en el puerto 8080 del host mientras se ejecuta el contenedor en modo detach
```
### VER LOS LOGS DE UN CONTENEDOR
```console
docker logs <container-id-or-name>
docker logs -f <container-id-or-name>   <-- (-f) Enchufarse a los logs
docker logs --tail <number> -f <container-id-or-name>   <-- (--tail) ver solo las ultimas <number> entradas de log
```
### BIND MOUNTS
- Crear un bind mount para una conexion bidireccional de archivos
```console
docker run -d --name <container-name> -v <host-folder-or-file>:<docker-folder-or-file> <image>
docker run -d --name db -v /Users/jeffersonpazmino/dockerdata:/data/db mongo
```
### IMAGENES
- Ver imágenes en el entorno local
```console
docker image ls
```
- Traer una imagen de docker hub (hub.docker.com)
```console
docker pull <image>
docker pull <image>:<tag>  <-- un <tag> es la version de la imagen, si no la especificamos de asume el tag latest
```
### CREAR IMAGENES
- 1. Crear un archivo llamado Dockerfile que sirve para crear imagenes con nuevas capas
#### Dockerfile
```
FROM alpine:3.14
RUN touch ~/new_dir
```
- 2. Crear la imagen con el contexto . (Donde se encuentra el Dockerfile)
```console
docker build -t alpine:custom .
```
- 3. Crear un contenedor con la imagen nueva
```console
docker run -it alpine:custom
```
- 4. Ver las capas de una imagen
```console
docker history alpine:custom
```
- 5. Con el comando "dive alpine:custom" se puede ver mejor el history https://github.com/wagoodman/dive

### PUBLICAR IMAGENES
- 1. Retaggear la imagen con el nombre del repositorio para subirla
```console
docker tag alpine:custom <repository-username>:custom
```
- 2. Publicar la imagen
```console
docker login
docker push <repository-username>:custom
```
Cuando se corre un contenedor, docker ofrece una nueva capa mutable de este. Con docker commit se puede crear una capa inmutable a partir de los cambios hechos en la capa mutable del contenedor creado.

### 19: PROYECTO NODE. IMAGENES Y REDES DE DOCKER
- proyecto: git clone https://github.com/platzi/docker
#### Dockerfile
```
# imagen node:12 como capa base
FROM node:12

# copiar los archivos del contexto de build a /usr/lib 
COPY [“.”, “/usr/lib”]

# comando cd /usr/lib
WORKDIR /usr/lib

# instalar dependencias de node
RUN npm Install

# puerto para poder exponer el contenedor
EXPOSE 3000

# definir el comando por defecto a ejecutar cuando se corra el contenedor
CMD [“node”, “index.js”]
```
# construir la imagen con el contexto (.) y (-t) para taggear la imagen
```console
  > docker build -t platziapp .
```
### 20: LAYER CACHE
- Docker aprovecha las capas construidas si no se producen cambios en estas. En el Dockerfile anterior, si se quiere cambiar la version de node a v14, esto provocará que todas las demás capas seran invalidadas y tendran que reconstruirse nuevamente al ejecutar docker build.
- Desde la instrucción “COPY [“.”, “/usr/lib”]” se reconstruirán todas las capas siguientes cada que el código de la aplicación cambie. La capa “RUN npm Install” que construye los modulos de node no es deseable que se reconstruya cada vez que pase esto. Para ahorrarnos ese paso, solo copiamos los archivos necesarios y luego instalamos los modulos de node, finalmente copiamos los demás archivos que incluyen "index.js" el cual si sufre cambios y reconstruimos, docker solo invalidará las capas que parten de ese punto
#### Dockerfile v2
```
FROM node:12

# solo archivos necesarios para el npm install

COPY ["package.json","package-lock.json", "/usr/src/"]

WORKDIR /usr/src

RUN npm install

# copiar el resto de los archivos. Docker es inteligente y sabe que como no hay diferencia entre los archivos anteriormente copiados y los que se encuentran en el contexto de build, ya no los vuelve a copiar.

COPY [".", "/usr/src/"]

EXPOSE 3000

CMD ["node", "index.js"]
```

- Si no se desea buildear cada vez que se cambia el código podemos usar volúmenes.

- Con nodemon monitoreamos cambios en los archivos. Esta dependencia ya está insertada en el package.json, así que basta con hacer lo siguiente:

1. Cambiar el comando “CMD ["node", "index.js"]” a “CMD ["npx","nodemon", "index.js"]” y buildear nuevamente.

2. Ejecutar el “docker run”, esta vez usando bind mounts
```console
docker run --rm -p 3000:3000 -v `pwd`/index.js:/usr/src/index.js platziapp
```
- Ahora si se hacen cambios en "index.js" estos se reflejarán en http://localhost:3000/

### 21: DOCKER NETWORKING

En "index.js" la forma de conectarse a mongo es mediante la instrucción:
```python
const mongoUrl = process.env.MONGO_URL || 'mongodb://localhost:27017/test';
```
Como se aprecia, si no hay una variable de entorno, usa localhost. Para conectar nuestro contenedor python con el contenedor mongo se usarán las networks

- Listar las redes existentes
```console
docker network ls
```
1. Crear una network  (--attachable) para que otros contenedores se puedan conectar a esta red
```console
docker network create --attachable <network-name>
docker network create --attachable platzinet  <-- aqui estamos creando una red llamada platzinet
```
2. Crear un contenedor y conectarse a la network platzinet
```console
docker run -d --name db mongo

docker network connect <network> <container-id-or-name>
docker network connect platzinet db
```
# Inspeccionar una red
```console
docker network inspect <network>
```
3. Ejecutar el contenedor a partir de platziapp, le especificamos una variable de entorno (--env) que será usada en el "index.js" para conectarse a la base de datos
```console
docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test platziapp
```
En la variable de entorno se especifica el nombre del contenedor "db". En docker cuando dos contenedores están en la misma red, no es necesario indicar el host ya que pueden encontrarse por sus nombres de contenedor

4. La aplicación aún no se conectará a mongo porque el contenedor app no está en la red platzinet. procedemos a agregarlo
```console
docker network connect platzinet app
```
Ahora la aplicación correrá correctamente en http://localhost:3000/ y ya indica la conexion a mongo.

### 23: DOCKER COMPOSE
Docker compose permite describir de forma declarativa la arquitectura de servicios que una aplicación necesita.
#### docker-compose
```
version: "3.8"
services:
  app:
    image: platziapp
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
  db:
    image: mongo
```
- Ejecutar el docker-compose.yml
```console
docker-compose up
docker-compose up -d  <-- en modo detach
```
### 23: DOCKER COMPOSE. SUBCOMANDOS

- Ver los logs de todos los servicios
```console
docker-compose logs
```
- Ver solo los logs de un servicio o varios
```console
docker-compose logs <service1> <service2> …
```
- Hacer un follow de los logs de un servicio
```console
docker-compose logs -f <service>
```
- Correr un comando en un contenedor
```console
docker-compose exec <service> <command>
```
- Limpiar todo el estado de nuestro docker-compose destruyendo todo lo que tenemos. Elimina contenedores, servicios y redes
```console
docker-compose down
````
### 24: DOCKER COMPOSE
para no usar una imagen ya construida e inmutable, podemos hacer el build desde el mismo docker-compose.yml
#### docker-compose v2
```
version: "3.8"
services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
  db:
    image: mongo
```
Creamos un volumen para el servicio app para poder hacer cambios y que en el contenedor se reflejen

#### docker-compose v3
```
version: "3.8"
services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src
      - /usr/src/node_modules
  db:
    image: mongo
```
- Con la primera declaración en volumes decimos que haga un espejo entre la carpeta actual del host y la carpeta /usr/src del contenedor, además en la segunda linea decimos que se ignore espejar los módulos de node porque sino estos van a desaparecer ya que en el host no existen, solo existen en el contenedor.

- Pero falta monitorear los cambios, en el último dockerfile si usamos el comando para monitorear. Pero si se desea hacer desde el docker-compose.yml, se escribe la declaración de node:
#### docker-compose v4
```
version: "3.8"
services:
  app:
    build: .
    environment:
      MONGO_URL: "mongodb://db:27017/test"
    depends_on:
      - db
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src
      - /usr/src/node_modules
    command: npx nodemon index.js
  db:
    image: mongo
```
### 25: Docker compose: compose en equipo   ::compose override::

- El compose override es un compose file que sirve para personalizar o hacer pequeños cambios propios para nuestro ambiente sobre el compose file original si necesidad de alterar el archivo original.

# para crear el archivo
```console
touch docker-compose.override.yml
```

# en este archivo solo se especifican las cosas que se desean sobrescribir o aumentar


Ver escalabilidad final del video…???????????


### 26: Administrando ambiente de docker

en este archivo solo se especifican las cosas que se desean sobrescribir o aumentar


- mostrar todos los ids de todos los contenedores
```console
> docker ps -aq
```
- eliminar todos los contenedores
```console
docker rm -f $(docker ps -aq)
```
- eliminar todos los volumenes que no se están usando
```console
docker volume prune
```
- eliminar todas las networks que no se están usando
```console
docker network prune
```
- borrar todo lo que no esta siendo usado: contenedores, imágenes, volumenes, redes
```console
docker system prune
```
-  limitar uso de memoria a un contenedor
```console
docker run -d --name app --memory 1g platziapp
```
- para ver cuanta memoria esta consumiendo una aplicación
```console
docker stats
```
### 27: DETENER CONTENEDORES CORRECTAMENTE > SHELL vs. EXEC


Docker para indicarla a un proceso que tiene que terminar le va a mandar una señal SIGTERM y si el contenedor no response después de un determinado tiempo, docker manda una señal SIGKILL para forzar la salida.

- enviar señal SIGTERM para terminar un contenedor
```console
docker stop <container>
```
- enviar directamente una señal SIGKILL para terminar un contenedor
```console
docker kill <container>
```

### 28: Contenedores ejecutables correctamente: ENTRYPOINT vs. CMD


### 29: El contexto de build


Existe un archivo similar a .gitignore que se llama .dockerignore y lo que pongamos ahí le decimos a docker que no los considere para construir imágenes o espejar.

Se listan una serie de archivos que no suelen copiarse cuando se está en producción.

#### .dockerignore
```
*.log
.dockerignore
.git
.gitignore
build/*
Dockerfile
node_modules
npm-debug.log*
README.md
Docker-compose.yml
```
### 30: Multi-stage build

No es necesario que esté todo el código de un proyecto en la imagen productiva final, especialmente si se están usando lenguajes compilados, no es necesario que el código termine en la imagen, solo los ejecutables o artefactos que serán generados a partir de esos códigos. otro caso típico es el código de testing que también no tiene sentido que esté en la imagen productiva final, porque se esta imagen se genera después de asegurarnos que pasa los test.

Hay una herramienta que sirve ara resolver este problema.


Por lo general se especifica un directorio build done estarán dos archivos

	development.Dockerfile
	production.Dockerfile

Revisar..


<<docker_31>>  Docker-in-Docker

Existe la capacidad de ejecutar docker desde otros contenedores con un concepto que se llama docker-in-docker.


Revisar..












