# 🏦 Reto técnico Java Scaffold

Este documento presenta el desarrollo de un microservicio construido en Java con Spring Boot, utilizando arquitectura limpia basada en el scaffold de Bancolombia. El objetivo principal del servicio es exponer un endpoint POST para almacenar información en DynamoDB y publicar un evento en RabbitMQ. El proyecto está completamente dockerizado, permitiendo su despliegue local de forma rápida y sencilla.
<br> <!-- Salto de línea -->

#  Funcionalidades
Puedes usar viñetas o un diagrama (si tienes tiempo, un diagrama tipo flujo es ideal). Aquí un ejemplo simple:

1. Se recibe una solicitud POST con los datos del usuario.
2. Se valida y transforma el payload a una entidad de dominio.
3. Se guarda la información en DynamoDB.
4. Se genera un evento y se envía a RabbitMQ.
<br> <!-- Salto de línea -->

# Tecnologías

- ☕ Java 17
- ⚙️ Spring Boot
- 🧱 Arquitectura Limpia (Scaffold Bancolombia)
- 🐳 Docker & Docker Compose
- 📦 DynamoDB (LocalStack)
- 🐇 RabbitMQ
- 🌐 REST API (POST)
<br> <!-- Salto de línea -->


# Estructura del Proyecto
Aquí puedes insertar una imagen del árbol de carpetas o escribirlo de forma visual.
```css
application/
  ├── usecase/               <- Casos de uso o servicios de aplicación

domain/
  └─ model/                  <- Entidades del dominio y gateways (interfaces)
  └─ useCase/                <- Interfaces de los casos de uso

infrastructure/
  └─ adapters/               <- Adaptadores de salida (Base de datos, clientes REST, colas, etc)
  └─ entry-points/           <- Adaptadores de entrada (REST controllers, GraphQL, solicitudes externas) 
```
<br> <!-- Salto de línea -->


#  Ejecutar proyecto

1. Clonar
2. Levantar entorno
3. Configuraciones
4. 
<br> <!-- Salto de línea -->


# Endpoint Expuesto
Incluye el detalle del endpoint:

Método: POST
Ruta: /api/stats
Body de ejemplo:

```json
{
  "totalContactoClientes": 300,
  "motivoReclamo": 15,
  "motivoGarantia": 20,
  "motivoDuda": 50,
  "motivoCompra": 80,
  "motivoFelicitaciones": 5,
  "motivoCambio": 10,
  "hash": "2692af3c8d7a895a40bb0be1fd160c3b"
}
```
Respuesta esperada:
```json
{
    "httpStatus": 201,
    "success": true,
    "message": "Estadística almacenada en DynamoDB y evento enviado a RabbitMQ",
    "timestamp": "2025-07-07 14:58:42",
    "data": {
        "totalContactoClientes": 300,
        "motivoReclamo": 15,
        "motivoGarantia": 20,
        "motivoDuda": 50,
        "motivoCompra": 80,
        "motivoFelicitaciones": 5,
        "motivoCambio": 10,
        "hash": "2692af3c8d7a895a40bb0be1fd160c3b",
        "timestamp": "2025-07-07 14:58:42.556"
    }
}
```
<br> <!-- Salto de línea -->


#  Pruebas

1. Clonar
2. Levantar entorno
3. Configuraciones
4. 
<br> <!-- Salto de línea -->



>  End
<br> <!-- Salto de línea -->

# Author
### Alexis Chavarría
Email: alexischavarria@hotmail.com
4. 
<br> <!-- Salto de línea -->




















# Instalación y Ejecución del Proyecto (Docker Compose)
Incluye instrucciones claras para clonar y levantar el proyecto.

1. Clona el repositorio:
```bash
git clone https://github.com/Vex-Alexis/................
```
<br> <!-- Salto de línea -->
2. Navega al directorio del proyecto:
```bash
cd data-power-bancolombia
```
3. Levanta los servicios:
```bash
docker-compose up --build
```
> El servicio estará disponible en: http://localhost:8080/api/stats














