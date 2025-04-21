# Cuentas Service

Microservicio encargado de gestionar cuentas bancarias y sus movimientos asociados. Permite la creación, consulta y actualización de cuentas, así como registrar movimientos (retiros, depósitos, reversiones).

<br> <!-- Salto de línea -->
## Contenido

- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Funcionalidades Principales]()
- [Clonar y levantar el proyecto](#-clonar-y-levantar-el-proyecto)
- [Endpoints](#-endpoints)
- [Excepciones](#excepciones)
- [Pruebas](#-pruebas)
- [Arquitectura](#arquitectura)


<br> <!-- Salto de línea -->
## 🧩 Funcionalidades Principales (Darle prioridad a las funcionalidades que piden)

- Gestión de clientes: creación, consulta, actualización y eliminación.
- Gestión de cuentas bancarias: creación, consulta y actualización.
- Registro de movimientos bancarios: creación, consulta y reversiones.
- Generación de reporte de estado de cuenta por cliente y rango de fechas.
- Validaciones de negocio robustas (saldo insuficiente, cuentas inactivas, etc).
- Comunicación con microservicio externo de clientes.

<br> <!-- Salto de línea -->
## ⚙️ Tecnologías utilizadas

- **Java 21**
- **Spring Boot 3**
- **JPA**
- **PostgreSQL**
- **Docker & Docker Compose**
- **AWS SQS**
- **JUnit 5**
- **Arquitectura Limpia (Clean Architecture)**


<br> <!-- Salto de línea -->
## 🛠️ Clonar y levantar el proyecto

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

Esta sección describe todos los endpoints REST expuestos por los microservicios **clientes-service** y **cuentas-service**, accesibles una vez los servicios estén desplegados con Docker. También incluye una colección de Postman para facilitar el consumo de las API.

<br> <!-- Salto de línea -->
### 📌 Los puertos por defecto son:

- clientes-service: http://localhost:8080
- cuentas-service: http://localhost:8081

<br> <!-- Salto de línea -->
### 🌐 Rutas base por servicio

| Servicio    | Base URL                           | Descripción
|-------------|------------------------------------|-------------------------------------------
| Clientes    | http://localhost:8080/clientes     | CRUD y consulta de clientes
| Cuentas     | http://localhost:8081/cuentas      | CRUD y consulta de cuentas
| Movimientos | http://localhost:8081/movimientos  | Registro y consulta de movimientos


<br> <!-- Salto de línea -->
### 📬 Colección de Postman
Puedes usar la colección de Postman para probar rápidamente todos los endpoints disponibles.

Ruta dentro del repositorio:

[📄 Devsu Postman Collection](./docs/Devsu-Postman-Collection.json)

> Asegúrate de tener los servicios levantados (clientes-service en 8080, cuentas-service en 8081) antes de hacer peticiones.


<br> <!-- Salto de línea -->
### 👤 Clientes (`/clientes`)

| Método | Endpoint                                     | Descripción                             |
|--------|----------------------------------------------|-----------------------------------------|
| POST   | `/clientes`                                  | Crear un nuevo cliente                               |
| GET    | `/clientes`                                  | Listar todos los clientes                            |
| GET    | `/clientes/{id}`                             | Consultar cliente por ID                             |
| GET    | `/clientes/identificacion/{identificacion}`  | Consultar cliente por número identificación          |
| PUT    | `/clientes/{id}`                             | Actualizar datos de un cliente                       |
| DELETE | `/clientes/{id}`                             | Eliminar cliente por cuentaId                        |

<br> <!-- Salto de línea -->
### 🏦 Cuentas (`/cuentas`)

| Método | Endpoint                                    | Descripción                             |
|--------|---------------------------------------------|-----------------------------------------|
| GET    | `/cuentas`                                  | Listar todas las cuentas                |
| GET    | `/cuentas/{id}`                             | Consultar cuenta por ID                 |
| GET    | `/cuentas/numero-cuenta/{numero-cuenta}`    | Consultar cuenta por número de cuenta   |
| POST   | `/cuentas`                                  | Crear nueva cuenta                      |
| PUT    | `/cuentas/{numero-cuenta}`                  | Actualizar datos de una cuenta          |
| GET    | `/cuentas/reportes?identificacionCliente={identificacion}&desde={fecha1}&hasta={fecha2}`                        | Reporte de estado de cuenta por cliente y rango de fechas |
>  El reporte de estado de cuenta incluye el saldo actual de cada cuenta asociada y el detalle de movimientos en el rango de fechas solicitado.


<br> <!-- Salto de línea -->
### 💸 Movimientos (`/movimientos`)

| Método | Endpoint                                    | Descripción                             |
|--------|---------------------------------------------|-----------------------------------------|
| POST   | `/movimientos`                              | Crear movimiento       |
| POST   | `/movimientos/{id}/revertir`                | Revertir un movimiento             |
| GET    | `/movimientos`                              | Consultar todos los movimientos        |
| GET    | `/movimientos/{id}`                         | Consultar movimiento por Id             |
| GET    | `/movimientos/cuenta/{id}`                  | Consultar movimientos por cuentaId        |
> Al registrar un movimiento, si el saldo es insuficiente, se lanza una excepción con una respuesta controlada.

> En lugar de eliminar movimientos físicamente, se cambia el tipoMovimiento a "REVERTIDO: original_tipo" y se crea un nuevo movimiento con el tipoMovimiento "REVERSION" para mantener trazabilidad y llevar el registro de las transacciones realizadas.

<br> <!-- Salto de línea -->
### 🧾 Ejemplos de Request Body
#### 📍 POST /clientes
Crea un nuevo cliente.
```json
{
  "nombre": "Santiago Pérez",
  "genero": "Masculino",
  "edad": 35,        
  "identificacion": "1230000123",
  "direccion": "Calle 123 #45-67",
  "telefono": "3101234567",
  "contraseña": "pass123",
  "estado": true
}
```
---
#### 📍 PUT /clientes/{id}
Actualiza los datos de un cliente existente.
```json
{
  "nombre": "Santiago Pérez Update",
  "genero": "Masculino",
  "edad": 35,
  "identificacion": "1000123123",
  "direccion": "Carrera 10 #45-89",
  "telefono": "3102351212",
  "contraseña": "claveActualizada",
  "estado": true
}
```
---
#### 📍 POST /cuentas
Crea una nueva cuenta asociada a un cliente.
```json
{
  "numeroCuenta": "600700800",
  "tipoCuenta": "Ahorros",
  "estado": true,
  "clienteId": 1
}
```
---
#### 📍 PUT /cuentas/{numeroCuenta}
Actualiza los datos de una cuenta existente.
```json
{
  "tipoCuenta": "Ahorros Update",
  "estado": false
}
```
---
#### 📍 POST /movimientos
Crea un nuevo movimiento.
> El valor positivo representa un depósito, y el valor negativo un retiro.
##### Ejemplo de Depósito:
```json
{
  "tipoMovimiento": "Deposito 200.0000",
  "valor": 2000000,
  "cuentaId": 1
}
```
##### Ejemplo de Retiro:
```json
{
  "tipoMovimiento": "Retiro 200.0000",
  "valor": -2000000,
  "cuentaId": 1
}
```
---
#### 📍 POST /movimientos/{id}/revertir
Revierte un movimiento previamente realizado.
> No requiere un cuerpo en la solicitud (body vacío).
---

<br> <!-- Salto de línea -->
### 📈 Endpoint: Generación de Reporte de Cuentas
#### 📍 POST /cuentas/reportes
Obtiene un reporte consolidado de los movimientos de todas las cuentas asociadas a un cliente, dentro de un rango de fechas.
Ejemplo de URL:
```
http://localhost:8081/cuentas/reportes?identificacionCliente=1234567890&desde=2024-01-01&hasta=2025-04-30
```


---
<br> <!-- Salto de línea -->
## 🚨 Manejo de Excepciones

La aplicación implementa un sistema centralizado y controlado para el manejo de errores.

### Enfoque Adoptado
Cada microservicio define sus propias excepciones personalizadas dentro de la capa de dominio. Estas excepciones son lanzadas desde los casos de uso (use cases) ubicados en la capa de aplicación. 
Posteriormente, un manejador global de excepciones captura y procesa estas excepciones, devolviendo respuestas HTTP claras, estructuradas y con información relevante para el cliente.

<br> <!-- Salto de línea -->
### Ejemplo de Respuesta de Error
Cuando ocurre una excepción, el cliente recibe una respuesta estructurada como esta:

```json
{
    "status": 400,
    "success": false,
    "message": "Saldo no disponible para realizar el movimiento.",
    "timestamp": "2025-04-20 19:13:35"
}
```
<br> <!-- Salto de línea -->
### Excepciones Personalizadas y sus Códigos


| Excepción                     | Códgio | Descripción
|-------------------------------|--------|----------------------------------------------------
| DuplicatedClientException     | 409	 | Ya existe un cliente con la misma identificación.
| DuplicateAccountException     | 409	 | Ya existe una cuenta con ese número.
| InactiveAccountException      | 400    | Se intentó operar sobre una cuenta inactiva.
| InsufficientBalanceException  | 400    | Saldo insuficiente para realizar el movimiento
| NotFoundException             | 404    | El recurso solicitado no fue encontrado.

---
<br> <!-- Salto de línea -->
## 🧪 Pruebas
Las pruebas unitarias están en la carpeta `src/test/java` se pueden ejecutar con:

```bash
(agregar informaicon relacioanda a la ejecucion de las pruebas)
```

---
<br> <!-- Salto de línea -->
## 🏛️ Arquitectura

| Capa                    | Descripción
|-------------------------|------------------------------------------
|        Domain           | ← Entidades, lógica y reglas del negocio
|      Application        | ← Casos de uso y orquestación 
|     Infrastructure      | ← Adaptadores, controladores, gateways


---
