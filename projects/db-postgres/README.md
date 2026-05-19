# 🛡️ Fortigate Inventory — Docker Lab

Este lab levanta un contenedor de **PostgreSQL** que sirve como base de datos para el proyecto de inventario de dispositivos Fortigate.

La base de datos almacena la información de los equipos de red (nombre, IP, token de acceso y estado), permitiendo hacer altas, bajas y ediciones desde la aplicación.

---

## ¿Qué se levanta?

| Componente   | Detalle                        |
|--------------|--------------------------------|
| Contenedor   | PostgreSQL (`postgres:latest`) |
| Puerto       | `5432`                         |
| Volumen      | Persiste los datos entre reinicios del contenedor |

---

## Archivos de este lab

| Archivo          | Descripción                                                  |
|------------------|--------------------------------------------------------------|
| `setup.md`       | Guía paso a paso para levantar el entorno desde cero        |
| `commands.md`    | Referencia detallada de cada comando usado y sus flags      |

---

## Inicio rápido

Si es la primera vez, ve directo a [`setup.md`](./setup.md) y sigue los pasos en orden.

Si ya tienes el entorno levantado y solo necesitas consultar un comando, ve a [`commands.md`](./commands.md).
