# 📦 Sistema de Gestión de Inventario

Sistema de gestión de inventario basado en **microservicios**, desarrollado en **Java 21** con **Spring Boot 3.5.3**.  
Permite registrar productos, consultar su inventario y registrar movimientos de stock

<br> <!-- Salto de línea -->
## Contenido



- [Funcionalidades Principales](#-funcionalidades-principales)
- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Instalación y ejecución](#-instalación-y-ejecución)
- [Descripción de la arquitectura y patrones de diseño](#%EF%B8%8F-descripción-de-la-arquitectura-y-patrones)
- [Diagrama de interacción entre servicios](#-diagrama-de-interacción-entre-servicios)
- [Decisiones técnicas y justificaciones](#%EF%B8%8F-decisiones-técnicas-y-justificaciones)
- [Explicación del flujo de compra implementado](#-explicación-del-flujo-de-compra-implementado)
- [Endpoints](#-endpoints)
- [Documentación de endpoints](#-documentación-de-endpoints)
- [Manejo de Excepciones](#-manejo-de-excepciones)
- [Pruebas](#-pruebas)
- [Documentación sobre el uso de herramientas de IA](#-documentación-sobre-el-uso-de-herramientas-de-ia)




<br> <!-- Salto de línea -->
## 🧩 Funcionalidades Principales

- Crear producto, consultar por ID y obtener lista de productos
- Consultar stock de producto y obtener su informacion desde el otro microservicio
- Actualizar cantidad disponible de producto
- Endpoint de movimientos (para integrar flujo de compras o transacciones)
- Comunicacion sincronica entre microservicios mediante HTTP
- Arquitectura limpia y patrones de diseño
- Se implementa transaccion para mantener la consistencia de datos entre ambos servicios (atomicidad)
- Manejo de exepciones, se implementan personalizadas y se crean un manejador global de excepciones
- Respuestas del API cumpliendo los estandares de JSON:API
- Autenticacion basica mediante API keys
- Manejo de timeouts y reintentos basicos con circuit braker
  



<br> <!-- Salto de línea -->
## 🛠️ Tecnologías Utilizadas
- Java 21
- Spring Boot 3.5.3
- Spring WebFlux (WebClient)
- PostgreSQL
- Resilience4j (Circuit Breaker)
- Docker & Docker Compose
- Maven


<br> <!-- Salto de línea -->
## 📦 Instalación y ejecución

1. Clona el repositorio:
```bash
git clone https://github.com/Vex-Alexis/devsu-sistema-bancario.git
```
2. Navega al directorio del proyecto:
```bash
cd devsu-sistema-bancario
```
3. Levanta los servicios:
```bash
docker-compose up -d
```
4. Servicios expuestos:

| Servicio                | Puerto
|-------------------------|------
| product-service         | `8080`
| inventory-service       | `8081`
| product-db              | `5433`
| inventory-db            | `5434`

> Asegúrate de que no estén siendo usados por otros procesos.


<br> <!-- Salto de línea -->
## 🏛️ Descripción de la arquitectura y patrones

El proyecto está implementado una **Arquitectura limpia** con el patrón **Ports & Adapters (arquitectura hexagonal)** y aplicando principios de **DDD (Domain-Driven Design)** para una mejor separación de responsabilidades y mantenibilidad. Cada capa tiene su responsabilidad: 

<p align="center">
  <img src="estructura-microservicio.png" alt="Arquitectura general" width="400"/>
</p>

 #### - Domain
Contiene los modelos y entidades de dominio, que representan las reglas y la lógica de negocio También define los puertos como interfaces ("Gateways") que se utilizarán en la capa de negocio.
 #### - Business
Define la lógica de la aplicación y reacciona a las invocaciones de los `entry-poits`, orquestando los flujos y utilizando los puertos definidos.
 #### - Infraestructure
En esta capa, se detallarán las tecnologías e implementaciones de los puertos definidos en la capa de dominio. Esta capa está compuesta por dos grupos de módulos llamados `entry-points` y `driven-adapters`.
  - `driven-adapters` son los módulos implementan las interfaces ("Gateways") para conectar tecnologías externas al sistema, como conexiones a bases de datos, servicios REST, SOAP, lectura de archivos planos y, en particular, cualquier fuente de datos con la que debamos interactuar.
  - `entry-poits` son los puntos de entrada de la aplicación o el inicio de los flujos de negocio. Estos pueden ser controladores REST, consumidores de Kafka, SQS, etc, además de manejo centralizado de excepciones.

## ✏️ patrones de diseño

- **Dependency Injection:** facilita la inversión de dependencias y el desac acoplamiento de componentes.
- **Repository Pattern:** abstrae el acceso a la persistencia, ocultando detalles del almacenamiento.
- **Adapter Pattern:** permite integrar tecnologías o servicios externos sin acoplar el dominio.
- **Service Layer:** encapsula la lógica de negocio de la aplicación.
- **Transactional:** asegura la integridad de los datos durante operaciones críticas.
- **DTO & Mapper:** se usan para transferir datos entre capas y evitar exponer directamente las entidades de dominio.
- **Resilience Patterns:** implementación de reintentos, timeouts u otros mecanismos para mayor tolerancia a fallos.
- **Exception Handler:** manejo centralizado de errores para devolver respuestas consistentes.



<br> <!-- Salto de línea -->
## 🔄 Diagrama de interacción entre servicios


<p align="center">
  <img src="diagrama-interaccion-microservicios.png" alt="Interaccion microservicios" width="600"/>
</p>


El sistema implementa una arquitectura de microservicios donde cada servicio tiene su propia base de datos (Database per Service) y se comunica de la siguiente forma:

- Comunicación síncrona:
`inventory-service` consume el API REST de `product-service` mediante WebClient, para obtener la información del producto.
Para garantizar resiliencia se implementa un circuit breaker que maneja reintentos, fallback y timeout, evitando que fallas en `product-service` afecten a `inventory-service`.

- Comunicación asíncrona (Planeado, no implementado):
La idea era que `product-service` publicara un evento a AWS SQS al crear un nuevo producto, y `inventory-service` consumiera ese evento para crear automáticamente el inventario correspondiente.
Esto permitiría desacoplar los servicios y procesar eventos de forma eventual.


<br> <!-- Salto de línea -->
## ⚙️ Decisiones técnicas y justificaciones

- **Base de datos (PostgreSQL por microservicio):** Se eligió PostgreSQL por ser una base de datos relacional robusta, ampliamente adoptada, con soporte avanzado para integridad referencial y transacciones. Además, cada microservicio tiene su propia base de datos (Database per Service) para garantizar un mayor desacoplamiento, escalabilidad y evitar dependencias directas a nivel de datos entre servicios.
- **Comunicación síncrona usando WebClient:** Se optó por una llamada HTTP REST síncrona entre `inventory-service` y `product-service` para resolver solicitudes en tiempo real (en este caso, consultar información actualizada del producto). Se eligió WebClient por su naturaleza reactiva, ligera y no bloqueante, mejorando el rendimiento y escalabilidad
- **Registros atómicos y manejo transaccional:** Al registrar un movimiento de inventario (compra o venta) y actualizar el stock, se configuró la operación como transaccional. Esto asegura que las operaciones se realicen de forma atómica, manteniendo la consistencia de los datos incluso ante fallos parciales

- **Manejador global de excepciones:** Se creó un handler global que captura errores controlados y lanza respuestas claras al cliente. Sse definieron excepciones personalizadas que son lanzadas desde la lógica de negocio ante casos esperados (como no existencia de un producto, datos inválidos, etc.), permitiendo separar la gestión de errores de la lógica principal.


### Flujo de compra (justificación de no implementarlo):
Se consideró que un flujo de compra completo correspondería a un microservicio dedicado de órdenes o compras, siguiendo el principio de responsabilidad única y evitando un alto acoplamiento.
En lugar de esto, se implementó en `inventory-service` un **flujo de movimientos** (SALE o PURCHASE) que permite registrar salidas o ingresos de stock. La petición recibe el ID del producto, la cantidad y el tipo de movimiento; en el caso de venta se descuenta del stock y en compra se suma, validando siempre que los valores sean positivos.
- **Circuit breaker (Resilience4j):** Se implementó un circuit breaker usando Resilience4j para proteger el `inventory-service` de fallas o latencias excesivas al consumir el `product-service`. Este patrón gestiona reintentos, fallback y timeout, evitando fallos en cascada y mejorando la resiliencia general del sistema.





<br> <!-- Salto de línea -->
## 🛒 Explicación del flujo de compra implementado

<br> <!-- Salto de línea -->
## 📡 Endpoints

<br> <!-- Salto de línea -->
## 📄 Documentación de endpoints

<br> <!-- Salto de línea -->
## 🚨 Manejo de Excepciones

<br> <!-- Salto de línea -->
## 🧪 Pruebas

- Test Containers Prueba unitarias y de integracion

<br> <!-- Salto de línea -->
## 🤖 Documentación sobre el uso de herramientas de IA






