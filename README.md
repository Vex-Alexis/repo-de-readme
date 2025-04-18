# repo-de-readme


## Antes de Iniciar

Empezaremos por explicar los diferentes componentes del proyectos y partiremos de los componentes externos, continuando con los componentes core de negocio (dominio) y por último el inicio y configuración de la aplicación.

devsu-java/
├── cliente-service/            # Microservicio de clientes
│   ├── Dockerfile
│   └── ...
├── cuentas-service/           # Microservicio de cuentas
│   ├── Dockerfile
│   └── ...
├── docker-compose/            # Archivos de despliegue
│   ├── docker-compose.yml
│   └── db/
│       ├── 01_DataBase.sql    # Script de creación de tablas
│       └── 02_Populate.sql    # Script con datos de prueba
