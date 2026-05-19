# 🛡️ Fortigate Inventory — Setup del entorno Docker

Guía paso a paso para levantar el contenedor de PostgreSQL usado en este proyecto.

---

## Prerequisitos

- Docker instalado y corriendo
- PowerShell (Windows) o terminal

---

## Paso 1 — Limpiar entorno anterior

> Omite este paso si es la primera vez que configuras el lab.

**Elimina el contenedor existente:**
```powershell
docker rm -f <nombre_contenedor>
```

**Elimina el volumen para borrar la configuración vieja:**
```powershell
docker volume rm postgres_data
```

---

## Paso 2 — Crear el contenedor

Ejecuta este comando completo en una sola línea:

```powershell
docker run -d `
  --name <nombre_contenedor> `
  -p 5432:5432 `
  -e POSTGRES_DB=<nombre_base_de_datos> `
  -e POSTGRES_USER=<usuario> `
  -e POSTGRES_PASSWORD=<contraseña> `
  -v postgres_data:/var/lib/postgresql `
  postgres:latest
```

### Equivalencia con el archivo de configuración del proyecto

| Parámetro en tu archivo | Variable en Docker       | Valor configurado         |
|-------------------------|--------------------------|---------------------------|
| `DB_HOST`               | (tu máquina local)       | `localhost`               |
| `DB_PORT`               | `-p 5432:5432`           | `5432`                    |
| `DB_NAME`               | `-e POSTGRES_DB`         | `<nombre_base_de_datos>`  |
| `DB_USER`               | `-e POSTGRES_USER`       | `<usuario>`               |
| `DB_PASS`               | `-e POSTGRES_PASSWORD`   | `<contraseña>`            |

> ⏳ Espera 10-15 segundos para que PostgreSQL termine de inicializar antes de continuar.

---

## Paso 3 — Conectarse a la base de datos

Al usar `-e POSTGRES_DB=<nombre_base_de_datos>`, Docker creó la base de datos automáticamente al arrancar.  
**No es necesario ejecutar `CREATE DATABASE`** — si lo intentas, PostgreSQL dará error porque ya existe.

Conéctate directamente:

```powershell
docker exec -it <nombre_contenedor> psql -U <usuario> -d <nombre_base_de_datos>
```

Sabrás que estás dentro porque el prompt cambiará a:
```
<nombre_base_de_datos>=>
```

---

## Paso 4 — Crear la tabla

> 💡 Cambia `<nombre_tabla>` por el nombre que necesites para tu proyecto.

Pega este bloque completo y presiona Enter:

```sql
CREATE TABLE public.<nombre_tabla> (
    id                   SERIAL PRIMARY KEY,
    nombre               CHARACTER VARYING(100) NOT NULL UNIQUE,
    ip                   CHARACTER VARYING(50) NOT NULL,
    token_cifrado        TEXT NOT NULL,
    activo               BOOLEAN DEFAULT TRUE,
    ultima_actualizacion TIMESTAMP WITHOUT TIME ZONE DEFAULT CURRENT_TIMESTAMP
);
```

Si todo salió bien, la terminal responde:
```
CREATE TABLE
```

### Descripción de columnas

| Columna               | Tipo          | Descripción                                      |
|-----------------------|---------------|--------------------------------------------------|
| `id`                  | SERIAL        | Identificador único, se incrementa automáticamente |
| `nombre`              | VARCHAR(100)  | Nombre del equipo, no puede repetirse            |
| `ip`                  | VARCHAR(50)   | Dirección IP del dispositivo, obligatoria        |
| `token_cifrado`       | TEXT          | Token o API Key del dispositivo                  |
| `activo`              | BOOLEAN       | Estado del equipo, `true` por defecto            |
| `ultima_actualizacion`| TIMESTAMP     | Fecha y hora de creación o último cambio         |

---

## Paso 5 — Verificar la tabla

Dentro de la consola de PostgreSQL ejecuta:

```sql
\dt
```

Deberías ver la tabla `equipos` listada.

---

## Paso 6 — Salir de PostgreSQL

```sql
\q
```

---

## ⚠️ Nota de seguridad

La columna `token_cifrado` está pensada para guardar tokens de FortiOS encriptados.  
Cuando conectes tu script de automatización (Python u otro), usa una librería como [`cryptography` (Fernet)](https://cryptography.io/en/latest/fernet/) para encriptar los tokens **antes** de insertarlos en la base de datos.
