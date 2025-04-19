# Cuentas Service

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta, actualización y eliminación de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

<br> <!-- Salto de línea -->

## Contenido

- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Clonar y levantar el proyecto](#-clonar-y-levantar-el-proyecto)
- [Endpoints](#-endpoints)
- [Descripcion Endpoints](#-descripcion-endpoints)
- Excepciones
- [Pruebas](#-pruebas)
- [Arquitectura](#arquitectura)



<br> <!-- Salto de línea -->

## ⚙️ Tecnologías utilizadas

- **Java 17**
- **Spring Boot 3**
- **JPA**
- **PostgreSQL**
- **Docker & Docker Compose**
- **AWS SQS**
- **JUnit 5**
- **Arquitectura Limpia (Clean Architecture)**
- 

<br> <!-- Salto de línea -->

## 🔧 Clonar y levantar el proyecto

<br> <!-- Salto de línea -->
1. Clona el repositorio:
```bash
git clone https://github.com/Vex-Alexis/devsu-cuentas-sevice
```
<br> <!-- Salto de línea -->
2. Navega al directorio del proyecto:
```bash
cd devsu-cuentas-sevice/docker-compose
```
3. Levanta los servicios:
```bash
docker-compose up --build
```
4. Servicios expuestos:


| Servicio                | Puerto
|-------------------------|------
| clientes-service        | `8080`
| cuentas-service         | `8081`
| PostresSQL              | `5432`

> Asegúrate de que no estén siendo usados por otros procesos.



<br> <!-- Salto de línea -->
## 🚀 Endpoints
<br> <!-- Salto de línea -->

| Método | Endpoint                      | Descripción                             |
|--------|-------------------------|-----------------------------------------|
| GET    | `/cuentas`                                  | Listar todas las cuentas                |
| GET    | `/cuentas/numero-cuenta/{numero-cuenta}`    | Consultar cuenta por número de cuenta            |
| GET    | `/cuentas/{id}`                             | Consultar cuenta por Id                   |
| POST   | `/cuentas`                                  | Crear nueva cuenta                      |
| PUT    | `/cuentas/{numero-cuenta}`                  | Actualizar cuenta                       |
|        |                                             |
| GET    | `/cuentas/reportes?`                        | Consulta el reporte de estado de cuenta |
|        |                                             |
| POST   | `/movimientos`                              | Crear movimiento       |
| POST   | `/movimientos/{id}/revertir`                | Revertir un movimiento             |
| GET    | `/movimientos`                              | Consultar todos los movimientos        |
| GET    | `/movimientos/{id}`                         | Consultar movimiento por Id             |
| GET    | `/movimientos/cuenta/{id}`                  | Consultar movimientos por cuentaId        |


---
<br> <!-- Salto de línea -->
## 🚀 Descripcion endpoints

---
<br> <!-- Salto de línea -->
## 🧪 Pruebas
Las pruebas unitarias están en la carpeta `src/test/java` se pueden ejecutar con:

```bash
(agregar informaicon relacioanda a la ejecucion de las pruebas)
```

---
<br> <!-- Salto de línea -->
## Arquitectura



---
