# Cuentas Service (TEST)

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta, actualización y eliminación de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

<br> <!-- Salto de línea -->

## Contenido

- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Clonar y levantar el proyecto](#-clonar-y-levantar-el-proyecto)
- [Documentacion swagger](#-documentacion-swagger)
- [Endpoints](#-endpoints)
- [Descripcion de cada endpoint](#-descripcion-de-cada-endpoint)
- [Pruebas](#pruebas)
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

## 🔧 Clonar y levantar el proyecto

### Opción 1: Maven

```bash
./mvnw spring-boot:run
```
---
<br> <!-- Salto de línea -->



---
<br> <!-- Salto de línea -->




---
<br> <!-- Salto de línea -->

## 🚀 Endpoints

<br> <!-- Salto de línea -->

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
