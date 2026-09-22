# FinTech Nova - Plataforma de Microservicios 

Este repositorio contiene el código fuente y la infraestructura como código para la migración de la plataforma *FinTech Nova* hacia una arquitectura de microservicios políglota.

El objetivo principal de este proyecto es contenerizar múltiples servicios desarrollados en distintos lenguajes y orquestarlos de manera segura para su posterior despliegue en la nube (AWS EC2).

##  Arquitectura del Sistema

La solución está compuesta por los siguientes microservicios:

- **api-clientes**: API REST en Python (Flask) para la gestión de clientes.
- **api-pagos**: API REST en Node.js (Express) para el procesamiento de pagos.
- **api-facturas**: API en Java (Spring Boot) para la emisión de facturas.
- **api-tarjetas**: API en .NET para la validación y gestión de tarjetas.
- **api-transacciones**: API en Go para el registro de movimientos.
- **web**: Frontend (SPA) desarrollado con Vite, servido a través de NGINX.
- **db**: Base de datos central MariaDB compartida entre los servicios.

##  Estado Actual del Proyecto (Progreso)

Hasta el momento, hemos avanzado con las siguientes fases:

- [x] **Pruebas Locales**: Validación del correcto funcionamiento en entorno local de las APIs (`api-clientes` y `api-pagos`).
- [x] **Dockerización Inicial**: Creación de imágenes optimizadas (`Dockerfile`) y configuración de ignorados (`.dockerignore`) para los microservicios:
  - `api-clientes` (Python)
  - `api-pagos` (Node.js)
- [x] **Testeo de Contenedores**: Construcción y ejecución exitosa de los contenedores de forma aislada localmente.

##  Próximos Pasos (To-Do)

El desarrollo y despliegue continuará con las siguientes tareas:

1. **Dockerización Restante**:
   - Escribir los `Dockerfile` con estrategias de compiliación *multi-stage* para Java, Go, .NET y el Frontend.
2. **Orquestación con Docker Compose**:
   - Integrar todos los servicios en un `docker-compose.yml`.
   - Definir redes internas, dependencias de inicio (`depends_on`) y volúmenes persistentes para la base de datos.
3. **Seguridad y Proxy Inverso**:
   - Configurar el contenedor `web` (NGINX) como proxy inverso.
   - Implementar la generación dinámica de certificados TLS auto-firmados para asegurar que todo el tráfico expuesto sea estrictamente HTTPS (puerto 443).
4. **Despliegue en AWS (EC2)**:
   - Aprovisionamiento de la instancia EC2.
   - Creación de scripts de automatización (`deploy.sh`) para clonar, preparar y levantar el stack productivo en la nube.

