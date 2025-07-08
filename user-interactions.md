# 📊 Sistema de Registro de Estadísticas de Interacciones

Este proyecto representa una aplicación basada en un microservicio, diseñada para procesar estadísticas de interacciones de usuarios, almacenar los datos en una base NoSQL (DynamoDB) y publicar eventos en una cola de mensajería (RabbitMQ). La solución está construida siguiendo los principios de la Arquitectura Limpia, empleando el Scaffold de Bancolombia. El proyecto está completamente dockerizado, permitiendo su despliegue local de forma rápida y sencilla.

<br> <!-- Salto de línea -->

## 🚀 Funcionalidades

- Recepción de estadísticas de interacciones vía API REST
- Validación de integridad mediante hash MD5
- Persistencia de datos en Amazon DynamoDB (Local)
- Publicación de eventos en RabbitMQ si el guardado es exitoso
- Manejo de errores controlado con tipos de excepciones específicas
- Pruebas unitarias

<br> <!-- Salto de línea -->

## 🛠️ Tecnologías

- Java 21
- Spring WebFlux
- Reactor (programación reactiva)
- Amazon DynamoDB (Local)
- RabbitMQ
- Docker y Docker Compose
- Scaffold Bancolombia (Arquitectura Limpia)

<br> <!-- Salto de línea -->


## 📁 Estructura del Proyecto

```css
application/
  └─ app-service/               <- Arma y configura toda la aplicación (Inyecta dependencias y ejecuta el main).

domain/
  └─ model/                      <- Entidades del dominio y gateways (puertos)
  └─ useCase/                    <- Casos de uso que contienen la lógica y reglas de negocio.

infrastructure/
  └─ driven-adapters/            <- Adaptadores, implementan puertos para conexiones externas (DB, APIs, Producer, etc)
  └─ entry-points/               <- Puntos de entrada (como controladores REST, Kafka, GraphQL, consumer, etc) 
```

<br> <!-- Salto de línea -->


## 📢 Ejecutar proyecto

### Requisitos: 
- Java 21
- Docker Compose
- AWS CLI

### Clonar y levantar

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

#### Esto levantará:
| Servicio                               | Puerto
|----------------------------------------|------
| Microservicio   `user-interactions`    | puerto `8080`
| Dynamodb-local                         | puerto `8081`
| RabbitMQ                               | puertos `5672` (AMQP) y `15672` (UI)

> El Microservicio estará disponible en: `http://localhost:8080`
> Asegúrate de que no estén siendo usados por otros procesos.


## ⚙️ Configuraciones Iniciales
Una vez los servicios esten corriendo, realiza las siguientes configruaciones iniciales.

### Crear tabla en DynamoDB
- Debes tener instalado AWS CLI para crear la tabla requerida (interaction_stats) ejecutando el siguiente comando:
```bash
aws dynamodb create-table --table-name interaction_stats --attribute-definitions AttributeName=timestamp,AttributeType=S --key-schema AttributeName=timestamp,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 --endpoint-url http://localhost:8000 --region us-east-1
```

### Crear cola en RabbitMQ
- Para publicar evento en RabbitMQ debe exitir la cola `event.stats.validated`, verifica que ya exista o creala con los siguientes pasos:
1. Abre http://localhost:15672
2. Ingresa con:
  - usuario: guest
  - contraseña: guest
3. Ve a la sección Queues and Streams → Add a new queue
4. Nombre: event.stats.validated
5. Tipo: classic
6. Haz clic en Add queue




- Crear una tabla en DynamoDB llamada `interaction_stats`
- Crear cola en RabbitMQ manualmente desde `http://localhost:15672` con el nombre `event.stats.validated`

<br> <!-- Salto de línea -->


## 🌐 Flujo de la Aplicación
1. Se recibe una petición POST /api/stats con los datos de interacciones.
2. Se valida el hash MD5 del contenido.
3. Si el hash es válido:
   - Se almacena en DynamoDB
   - Se publica un evento a RabbitMQ
4. Si el hash es inválido o ocurre un error:
   - Se responde mensaje de error

<br> <!-- Salto de línea -->


# Endpoint Expuesto

| Método | Endpoint                              | Descripción                                      |
|--------|---------------------------------------|--------------------------------------------------|
| POST   | `/api/stats`                          | Recepción de estadísticas y procesamiento        |
| GET    | `/api/stats/test`                     | Verificación de disponibilidad del servicio      |


### Detalle del endpoint (`/api/stats`):

- Método: POST
- Ruta: `http://localhost:8080/api/stats`
- Body de ejemplo:

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
- Respuesta esperada:
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

### Ejecuta pruebas unitarias e integración
- 
```bash
./gradlew test
```
---

<br> <!-- Salto de línea -->

## Author
### Alexis Chavarría
Email: alexischavarria@hotmail.com
<br> <!-- Salto de línea -->












