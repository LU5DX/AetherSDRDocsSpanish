# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir la referencia de frecuencia de su FLEX-8600 mediante los controles de calibración integrados. Una calibración de frecuencia precisa reduce el error de dial en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX en Radio Setup solo está disponible cuando hay una conexión de radio activa.
- Si hay un GPSDO instalado, los controles de calibración siguen disponibles. Sin un GPSDO, se muestra un mensaje de estado en amarillo en lugar de la confirmación verde del GPSDO.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia de precisión conocida.
4. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** y aparece un mensaje de estado mientras se ejecuta el barrido. El botón **Start** permanece deshabilitado hasta que el barrido finalice o falle.
5. Cuando el barrido concluya, revise el desplazamiento medido que se muestra en **Freq Offset (ppb):**.
6. Si prefiere establecer el desplazamiento manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Configúrela con una señal de precisión conocida — por ejemplo, una emisora de frecuencia estándar de radiodifusión. El campo no debe estar vacío antes de hacer clic en **Start**; si está vacío, se muestra una advertencia y el barrido no se inicia. |
| **Start** | Botón | Inicia el barrido de calibración a la frecuencia ingresada en **Cal Frequency (MHz):**. Antes de iniciar, AetherSDR restablece el error de frecuencia actual a cero (`freq_error_ppb=0`) para que el barrido comience desde una línea base limpia. El botón se deshabilita y muestra **Busy** mientras el barrido está en curso. |
| **Freq Offset (ppb):** | Spinbox | El desplazamiento de frecuencia aplicado al oscilador de referencia del radio, en partes por mil millones. Puede ser establecido por el barrido o ingresado manualmente. |
| **10 MHz Reference Source:** | Combo box | Selecciona la fuente de referencia del oscilador. Valores válidos: `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. Un indicador de estado de enganche en tiempo real (Locked / Unlocked) aparece junto al combo box. |
| **TX Follows Active Slice** | Botón | TX sigue al slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Control deslizante | Establece la nitidez del filtro (0 = menor latencia hasta 3 = mayor nitidez) por modo. El control se deshabilita cuando **Auto** está habilitado para ese modo. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón alternante | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere manipulación desde el cliente. Si el campo de IP está vacío y el radio ya descubrió el TGXL, la IP descubierta se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Mensajes de estado de calibración

A partir de la v0.9.2.1, aparece una etiqueta de estado junto al botón **Start** que se actualiza durante todo el barrido.

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul grisáceo | La secuencia de comandos de calibración ha sido enviada al radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese una frecuencia e intente de nuevo. |
| Busy | — | Se muestra en el propio botón **Start** mientras hay un barrido en curso. |

## Banner de estado del GPSDO

El banner en la parte superior del grupo de calibración indica si hay un GPSDO instalado:

- **Banner verde** — El GPSDO está instalado. La calibración manual del desplazamiento de frecuencia sigue disponible.
- **Banner ámbar** — No hay GPSDO instalado. La calibración manual del desplazamiento de frecuencia está disponible.

En la v0.9.2.1 el texto del banner verde cambió. Anteriormente decía "GPSDO is installed. Frequency error correction is not required." Ahora dice "GPSDO installed. Manual frequency offset calibration available." Esto hace que el comportamiento sea coherente: los controles de calibración se muestran siempre independientemente de la presencia del GPSDO.

## Consejos

- Si tiene la intención de usar una referencia externa de 10 MHz en lugar del GPSDO, configure **10 MHz Reference Source:** en `External` antes de calibrar, para que el desplazamiento se aplique a la fuente correcta.
- El barrido restablece `freq_error_ppb` a cero antes de iniciar. Si tiene un desplazamiento ingresado manualmente que desea conservar, anótelo antes de hacer clic en **Start**.

## Relacionados

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
