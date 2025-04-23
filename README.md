# Byron Cholca  
**Carrera:** Desarrollo de Software  
**Curso:** TRANSFORMACIÓN DIGITAL APROVECHANDO LAS TECNOLOGÍAS DE LA NUBE CON AWS  
**Tarea:** Implementación de un entorno de desarrollo con Docker Compose  

---

## Descripción del Proyecto

Este proyecto consiste en la dockerización de un entorno de desarrollo compuesto por una API Web desarrollada en .NET Core 8 y una base de datos SQL Server. Se implementa un CRUD básico para gestionar datos de una tabla **CLIENTE**, y se expone mediante una API REST, que puede ser probada con herramientas como Postman.

Docker Compose se utiliza para levantar simultáneamente ambos servicios (API y base de datos), facilitando la configuración y el entorno de desarrollo.

---
## Objetivo

Configurar un entorno de desarrollo utilizando Docker Compose que permita levantar una aplicación Web API 
desarrollada en .NET Core 8 y una base de datos SQL Server. Se implementa un CRUD sobre una tabla `Cliente`.

---

## Contenido del proyecto

- `Dockerfile`: Define la construcción de la imagen del proyecto API en .NET Core.
- `docker-compose.yml`: Levanta los servicios del API y la base de datos SQL Server.
- CRUD a la entidad `CLIENTE` expuesto vía Web API.
- Persistencia de datos mediante volúmenes en SQL Server.

---

## Guía de Implementación

### 1. Construir y levantar los contenedores 🚀

Para construir las imágenes y levantar los servicios definidos en el archivo `docker-compose.yml`, ejecuta el siguiente comando en la raíz del proyecto:

```bash
docker-compose -f .\docker-compose-SqlServer.yml up -d
```
### 2. Verificar el nombre del contenedor SQL Server

```bash
docker ps
```
---

### 3. Conexión a la base de datos desde el proyecto .NET Core

En el proyecto Web API configuro `appsettings.json` con el nombre del contenedor del SqlServer: database-sql

```json
"ConnectionStrings": {
  "Connection": "Server=database-sql,1433;Database=ECommerceData;User Id=sa;Password=adminAppDist2024#;TrustServerCertificate=True"
}
```

---

### 4. Explicación de las APIs del CRUD

- `POST /api/cliente/obtenerClientes`
- `POST /api/cliente/insertarCliente`
- `GET /api/cliente/{id}`
- `PUT /api/cliente/{id}`
- `DELETE /api/cliente/{id}`

---


### 5. Dockerización del proyecto API .NET Core

El proyecto contiene un `Dockerfile` para construir la imagen de la API.

---

### 6. Crear el archivo `docker-compose-apisweb.yml`

Este archivo define el servicio para levantar la API conectada a SQL Server.

---

### 7. Crear la imagen del contenedor de la API

```bash
docker-compose -f docker-compose-apisweb.yml build
```

---

### 8. Levantar el contenedor de la API

```bash
docker-compose -f docker-compose-apisweb.yml up -d
```

---

### 9. Verificación en Docker Desktop

Abrir Docker Desktop y verificar que los contenedores estén en ejecución:
- `database-sqlserver`
- `proyectoEcommerce-BCH`

---

### 10. Probar las APIs desde Postman

Probar los siguientes endpoints:

- `POST http://localhost:8081/api/cliente/obtenerClientes`
- `POST http://localhost:8081/api/cliente/insertarCliente`
- `GET  http://localhost:8081/api/cliente/{id}`
- `PUT  http://localhost:8081/api/cliente/{id}`
- `DELETE http://localhost:8081/api/cliente/{id}`

---

## Comandos útiles

```bash
# Ver contenedores activos
docker ps

# Detener y eliminar contenedores
docker-compose -f archivo.yml down
```
