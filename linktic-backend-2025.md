# 📦 Sistema de Gestión de Inventario

Sistema de gestión de inventario basado en **microservicios**, desarrollado en **Java 21** con **Spring Boot 3.5.3**.  
Permite registrar productos, consultar su inventario y registrar movimientos de stock

<br> <!-- Salto de línea -->
## Contenido



- [Funcionalidades Principales](#-funcionalidades-principales)
- [Tecnologías Utilizadas](#%EF%B8%8F-tecnologías-utilizadas)
- [Instalación y ejecución](#%EF%B8%8F-clonar-y-levantar-el-proyecto)
- [Descripción de la arquitectura y patrones](#%EF%B8%8F-clonar-y-levantar-el-proyecto)
- [Diagrama de interacción entre servicios](#%EF%B8%8F-clonar-y-levantar-el-proyecto)
- [Decisiones técnicas y justificaciones](#%EF%B8%8F-clonar-y-levantar-el-proyecto)
- [Explicación del flujo de compra implementado](#%EF%B8%8F-clonar-y-levantar-el-proyecto)
- [Endpoints](#-endpoints)
- [Documentacion de endpoints](#-ejemplos-de-request-body)
- [Manejo de Excepciones](#-manejo-de-excepciones)
- [Pruebas](#-pruebas)
- [Documentación sobre el uso de herramientas de IA](#%EF%B8%8F-clonar-y-levantar-el-proyecto)




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
- Manejo de timeouts y reintentos basicos
- 



<br> <!-- Salto de línea -->
## 🛠️ Tecnologías Utilizadas
## 📦 Instalación y ejecución
## 🏗️ Descripción de la arquitectura y patrones
## 🔄 Diagrama de interacción entre servicios
## ⚙️ Decisiones técnicas y justificaciones
## 🛒 Explicación del flujo de compra implementado
## 📡 Endpoints
## 📄 Documentación de endpoints
## 🚨 Manejo de Excepciones
## 🧪 Pruebas
## 🤖 Documentación sobre el uso de herramientas de IA






