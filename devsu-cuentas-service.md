# Cuentas Service (TEST)

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta, actualización y eliminación de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

<br> <!-- Salto de línea -->

## Contenido

- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Clonar y levantar el proyecto](#-clonar-y-levantar-el-proyecto)
- [Documentacion swagger](#-documentación-swagger)
- [Endpoints](#-endpoints)
- [Descripcion de Endpoints](#-descripcion-de-endpoints)
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

<br> <!-- Salto de línea -->
### Clonar repositorio

1. Clona este repositorio en tu máquina local:
```bash
git clone https://github.com/Vex-Alexis/Backend-BankInc.git
```

<br> <!-- Salto de línea -->
### Levantar el proyecto

2. Navega al directorio del proyecto:
```bash
cd Backend-BankInc
```

3. Compila el proyecto y descarga las dependencias utilizando Maven:
```bash
mvn clean install
```

4. Ejecuta la aplicación o usa tu IDE favorito
```bash
mvn spring-boot:run
```
La API de Bank Inc Portal Web debería estar en funcionamiento en http://localhost:8080



---
<br> <!-- Salto de línea -->

## 🌐 Documentación Swagger 
Una vez desplegado el microservicio:
(http://localhost:8081/swagger-ui.html)

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
<br> <!-- Salto de línea -->
## 🚀 Descripcion endpoints

---
<br> <!-- Salto de línea -->
🧪 Pruebas
Las pruebas unitarias están en la carpeta src/test/java. Se puede ejecutar con:

---
<br> <!-- Salto de línea -->
## Arquitectura



---
