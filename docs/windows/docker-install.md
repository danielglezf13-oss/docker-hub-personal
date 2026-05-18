# [cite_start]Instalación de Docker en Windows [cite: 1]

[cite_start]Guía paso a paso para instalar y configurar Docker Desktop en entornos Windows utilizando WSL 2[cite: 1, 9, 16].

---

## [cite_start]Paso 1: Verificar los requisitos del sistema [cite: 2]

[cite_start]Antes de empezar, asegúrate de que tu computadora cumpla con los siguientes requisitos mínimos[cite: 3]:

* [cite_start]**Sistema Operativo:** Windows 10 (versión 21H2 o superior) o Windows 11 (Home, Pro, Enterprise o Education)[cite: 4].
* [cite_start]**Procesador:** Procesador de 64 bits con traducción de direcciones de segundo nivel (SLAT)[cite: 5].
* [cite_start]**RAM:** Mínimo 4 GB de memoria RAM[cite: 6].
* [cite_start]**BIOS:** La virtualización de hardware debe estar habilitada en la BIOS de tu computadora[cite: 7].

> 💡 **Tip de verificación:** Puedes comprobar la virtualización abriendo el **Administrador de tareas** -> pestaña **Rendimiento** -> sección **CPU**. [cite_start]Ahí deberías ver `Virtualización: Habilitada`[cite: 8].

[cite_start]![Verificación de Virtualización](images/virtualizacion.png)[cite: 8]

---

## [cite_start]Paso 2: Habilitar WSL 2 (Windows Subsystem for Linux) [cite: 9]

[cite_start]Docker Desktop en Windows funciona mejor si utiliza el motor de WSL 2[cite: 10]. [cite_start]Para instalarlo o actualizarlo sigue estos pasos[cite: 10]:

1. [cite_start]Abre la **Terminal de Windows** o el **Símbolo del sistema (CMD)** como **Administrador** (clic derecho -> *Ejecutar como administrador*)[cite: 11].
2. [cite_start]Ejecuta el siguiente comando y presiona `Enter`[cite: 12]:

```bash
wsl --install
[cite_start]
http://googleusercontent.com/immersive_entry_chip/0
http://googleusercontent.com/immersive_entry_chip/1
http://googleusercontent.com/immersive_entry_chip/2

### 📌 Consejo para las imágenes en Git:
[cite_start]En las etiquetas de imagen como `![Verificación de Virtualización](images/virtualizacion.png)`, crea una carpeta llamada `images` dentro de tu repositorio, mete ahí las capturas de pantalla de tu documento de Word y ponles el nombre correspondiente (ej. `virtualizacion.png`, `wsl_install.png`, etc.)[cite: 8, 13]. [cite_start]Al subir todo a Git, se verán idénticas a como las tenías en tu archivo original.
