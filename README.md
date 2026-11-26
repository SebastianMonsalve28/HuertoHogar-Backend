# Huerto Hogar - Backend

## Desarrollo Fullstack II - DUOC UC

### Integrantes

- Sebastian Monsalve
- Lucas Parra

### Descripción del proyecto

Huerto Hogar es una aplicación web de comercio electrónico dedicada a la venta de frutas, verduras y productos naturales.

El backend proporciona una API REST que permite gestionar productos, usuarios, pedidos, compras, cajas personalizadas y valoraciones, utilizando una base de datos MySQL.

El proyecto fue desarrollado para la asignatura Desarrollo Fullstack II.

## Tecnologías utilizadas

- Java 17
- Spring Boot
- Spring Security
- Spring Data JPA
- Hibernate
- MySQL
- Docker Compose
- JWT (JSON Web Token)
- Swagger / OpenAPI
- Maven
- JUnit

## Funcionalidades

- Registro e inicio de sesión de usuarios.
- Autenticación mediante JWT.
- Gestión de sesiones.
- Control de acceso según roles.
- Operaciones CRUD de productos.
- Catálogo inicial de 15 productos.
- Gestión de categorías.
- Control y validación de stock.
- Gestión de pedidos y compras.
- Cálculo de descuentos e IVA del 19%.
- Gestión de cajas preparadas y personalizadas.
- Valoraciones de productos.
- Persistencia de datos en MySQL.
- Documentación de API REST mediante Swagger.

## Roles de usuario

| Rol | Permisos |
|---|---|
| Administrador | Administración de productos, usuarios y pedidos. |
| Vendedor | Consulta de productos, pedidos y sus detalles. |
| Cliente | Consulta del catálogo, compras y valoraciones. |

## Estructura del proyecto

```text
backend/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── cl/duoc/huertohogar/
│   │   │       ├── auth/
│   │   │       ├── config/
│   │   │       ├── model/
│   │   │       ├── repository/
│   │   │       ├── service/
│   │   │       └── web/
│   │   └── resources/
│   └── test/
├── .env.example
├── .env.docker.example
├── .gitignore
├── crear_base.sql
├── docker-compose.yml
├── pom.xml
└── README.md
```

## Requisitos de instalación

- Java JDK 17 o superior.
- Apache Maven.
- Docker Desktop.
- Visual Studio Code.
- Git.

## Instalación y ejecución

### 1. Clonar el repositorio

```bash
git clone https://github.com/SebastianMonsalve28/HuertoHogar-Backend.git
cd HuertoHogar-Backend
```

### 2. Configurar las variables de entorno

Desde PowerShell:

```powershell
Copy-Item .env.example .env
```

Editar el archivo `.env` y configurar las siguientes variables:

```env
DB_ROOT_PASSWORD=TU_CLAVE_ROOT
DB_URL=jdbc:mysql://127.0.0.1:13317/huerto_hogar?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=America/Santiago
DB_USER=huerto
DB_PASSWORD=TU_CLAVE_MYSQL
JWT_SECRET=TU_SECRETO_ALEATORIO_DE_AL_MENOS_32_BYTES
APP_ADMIN_EMAIL=admin@duoc.cl
APP_ADMIN_PASSWORD=TU_CLAVE_ADMIN
APP_VENDOR_EMAIL=vendedor@duoc.cl
APP_VENDOR_PASSWORD=TU_CLAVE_VENDEDOR
FRONTEND_ORIGIN=http://127.0.0.1:15173
COOKIE_SECURE=false
```

Reemplazar los valores de ejemplo por credenciales propias.

Si existe una base de datos anterior, utilizar las contraseñas con las que fue creada.

### 3. Iniciar la base de datos

Abrir Docker Desktop y ejecutar:

```powershell
docker compose up -d
```

### 4. Cargar las variables de entorno

```powershell
Get-Content .env | Where-Object { $_ -match '^[A-Za-z_][A-Za-z0-9_]*=' } | ForEach-Object {
    $key, $value = $_ -split '=', 2
    [Environment]::SetEnvironmentVariable($key, $value, 'Process')
}
```

### 5. Ejecutar Spring Boot

En la misma terminal:

```powershell
mvn spring-boot:run
```

## Puertos y direcciones

| Servicio | Dirección |
|---|---|
| Frontend | http://127.0.0.1:15173 |
| Backend | http://127.0.0.1:18082 |
| Swagger | http://127.0.0.1:18082/swagger-ui.html |
| MySQL | 127.0.0.1:13317 |

## Documentación de la API

La documentación de la API REST se encuentra disponible mediante Swagger:

http://127.0.0.1:18082/swagger-ui.html

Swagger permite consultar y probar los endpoints del sistema, incluyendo las operaciones que requieren autenticación JWT.

## Integración con el frontend

El frontend está desarrollado con React y se comunica con Spring Boot mediante solicitudes HTTP a la API REST.

```text
Frontend React
      |
      | HTTP / JSON / JWT
      |
Backend Spring Boot
      |
      | JPA / Hibernate
      |
Base de datos MySQL
```

URL base de la API:

```text
http://127.0.0.1:18082/api/v1
```

Repositorio original del proyecto:

https://github.com/SebastianMonsalve28/tienda_HUERTO_HOGAR

Para utilizar el iniciador automático del proyecto completo, se deben mantener las carpetas frontend y backend dentro de una misma carpeta junto con los scripts de inicio.

## Pruebas automatizadas

El backend incluye pruebas de:

- Autenticación y sesiones.
- Seguridad de la API.
- Permisos del vendedor.
- Catálogo de productos.
- Cajas y valoraciones.
- Compras e impuestos.
- Integración de servicios.

Para ejecutar las pruebas:

```powershell
mvn test
```

## Seguridad

- Autenticación mediante JWT.
- Contraseñas protegidas mediante BCrypt.
- Autorización según roles.
- Validación de solicitudes.
- Configuración de CORS.
- Protección de endpoints privados.
- Credenciales mediante variables de entorno.

Los archivos `.env`, las contraseñas y los secretos JWT no deben publicarse en GitHub.

## Contexto académico

Proyecto desarrollado para el Examen Final Transversal de Desarrollo Fullstack II (DSY1104), DUOC UC.

El sistema corresponde a una demostración académica y no realiza cobros reales.

## Desarrolladores

- Sebastian Monsalve
- Lucas Parra

2026 - Huerto Hogar
