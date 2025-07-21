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
  <img src="Captura de pantalla 2025-07-21 134814.png" alt="Arquitectura general" width="600"/>
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

<br> <!-- Salto de línea -->
## ⚙️ Decisiones técnicas y justificaciones

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






