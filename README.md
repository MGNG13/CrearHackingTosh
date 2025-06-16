# 🍏 Crear HackingTosh

> ⚠️ **Este repositorio está diseñado exclusivamente para preparar desde Windows los archivos necesarios para crear un Hackintosh.**
> 
> - Solo se ha probado con procesadores **Intel**. No se garantiza compatibilidad con otras arquitecturas o GPUs.
> - Esta guía es un **registro personal de configuración**, **no** un tutorial universal para todos los dispositivos.

---

## 🧩 Basado en la siguiente configuración de hardware

![Perfil actual](https://github.com/MGNG13/CrearHackingTosh/blob/main/components.png?raw=true)

---

## ✅ Requisitos Previos

Antes de comenzar, asegúrate de descargar lo siguiente:

1. 📦 [Repositorio OpCore-Simplify](https://github.com/lzhoang2801/OpCore-Simplify)
2. 🧰 [Release (.zip) de OpenCore](https://github.com/acidanthera/OpenCorePkg)
3. 🛠️ [Repositorio SSDTTime](https://github.com/corpnewt/SSDTTime) – Para extraer las tablas ACPI, ya que OpCore-Simplify **a veces no** puede generarlas correctamente.

---

## 🪜 Pasos Iniciales

Sigue todos los pasos del repositorio **OpCore-Simplify** hasta llegar a la sección de **`ACPI Tables`**.

📌 Si obtienes un resultado como este, puedes continuar. Si **no** obtienes este resultado, sigue los pasos alternativos a continuación:

![Resultado esperado](https://camo.githubusercontent.com/260cdc2dd9586fd9bf8ee125d88855967b692e9ec844d5d41f0ecd6bf117a0f0/68747470733a2f2f692e696d6775722e636f6d2f53624c364e36762e706e67)

---

### ❌ Error: `cygwin1.dll` – Tablas ACPI no encontradas

- Este error indica que **no se pudieron generar las tablas ACPI** correctamente.
  
![cygwin1.dll](https://github.com/MGNG13/CrearHackingTosh/blob/main/cygwin.png?raw=true)  
![No valid .aml files were found!](https://github.com/MGNG13/CrearHackingTosh/blob/main/aml_not_found.png?raw=true)

#### ✅ Solución con SSDTTime

Usaremos SSDTTime junto con herramientas oficiales de Intel para extraer correctamente las tablas ACPI:

![ssdttime](https://github.com/MGNG13/CrearHackingTosh/blob/main/ssdttime.png?raw=true)

1. Ejecuta SSDTTime y presiona `P` para generar las tablas. Se guardarán en el directorio `results`.

![Generar tablas](https://github.com/MGNG13/CrearHackingTosh/blob/main/tables_0.png?raw=true)

2. Las tablas generadas deben verse así:

![Tablas generadas](https://github.com/MGNG13/CrearHackingTosh/blob/main/tables_1.png?raw=true)

---

## 📥 Integrar tablas ACPI en OpCore-Simplify

Copia y pega la ruta de tus tablas generadas por SSDTTime dentro de OpCore-Simplify:

![Paso 1](https://github.com/MGNG13/CrearHackingTosh/blob/main/drag_n_drop_acpi_tables.png?raw=true)  
![Paso 2](https://github.com/MGNG13/CrearHackingTosh/blob/main/ready_drag_n_drop.png?raw=true)

---

## 🛠️ Personalizar y construir EFI

En esta etapa puedes:

- Ajustar los **Kexts** para que coincidan con tu hardware.
- (Opcional) Personalizar los parches **ACPI** y **SMBIOS** (aunque lo recomendado es dejar que OpCore-Simplify lo genere automáticamente con base en tu CPU).

🔧 Al finalizar, se generará tu carpeta **EFI** lista para arrancar tu Hackintosh.

![Construcción de EFI](https://github.com/MGNG13/CrearHackingTosh/blob/main/pre_build.png?raw=true)

📝 *Hasta este punto, ya deberías tener tus tablas ACPI y la carpeta EFI generadas correctamente.*

---

## 💽 Descargar la imagen de macOS

Usa el script `macrecovery.py` incluido en OpenCore para descargar la imagen de macOS:

📂 Ruta: `OpenCore-{version}-RELEASE\Utilities\macrecovery\macrecovery.py`

![macrecovery1](https://github.com/MGNG13/CrearHackingTosh/blob/main/macrecover1.png?raw=true)  
![macrecovery2](https://github.com/MGNG13/CrearHackingTosh/blob/main/macrecover2.png?raw=true)

🧷 **Estructura del USB recomendada**:

- Solo necesitas copiar el folder `com.apple.recovery.boot` desde el resultado del `macrecovery`.
- Copia también tu carpeta **EFI** generada desde `Results\EFI` de OpCore-Simplify.

📌 Resultado esperado:

![Referencia](https://dortania.github.io/OpenCore-Install-Guide/assets/img/com-efi-done.a6fb730e.png)

---

## 🧩 ¿macOS no arranca sin USB?

Una solución temporal es:

1. Crear una partición FAT32 en el disco duro (de ~500 MB).
2. Copiar los mismos archivos que hay en el USB a esa partición.
   
⚠️ No es la solución ideal, pero puede funcionar como bootloader de emergencia.

📺 Referencias:

<a href="https://www.youtube.com/watch?v=rZ1iPYfB6Pk&t=137s"><img src="https://i3.ytimg.com/vi/rZ1iPYfB6Pk/maxresdefault.jpg" alt="1"></img></a>
<a href="https://www.youtube.com/watch?v=lpYMluGQTXY"><img src="https://i3.ytimg.com/vi/lpYMluGQTXY/maxresdefault.jpg" alt="2"></img></a>

---

## NOTAS

#### iGPU 7MB/4MB

Si cuentas con problemas de GPU como Glitch de preferencia en los boot-args usa `-igfxvesa` para desactivar este glitch y posteriormente editar con Hakintool en la seccion de Patch seleccionas la generación de tu procesador y en `platform-id` buscas el tipo de dispositivo dependiendo si es laptop, desktop o desktop tipo NUC. En patch seleccionas `Graphic Device` y si tienes problemas con tu configuración puedes directamente también seleccionar `Audio Device` y `PCI Devices` para que genere la configuración correcta de tu Patch de `DeviceProperties`.

Si no te carga la pantalla después de esto o tienes un glitch esto ya no es directamente algo que tenga que ver con la configuración generada. Si tiene relación pero no siempre.

---

## 🧠 Recomendación final

🔗 **Lee la documentación oficial de Dortania mientras realizas tu configuración.** Te ayudará a:

- Ajustar correctamente tu configuración EFI.
- Finalizar la instalación de macOS.
- Resolver errores comunes (Bluetooth, Wi-Fi, gráficos, etc.).

📘 [Guía oficial de instalación de OpenCore – Dortania](https://dortania.github.io/OpenCore-Install-Guide/)
