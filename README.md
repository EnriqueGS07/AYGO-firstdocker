# Aygo - Taller 1

## Descripcion

Esta es una plicacion Spring Boot que implementa un servicio REST con un endpoint de /greeting, el cual rsponde con un simple "Hello World", para este ejercicio se contenerizo la aplicacion en docker, se subio a dockerhub y se ejecuto desde una instancia EC2

## Arquitectura - AWS EC2
<img width="836" height="560" alt="image" src="https://github.com/user-attachments/assets/6d36d519-1cc0-4485-bb53-3cac1ad96ed4" />


## Tecnologias

- Java 17
- Maven 3.9+
- Docker

## Endpoint

### Greeting

Retorna un saludo personalizado.

**URL:** `http://localhost:8080/greeting`

**Metodo:** GET

**Ejemplo:**

```bash
curl http://localhost:8080/greeting
curl "http://localhost:8080/greeting?name=Juan"
```

**Respuesta:**

```
Hello, World!
```

## Build y Ejecucion Local

### Compilar el proyecto

```bash
mvn clean compile
```

### Ejecutar la aplicacion

```bash
mvn spring-boot:run
```

La aplicacion estara disponible en `http://localhost:8080`

## Docker

### Build de la imagen

```bash
docker build --tag dockersparkprimer .
```

### Ejecutar contenedor

```bash
docker run -d -p 8080:8080 --name aygo-container aygo-web
```

**Ver contenedor:**

```bash
docker ps
```

### Docker Hub

La imagen de la aplicacion esta publicada en Docker Hub:

**Repositorio:** `kikegonzalez202/firstdockercontainer`

**Imagen:** `kikegonzalez202/firstdockercontainer:latest`

**Descargar desde Docker Hub:**

```bash
docker pull kikegonzalez202/firstdockercontainer:latest
```

**Ejecutar imagen de Docker Hub:**

```bash
docker run -d -p 8080:8080 --name aygo-container kikegonzalez202/firstdockercontainer:latest
```

## Docker Compose

El proyecto incluye un archivo docker-compose.yml para orquestar contenedores.

### Servicios

- **web:** Aplicacion Spring Boot

### Ejecutar con Docker Compose

**Iniciar servicios:**

```bash
docker-compose up -d
```

**Ver servicios:**

```bash
docker-compose ps
```

**Detener servicios:**

```bash
docker-compose down
```

## Despliegue en AWS EC2

### Prerequisitos

- Instancia EC2 corriendo
- Docker instalado en la instancia
- Security Group configurado para permitir trafico en el puerto correspondiente

### Paso 1: Conectarse a la instancia EC2

- Crear la instancia EC2

### Paso 2: Instalar Docker

```bash
sudo yum update -y
sudo yum install docker -y
sudo service docker start
sudo usermod -a -G docker ec2-user
```

### Paso 3: Descargar y ejecutar la imagen

```bash
docker run -d -p 42000:8080 --name firstdockerimageaws kikegonzalez202/firstdockercontainer:latest
```

### Paso 4: Verificar que el contenedor este corriendo

```bash
docker ps
```

### Paso 5: Configurar Security Group

1. Ir a la consola de AWS EC2
2. Seleccionar la instancia
3. Ir a Security Groups
4. Agregar regla de entrada:
   - Tipo: Custom TCP
   - Puerto: 42000
   - Origen: 0.0.0.0/0

### Paso 6: Acceder a la aplicacion

Desde el navegador:

```
http://{IP_EC2}:42000/greeting
```

Desde el EC2 mismo:

```bash
curl http://localhost:42000/greeting
```

### Video de funcionmiento


