# Crear HackingTosh

> *Este repositorio esta pensado solo para instalar desde Windows los datos necesarios para crear la Hackingtosh. Solo tiene soporte probado para procesador Intel, no se ha probado si funciona con otros procesadores y otras GPU.*
>
> ***Solo es un repositorio de documentado personal de Hackingtosh, no es un tutorial exacto para todos los dispositivos.***

## *Repositorio basado en esta configuración*
![Perfil actual](https://github.com/MGNG13/CrearHackingTosh/blob/main/components.png?raw=true)

---

## Pre-requisitos
1. Descargar el repo de <a href="https://github.com/lzhoang2801/OpCore-Simplify">OpCore-Simplify</a>
2. Descargar el release .zip de <a href="https://github.com/acidanthera/OpenCorePkg">OpenCore</a>
3. Descargar el repo de <a href="https://github.com/corpnewt/SSDTTime">SSDTTime</a> (Para extraer las ACPI Tables debido a que OpCore-Simplify no puede generarlas y marca errores.)

## Pasos
**Sigue todos los pasos de OpCore-Simplify hasta la sección de las `ACPI Tables`**

Si no te aparece este mismo resultado o algo similar sigue los siguientes pasos, de lo contrario salta este paso.

![Resultado esperado](https://camo.githubusercontent.com/260cdc2dd9586fd9bf8ee125d88855967b692e9ec844d5d41f0ecd6bf117a0f0/68747470733a2f2f692e696d6775722e636f6d2f53624c364e36762e706e67)

### Error: cygwin1.dll -> ACPI Tables no encontradas
![cygwin1.dll](https://github.com/MGNG13/CrearHackingTosh/blob/main/cygwin.png?raw=true)
![No valid .aml files were found!](https://github.com/MGNG13/CrearHackingTosh/blob/main/aml_not_found.png?raw=true)

Para este momento vamos a usar SSDTTime para poder extraer ACPI Tables de forma correcta con una herramienta que provee Intel para extraer estas tablas de forma correcta.

![ssdttime](https://github.com/MGNG13/CrearHackingTosh/blob/main/ssdttime.png?raw=true)

1. En este punto debemos seleccionar P para generar las tablas y guardarlas en `results` de SSDTTime.
![ssdttime_generar_tablas](https://github.com/MGNG13/CrearHackingTosh/blob/main/tables_0.png?raw=true)

2. Ya una vez generado se mostrará algo así.
![ssdttime_tablas_generadas](https://github.com/MGNG13/CrearHackingTosh/blob/main/tables_1.png?raw=true)

### Ingresar tablas en OpCore-Simplify
En este paso simplemente debemos de pegar la ruta de nuestras tablas generadas por SSDTTime.
![paso_1](https://github.com/MGNG13/CrearHackingTosh/blob/main/drag_n_drop_acpi_tables.png?raw=true)
![paso_2](https://github.com/MGNG13/CrearHackingTosh/blob/main/ready_drag_n_drop.png?raw=true)

### OpCore-Simplify Build OpenCore EFI
En este paso simplemente necesitamos customizar los Kexts que son los que nos van a permitir que todo funcione correctamente basado en nuestra computadora. También podemos customizar los ACPI Patch y SMBIOS (este no se recomienda ya que OpCore Simplified lo adapta basado en nuestro procesador).

**Al final de todo esto vamos a construir nuestra EFI de OpCore-Simplify para que funcione correctamente nuestra hackingtosh.**

![Build](https://github.com/MGNG13/CrearHackingTosh/blob/main/pre_build.png?raw=true)

<mark>Hasta este punto tenemos las ACPI Tables generadas por SSDTTime y la EFI de nuestro MacOS.</mark>

