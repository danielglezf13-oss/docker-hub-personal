# 🐳 Docker Knowledge Base & Labs

¡Bienvenido! Este repositorio es mi base de conocimientos centralizada sobre **Docker** y **Docker Compose**. Aquí documento desde comandos esenciales y guías de instalación en diferentes entornos, hasta arquitecturas de proyectos listos para ser desplegados.

El objetivo de este espacio es servir como guía de referencia rápida para administración de infraestructura, despliegue de contenedores y buenas prácticas de seguridad en entornos de virtualización ligera.

---

## 📁 Estructura del Repositorio

*   **`/docs`**: Guías de instalación detalladas (Linux, WSL2, etc.) y configuración de entornos.
*   **`/cheatsheets`**: Comandos rápidos para gestión de contenedores, imágenes, volúmenes y redes.
*   **`/projects`**: Laboratorios prácticos y archivos `docker-compose.yml` listos para levantar servicios.

---

## 🚀 Proyectos Incluidos

Aquí hay una lista de los despliegues documentados en este repo:
*   [Proxy Inverso con Nginx]('./projects/nginx-reverse-proxy') - Configuración e instalacion de Docker Windows.
*   [Entorno de Monitoreo]('./projects/monitoring-stack') - Recolección de métricas básicas de contenedores.
*(Puedes ir sumando tus proyectos de automatización, firewalls, bases de datos, etc.)*

---

## 🛠️ Comandos Esenciales (Cheat Sheet de Emergencia)

### Gestión de Contenedores
```bash
# Levantar servicios en segundo plano
docker compose up -d

# Limpieza total (Contenedores detenidos, redes e imágenes sin usar)
docker system prune -a --volumes
