# 🐳 Docker Cheatsheet

Comandos genéricos de Docker organizados por categoría.
Los valores entre `< >` se reemplazan según tu proyecto.

---

## 📦 Contenedores

### Listar contenedores
```bash
docker ps         # solo los que están corriendo
docker ps -a      # todos, incluyendo los detenidos
```
| Flag | Qué hace |
|------|----------|
| `-a` | Muestra todos los contenedores, no solo los activos |

---

### Iniciar / Detener
```bash
docker start <nombre_contenedor>
docker stop <nombre_contenedor>
```
- `start` → levanta un contenedor que ya existe pero está detenido
- `stop` → lo detiene de forma limpia (espera que termine sus procesos)

---

### Eliminar contenedor
```bash
docker rm -f <nombre_contenedor>
```
| Parte | Qué hace |
|-------|----------|
| `docker rm` | Elimina un contenedor detenido |
| `-f` | Fuerza la eliminación aunque esté corriendo (force) |
| `<nombre_contenedor>` | Nombre o ID del contenedor a eliminar |

> ⚠️ Con `-f` no pide confirmación, el contenedor desaparece de inmediato.

---

### Ver logs
```bash
docker logs <nombre_contenedor>
docker logs -f <nombre_contenedor>
```
| Flag | Qué hace |
|------|----------|
| `-f` | Sigue los logs en tiempo real (follow), como `tail -f` |

---

### Entrar a un contenedor
```bash
docker exec -it <nombre_contenedor> bash
docker exec -it <nombre_contenedor> sh   # si no tiene bash
```
| Flag | Qué hace |
|------|----------|
| `-i` | Modo interactivo (mantiene stdin abierto) |
| `-t` | Asigna una terminal (TTY) |

---

## 🗄️ Volúmenes

### Listar volúmenes
```bash
docker volume ls
```

---

### Eliminar volumen
```bash
docker volume rm <nombre_volumen>
```
| Parte | Qué hace |
|-------|----------|
| `docker volume rm` | Elimina el volumen y todos los datos que contiene |
| `<nombre_volumen>` | Nombre exacto del volumen (ver con `docker volume ls`) |

> ⚠️ Los datos del volumen se pierden permanentemente. Úsalo para limpiar configuraciones viejas o resets de entorno.

---

### Eliminar volúmenes huérfanos
```bash
docker volume prune
```
Elimina todos los volúmenes que no están siendo usados por ningún contenedor.

---

## 🖼️ Imágenes

### Listar imágenes
```bash
docker images
```

### Eliminar imagen
```bash
docker rmi <nombre_imagen>:<tag>
```
> Si no especificas `:<tag>`, asume `latest`.

---

## 🧹 Limpieza general

### Limpiar todo lo que no se usa
```bash
docker system prune
docker system prune -a    # incluye imágenes no usadas
```
| Flag | Qué hace |
|------|----------|
| `-a` | Elimina también imágenes que no tienen contenedores asociados |

> Útil para liberar espacio en disco después de varios labs.

---

## 🔌 Redes

### Listar redes
```bash
docker network ls
```

### Inspeccionar una red
```bash
docker network inspect <nombre_red>
```
Muestra qué contenedores están conectados y su configuración IP.

---

## ℹ️ Inspección general

### Ver detalles de cualquier objeto Docker
```bash
docker inspect <nombre_contenedor_o_volumen_o_imagen>
```
Devuelve un JSON con toda la configuración. Útil para debuggear.

---

*Para comandos específicos de cada lab, ver el README de cada proyecto.*
