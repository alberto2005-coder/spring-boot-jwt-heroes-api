# Spring Boot JWT Heroes API

[![Java](https://img.shields.io/badge/Java-17%2B-ED8B00?logo=openjdk&logoColor=white)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![JWT](https://img.shields.io/badge/Auth-JWT-000000?logo=jsonwebtokens&logoColor=white)](https://jwt.io/)
[![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![MIT](https://img.shields.io/badge/Licencia-MIT-green)](LICENSE)

[Español](#español) · [English](#english)

---

## Español

### Índice

- [Descripción](#descripción)
- [Stack tecnológico](#stack-tecnológico)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Requisitos](#requisitos)
- [Configuración](#configuración)
- [Ejecución](#ejecución)
- [Endpoints](#endpoints)
- [Autenticación](#autenticación)
- [Licencia](#licencia)

### Descripción

API REST de ejemplo construida con **Spring Boot 3** y asegurada con **JWT**. Gestiona un universo de superhéroes con sus equipos, poderes e identidades secretas, y sirve como base para proyectos que necesiten autenticación sin sesiones y operaciones CRUD por capas.

Todas las rutas cuelgan de `/api/v1` y, salvo el registro y el login, requieren la cabecera `Authorization: Bearer <token>`.

### Stack tecnológico

| Capa | Tecnología |
|---|---|
| Lenguaje | Java 17+ |
| Framework | Spring Boot 3.5.8 (Web, Data JPA, Security, Actuator, Test) |
| Tokens | JJWT 0.11.5 |
| Base de datos | MySQL 8 (conector oficial) |
| Build | Maven y Maven Wrapper |
| Contraseñas | BCrypt |

### Estructura del proyecto

```text
spring-boot-jwt-heroes-api/
├── src/main/java/com/example/jwt2/
│   ├── JWT2Application.java
│   ├── config/          # Seguridad, inicialización de roles
│   ├── controllers/     # Auth, héroes, equipos, poderes e identidades
│   ├── dto/             # Objetos de transferencia
│   ├── entities/        # Entidades JPA (Heroe, Equipo, Poder, Role, User…)
│   ├── filter/          # Filtro JWT por petición
│   ├── repositories/    # Spring Data JPA
│   ├── security/        # UserDetails y utilidades
│   ├── service/         # Lógica de negocio
│   └── util/            # Generación y validación del token
├── src/main/resources/application.properties
├── mvnw · mvnw.cmd
├── LICENSE
└── README.md
```

### Requisitos

- **JDK 17** o superior.
- **MySQL 8** escuchando en el puerto **3307** (ajustable).
- Maven no es obligatorio: el wrapper viene incluido.

### Configuración

Edita `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3307/heroes_db?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true
spring.datasource.username=root
spring.datasource.password=TU_CONTRASEÑA

jwt.secret=UNA_CLAVE_LARGA_Y_ALEATORIA
jwt.expiration=86400000
```

- `createDatabaseIfNotExist=true` crea `heroes_db` si el usuario tiene permisos.
- Sustituye el secreto de ejemplo por uno propio y no lo subas al repositorio. `jwt.expiration` está en milisegundos (24 h por defecto).
- Si tu MySQL usa el puerto 3306, cambia la URL; el archivo de ejemplo apunta a 3307.

### Ejecución

```bash
./mvnw spring-boot:run        # Windows: mvnw.cmd spring-boot:run
```

La API arranca en `http://localhost:8080`.

### Endpoints

**Autenticación** — base `/api/v1/auth`

| Método | Ruta | Descripción |
|---|---|---|
| `POST` | `/register` | Crea un usuario. Cuerpo: `username`, `password`, `email`, `roles` |
| `POST` | `/login` | Devuelve `{ "token": "…" }` |
| `GET` | `/me` | Datos del usuario autenticado |

**Héroes** — base `/api/v1/heroes`

| Método | Ruta | Descripción |
|---|---|---|
| `GET` | `/` | Lista todos los héroes |
| `GET` | `/{id}` | Héroe por ID |
| `GET` | `/buscar?…` | Búsqueda por filtros |
| `GET` | `/buscar/nombre?prefijo=…` | Héroes cuyo nombre empieza por el prefijo |
| `GET` | `/universo/{universo}` | Héroes de un universo |
| `POST` | `/` | Crea un héroe |
| `PUT` | `/{id}` | Actualiza un héroe |
| `PUT` | `/universo/{universo}/base` | Actualiza un campo común del universo |
| `DELETE` | `/{id}` | Elimina un héroe |
| `POST` | `/{heroeId}/poderes` | Asigna un poder al héroe |
| `DELETE` | `/{heroeId}/poderes/{poderId}` | Quita un poder al héroe |

**Equipos** — base `/api/v1/equipos`: `GET /`, `GET /{id}`, `GET /min-miembros/{count}`, `POST /`, `PUT /{id}`, `DELETE /{id}`.

**Poderes** — base `/api/v1/poderes`: `GET /`, `GET /{id}`, `GET /sin-asignar`, `POST /`, `PUT /{id}`, `DELETE /{id}`, `DELETE /nombre/{nombre}`.

**Identidades secretas** — base `/api/v1/identidades`: `GET /`, `GET /{id}`, `POST /`, `PUT /{id}`, `DELETE /{id}`.

### Autenticación

```bash
# 1. Registrar un usuario
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"demo","password":"secreto123","email":"demo@example.com"}'

# 2. Obtener el token
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"demo","password":"secreto123"}'

# 3. Usar el token
curl http://localhost:8080/api/v1/heroes \
  -H "Authorization: Bearer TU_TOKEN"
```

El campo `roles` del registro acepta `["admin"]`; si se omite, el usuario recibe `ROLE_USER`. Los roles se crean al arrancar, pero la configuración de seguridad actual solo exige estar autenticado: no restringe rutas por rol. Si necesitas permisos distintos por rol, añade reglas en `config/SecurityConfig.java`.

### Licencia

**MIT** — consulta [LICENSE](LICENSE).

---

## English

### Table of contents

- [Overview](#overview)
- [Tech stack](#tech-stack)
- [Project structure](#project-structure)
- [Requirements](#requirements)
- [Configuration](#configuration)
- [Running](#running)
- [Endpoints](#endpoints)
- [Authentication](#authentication)
- [License](#license)

### Overview

A sample REST API built with **Spring Boot 3** and secured with **JWT**. It manages a superhero universe with teams, powers and secret identities, and works as a starting point for projects that need stateless authentication and layered CRUD.

Every route lives under `/api/v1` and, except for registration and login, requires the `Authorization: Bearer <token>` header.

### Tech stack

| Layer | Technology |
|---|---|
| Language | Java 17+ |
| Framework | Spring Boot 3.5.8 (Web, Data JPA, Security, Actuator, Test) |
| Tokens | JJWT 0.11.5 |
| Database | MySQL 8 (official connector) |
| Build | Maven and the Maven Wrapper |
| Passwords | BCrypt |

### Project structure

```text
spring-boot-jwt-heroes-api/
├── src/main/java/com/example/jwt2/
│   ├── JWT2Application.java
│   ├── config/          # Security and role initialisation
│   ├── controllers/     # Auth, heroes, teams, powers and identities
│   ├── dto/             # Data transfer objects
│   ├── entities/        # JPA entities (Heroe, Equipo, Poder, Role, User…)
│   ├── filter/          # Per-request JWT filter
│   ├── repositories/    # Spring Data JPA
│   ├── security/        # UserDetails and helpers
│   ├── service/         # Business logic
│   └── util/            # Token generation and validation
├── src/main/resources/application.properties
├── mvnw · mvnw.cmd
├── LICENSE
└── README.md
```

### Requirements

- **JDK 17** or later.
- **MySQL 8** listening on port **3307** (configurable).
- Maven is optional: the wrapper ships with the repo.

### Configuration

Edit `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3307/heroes_db?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

jwt.secret=A_LONG_RANDOM_KEY
jwt.expiration=86400000
```

- `createDatabaseIfNotExist=true` creates `heroes_db` when the user has enough privileges.
- Replace the sample secret with your own and never commit it. `jwt.expiration` is in milliseconds (24 h by default).
- If your MySQL uses port 3306, change the URL; the sample file points at 3307.

### Running

```bash
./mvnw spring-boot:run        # Windows: mvnw.cmd spring-boot:run
```

The API starts at `http://localhost:8080`.

### Endpoints

**Authentication** — base `/api/v1/auth`

| Method | Path | Description |
|---|---|---|
| `POST` | `/register` | Creates a user. Body: `username`, `password`, `email`, `roles` |
| `POST` | `/login` | Returns `{ "token": "…" }` |
| `GET` | `/me` | Authenticated user data |

**Heroes** — base `/api/v1/heroes`

| Method | Path | Description |
|---|---|---|
| `GET` | `/` | Lists every hero |
| `GET` | `/{id}` | Hero by ID |
| `GET` | `/buscar?…` | Filtered search |
| `GET` | `/buscar/nombre?prefijo=…` | Heroes whose name starts with the prefix |
| `GET` | `/universo/{universo}` | Heroes in a universe |
| `POST` | `/` | Creates a hero |
| `PUT` | `/{id}` | Updates a hero |
| `PUT` | `/universo/{universo}/base` | Updates a shared field for the universe |
| `DELETE` | `/{id}` | Deletes a hero |
| `POST` | `/{heroeId}/poderes` | Assigns a power to the hero |
| `DELETE` | `/{heroeId}/poderes/{poderId}` | Removes a power from the hero |

**Teams** — base `/api/v1/equipos`: `GET /`, `GET /{id}`, `GET /min-miembros/{count}`, `POST /`, `PUT /{id}`, `DELETE /{id}`.

**Powers** — base `/api/v1/poderes`: `GET /`, `GET /{id}`, `GET /sin-asignar`, `POST /`, `PUT /{id}`, `DELETE /{id}`, `DELETE /nombre/{nombre}`.

**Secret identities** — base `/api/v1/identidades`: `GET /`, `GET /{id}`, `POST /`, `PUT /{id}`, `DELETE /{id}`.

### Authentication

```bash
# 1. Register a user
curl -X POST http://localhost:8080/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"demo","password":"secret123","email":"demo@example.com"}'

# 2. Get the token
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username":"demo","password":"secret123"}'

# 3. Use the token
curl http://localhost:8080/api/v1/heroes \
  -H "Authorization: Bearer YOUR_TOKEN"
```

The `roles` field accepts `["admin"]`; when omitted, the user gets `ROLE_USER`. Roles are created on startup, but the current security config only requires authentication: it does not restrict routes by role. Add rules in `config/SecurityConfig.java` if you need per-role permissions.

### License

**MIT** — see [LICENSE](LICENSE).
