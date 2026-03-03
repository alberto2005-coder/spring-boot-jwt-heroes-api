# Spring Boot JWT Heroes API 🇪🇸 🇬🇧

[![es](https://img.shields.io/badge/lang-Espa%C3%B1ol-red.svg)](#versi%C3%B3n-en-espa%C3%B1ol)
[![en](https://img.shields.io/badge/lang-English-blue.svg)](#english-version)

---

## Versión en Español

Este es un proyecto de demostración que muestra una API REST construida con Spring Boot, asegurada mediante JSON Web Tokens (JWT) y conectada a una base de datos MySQL. Es ideal como punto de partida para proyectos que requieran autenticación y operaciones CRUD sobre una entidad (Héroes).

### Índice
1. [Tecnologías Utilizadas](#tecnologías-utilizadas)
2. [Requisitos Previos](#requisitos-previos)
3. [Configuración e Instalación](#configuración-e-instalación)
4. [Estructura del Proyecto](#estructura-del-proyecto)
5. [Endpoints de la API](#endpoints-de-la-api)

### Tecnologías Utilizadas
- **Java 17**
- **Spring Boot 3.5.8** (Starters: Web, Data JPA, Security, Actuator, Test)
- **MySQL Connector** (Conexión a la base de datos)
- **JJWT 0.11.5** (Creación y validación de tokens JWT)
- **Maven** (Gestión de dependencias)

### Requisitos Previos
- [Java Development Kit (JDK) 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html) o superior.
- [Maven](https://maven.apache.org/download.cgi) instalado en tu equipo.
- Servidor de base de datos **MySQL** ejecutándose localmente en el puerto `3307` (puedes ajustarlo en la configuración).

### Configuración e Instalación

1. **Clona el repositorio:**
   ```bash
   git clone <URL_DE_TU_REPOSITORIO>
   cd spring-boot-jwt-heroes-api
   ```

2. **Configura la base de datos y JWT:**
   Abre el archivo `src/main/resources/application.properties` y configura las credenciales de tu base de datos y una clave secreta fuerte para JWT:
   ```properties
   spring.datasource.password=TU_PASSWORD_DE_BASE_DE_DATOS
   jwt.secret=TU_CLAVE_SUPER_SECRETA
   ```
   *(Nota: La base de datos `heroes_db` se creará automáticamente gracias a la propiedad `createDatabaseIfNotExist=true` si tu usuario tiene permisos suficientes).*

3. **Ejecuta la aplicación:**
   Puedes iniciar la aplicación usando el wrapper de Maven (incluido) o tu instalación local de Maven:
   ```bash
   mvnw spring-boot:run
   ```
   o
   ```bash
   mvn spring-boot:run
   ```
   La aplicación arrancará por defecto en `http://localhost:8080`.

### Estructura del Proyecto
El proyecto sigue la arquitectura clásica por capas de Spring Boot:
- `Controller`: Maneja las peticiones HTTP y define los endpoints.
- `Service`: Contiene la lógica de negocio.
- `Repository`: Interfaces de Spring Data JPA para el acceso a la base de datos.
- `Model/Entity`: Representación de las tablas de la base de datos como objetos Java.
- `Security`: Configuración de Spring Security, filtros JWT y clases de ayuda para la autenticación.

### Endpoints de la API
*(Asegúrate de documentar aquí las rutas reales de tu proyecto. Ejemplo a continuación:)*

**Públicos:**
- `POST /api/auth/login`: Ruta para autenticarse usando usuario/contraseña. Devuelve un Token JWT de acceso.

**Protegidos (Requieren cabecera `Authorization: Bearer <token>`):**
- `GET /api/heroes`: Obtiene una lista de todos los héroes.
- `GET /api/heroes/{id}`: Obtiene los detalles de un héroe específico.
- `POST /api/heroes`: Crea un nuevo héroe.
- `PUT /api/heroes/{id}`: Actualiza un héroe existente.
- `DELETE /api/heroes/{id}`: Elimina un héroe por su ID.

---

## English Version

This is a demo project showcasing a REST API built with Spring Boot, secured using JSON Web Tokens (JWT), and connected to a MySQL database. It serves as a great starting point for projects requiring authentication and CRUD operations on an entity (Heroes).

### Table of Contents
1. [Technologies Used](#technologies-used)
2. [Prerequisites](#prerequisites)
3. [Setup and Installation](#setup-and-installation)
4. [Project Structure](#project-structure)
5. [API Endpoints](#api-endpoints)

### Technologies Used
- **Java 17**
- **Spring Boot 3.5.8** (Starters: Web, Data JPA, Security, Actuator, Test)
- **MySQL Connector** (Database connection)
- **JJWT 0.11.5** (JWT creation and validation)
- **Maven** (Dependency management)

### Prerequisites
- [Java Development Kit (JDK) 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html) or higher.
- [Maven](https://maven.apache.org/download.cgi) installed on your machine.
- **MySQL** database server running locally on port `3307` (this can be adjusted in the configuration).

### Setup and Installation

1. **Clone the repository:**
   ```bash
   git clone <YOUR_REPOSITORY_URL>
   cd spring-boot-jwt-heroes-api
   ```

2. **Configure the Database and JWT:**
   Open the `src/main/resources/application.properties` file and configure your database credentials and a strong secret key for JWT:
   ```properties
   spring.datasource.password=YOUR_DATABASE_PASSWORD
   jwt.secret=YOUR_SUPER_SECRET_KEY
   ```
   *(Note: The `heroes_db` database will be created automatically thanks to the `createDatabaseIfNotExist=true` property if your user has sufficient permissions).*

3. **Run the application:**
   You can start the application using the included Maven wrapper or your local Maven installation:
   ```bash
   mvnw spring-boot:run
   ```
   or
   ```bash
   mvn spring-boot:run
   ```
   The application will start by default at `http://localhost:8080`.

### Project Structure
The project follows the classic Spring Boot layered architecture:
- `Controller`: Handles HTTP requests and defines endpoints.
- `Service`: Contains business logic.
- `Repository`: Spring Data JPA interfaces for database access.
- `Model/Entity`: Representation of database tables as Java objects.
- `Security`: Spring Security configuration, JWT filters, and authentication helper classes.

### API Endpoints
*(Make sure to document your actual project routes here. Example below:)*

**Public:**
- `POST /api/auth/login`: Route to authenticate using username/password. Returns a JWT access token.

**Protected (Requires `Authorization: Bearer <token>` header):**
- `GET /api/heroes`: Gets a list of all heroes.
- `GET /api/heroes/{id}`: Gets details of a specific hero.
- `POST /api/heroes`: Creates a new hero.
- `PUT /api/heroes/{id}`: Updates an existing hero.
- `DELETE /api/heroes/{id}`: Deletes a hero by their ID.
