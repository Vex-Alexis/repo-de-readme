# Cuentas Service (TEST)

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta, actualización y eliminación de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

---
<br> <!-- Salto de línea -->

## ⚙️ Tecnologías utilizadas

- **Java 17**
- **Spring Boot 3**
- **Arquitectura Limpia**
- **PostgreSQL**
- **Maven**
- **Docker & Docker Compose**
- **Swagger / OpenAPI**


## 🔧 Cómo ejecutar

### Opción 1: Maven

```bash
./mvnw spring-boot:run
```

---

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
