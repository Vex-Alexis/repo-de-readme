# Cuentas Service (TEST)

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta, actualización y eliminación de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

<br> <!-- Salto de línea -->

## Contenido

- [Tecnologías Utilizadas](#tecnologías-utilizadas)
- Requisitos para levantar el proyecto
- Clonar y levantar el proyecto
- Documentacion - swagger
- Endpoints
- Descripcion de cada endpoint
- Pruebas
- [Arquitectura](#arquitectura)



<br> <!-- Salto de línea -->

## ⚙️ Tecnologías utilizadas

- **Java 17**
- **Spring Boot 3**
- **Arquitectura Limpia**
- **PostgreSQL**
- **Maven**
- **Docker & Docker Compose**
- **Swagger / OpenAPI**

<br> <!-- Salto de línea -->

## 🔧 Cómo ejecutar

### Opción 1: Maven

```bash
./mvnw spring-boot:run
```

<br> <!-- Salto de línea -->

## 🚀 Endpoints principales

| Método | Endpoint                | Descripción                             |
|--------|-------------------------|-----------------------------------------|
| GET    | `/cuentas`              | Listar todas las cuentas                |
| GET    | `/cuentas/{id}`         | Obtener cuenta por ID                   |
| POST   | `/cuentas`              | Crear nueva cuenta                      |
| PUT    | `/cuentas/{id}`         | Actualizar cuenta                       |
| DELETE | `/cuentas/{id}`         | Eliminar cuenta                         |
| POST   | `/movimientos`          | Crear movimiento (retiro o depósito)    |
| POST   | `/movimientos/{id}/revertir` | Revertir un movimiento             |

---

## Arquitectura





---
