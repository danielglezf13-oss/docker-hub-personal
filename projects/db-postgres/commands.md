# 🐳 Fortigate Inventory — Referencia de comandos

Comandos usados en este lab con explicación detallada de cada parte.

---

## `docker rm -f <nombre_contenedor>`

Elimina un contenedor existente.

```powershell
docker rm -f <nombre_contenedor>
```

| Parte                  | Qué hace                                                    |
|------------------------|-------------------------------------------------------------|
| `docker rm`            | Elimina un contenedor detenido                              |
| `-f`                   | Fuerza la eliminación aunque el contenedor esté corriendo   |
| `<nombre_contenedor>`  | Nombre del contenedor a eliminar                            |

> ⚠️ No pide confirmación. El contenedor desaparece de inmediato junto con sus datos internos.  
> Los datos guardados en volúmenes **no** se eliminan con este comando.

---

## `docker volume rm <nombre_volumen>`

Elimina un volumen y todos los datos que contiene.

```powershell
docker volume rm <nombre_volumen>
```

| Parte                | Qué hace                                                    |
|----------------------|-------------------------------------------------------------|
| `docker volume rm`   | Elimina el volumen especificado                             |
| `<nombre_volumen>`   | Nombre del volumen a eliminar (ver con `docker volume ls`)  |

> ⚠️ Los datos del volumen se pierden permanentemente.  
> Úsalo cuando quieras hacer un reset limpio del entorno.

---

## `docker run` — Crear el contenedor

Crea y levanta un nuevo contenedor con la configuración del proyecto.

```powershell
docker run -d `
  --name <nombre_contenedor> `
  -p 5432:5432 `
  -e POSTGRES_DB=<nombre_base_de_datos> `
  -e POSTGRES_USER=<usuario> `
  -e POSTGRES_PASSWORD=<contraseña> `
  -v <nombre_volumen>:/var/lib/postgresql `
  postgres:latest
```

| Parte                            | Qué hace                                                                 |
|----------------------------------|--------------------------------------------------------------------------|
| `docker run`                     | Crea y arranca un contenedor nuevo                                       |
| `-d`                             | Modo detached — corre en segundo plano, no bloquea la terminal           |
| `--name <nombre_contenedor>`             | Asigna un nombre al contenedor para referenciarlo fácilmente             |
| `-p 5432:5432`                   | Mapea el puerto: `<puerto_tu_máquina>:<puerto_del_contenedor>`           |
| `-e POSTGRES_DB=<nombre_base_de_datos>`   | Variable de entorno — nombre de la base de datos a crear automáticamente |
| `-e POSTGRES_USER=<usuario>`              | Variable de entorno — usuario de PostgreSQL                              |
| `-e POSTGRES_PASSWORD=<contraseña>`       | Variable de entorno — contraseña del usuario                             |
| `-v <nombre_volumen>:/var/lib/postgresql` | Monta un volumen para persistir los datos fuera del contenedor   |
| `postgres:latest`                | Imagen base a usar — PostgreSQL en su versión más reciente               |

> 💡 `-e` viene de *environment*. Cada flag `-e` define una variable de entorno dentro del contenedor.  
> 💡 Sin `-v`, al eliminar el contenedor perderías todos los datos de la base.

---

## `docker exec -it <nombre_contenedor> psql -U <usuario> -d <base_de_datos>`

Entra a la consola interactiva de PostgreSQL dentro del contenedor.

```powershell
docker exec -it <nombre_contenedor> psql -U <usuario> -d <nombre_base_de_datos>
```

| Parte                    | Qué hace                                                          |
|--------------------------|-------------------------------------------------------------------|
| `docker exec`            | Ejecuta un comando dentro de un contenedor que ya está corriendo  |
| `-i`                     | Modo interactivo — mantiene la entrada estándar abierta           |
| `-t`                     | Asigna una terminal (TTY) para poder escribir comandos            |
| `<nombre_contenedor>`    | Nombre del contenedor donde ejecutar el comando                   |
| `psql`                   | Cliente de línea de comandos de PostgreSQL                        |
| `-U <usuario>`           | Usuario con el que conectarse a PostgreSQL                        |
| `-d <nombre_base_de_datos>` | Base de datos a la que conectarse directamente                 |

> 💡 `-it` casi siempre van juntos cuando quieres una sesión interactiva.  
> El prompt cambia a `<nombre_base_de_datos>=>` cuando la conexión es exitosa.

---

## Comandos dentro de PostgreSQL (`psql`)

Estos no son comandos de Docker, sino del cliente `psql` de PostgreSQL.

| Comando | Qué hace                                              |
|---------|-------------------------------------------------------|
| `\dt`   | Lista todas las tablas del esquema actual             |
| `\l`    | Lista todas las bases de datos disponibles            |
| `\du`   | Lista todos los usuarios/roles de PostgreSQL          |
| `\q`    | Cierra la sesión y regresa a la terminal normal       |
