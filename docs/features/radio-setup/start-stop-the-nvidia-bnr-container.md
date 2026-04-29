# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en inteligencia artificial al audio del micrófono. Use los controles de la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema de forma independiente a AetherSDR. AetherSDR lo controla, pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR arranque, haga clic en **Autostart Container** para activarlo.
5. Para iniciar el contenedor de inmediato, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin modificarlo, haga clic en **Check Status**. El indicador de estado de color junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control                                                    | Tipo       | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|------------------------------------------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Autostart Container**                                    | Botón      | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al arrancar.                                                                                                                                                                                                                                                                                                                                                            |
| **Start**                                                  | Botón      | Inicia el contenedor NVIDIA BNR de inmediato.                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Stop**                                                   | Botón      | Detiene un contenedor NVIDIA BNR en ejecución de inmediato.                                                                                                                                                                                                                                                                                                                                                                                           |
| **Check Status**                                           | Botón      | Consulta el estado del contenedor y actualiza el indicador de estado.                                                                                                                                                                                                                                                                                                                                                                                 |
| Indicador de estado NVIDIA BNR                             | Indicador  | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown.                                                                                                                                                                                                                                                                                                                                                                      |
| TX Follows Active Slice                                    | Botón      | TX sigue el slice (canal de recepción) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split.                                                                                                                                                                                                                                                                                     |
| Active Slice Follows TX                                    | Botón      | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**.                                                                                                                                                                                                                                                                                                                  |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia mínima a 3=máxima nitidez) por modo. El control deslizante se deshabilita cuando Auto está activo. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`.                                                                                                                                                                                                                                  |
| Auto (Voice / CW / Digital)                                | Botón      | Activa la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`.                                                                                                                                                                                                                                                      |
| Connect / Disconnect (TGXL)                                | Botón      | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que no funciona en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL)                                | Botón      | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`.                                                                                                                                                                                                                                                                                                |
| Connect / Disconnect (Antenna Genius)                      | Botón      | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`.                                                                                                                                                                                                                                                                                                                  |

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de frecuencia de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, cuando se detectaba un GPSDO, los campos de calibración se ocultaban y se reemplazaban con un mensaje indicando que no se requería corrección. La pestaña ahora siempre muestra el campo **Cal Frequency (MHz)** y el botón **Start**.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea durante toda la secuencia de calibración:

| Texto de estado  | Significado                                                                     |
|------------------|---------------------------------------------------------------------------------|
| Starting...      | AetherSDR ha enviado los comandos de calibración a la radio.                    |
| Busy             | El botón **Start** está deshabilitado; la calibración está en progreso.         |
| (texto de error) | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**.          |

Cuando el hardware GPSDO está presente, la etiqueta en la parte superior del grupo indica "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta indica "Manual frequency offset calibration available." (ámbar). En ambos casos, los controles debajo de la etiqueta funcionan de manera idéntica.

### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida con precisión en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no se inicia.
5. Haga clic en **Start**. La etiqueta del botón cambia a **Busy** y se deshabilita hasta que la secuencia de calibración se complete.
6. Observe la etiqueta de estado para seguir el progreso. Cuando la calibración finaliza, el botón se vuelve a habilitar y **Freq Offset (ppb)** refleja la corrección medida.

### Notas

- Hacer clic en **Start** restablece `freq_error_ppb` a 0 antes de iniciar el barrido, por lo que cualquier desplazamiento almacenado previamente se borra al inicio de cada ejecución.
- El estado de calibración se rastrea por instancia de diálogo. Cerrar y volver a abrir el diálogo restablece la pantalla de estado; cualquier calibración en progreso del lado de la radio continúa de forma independiente.

## Consejos

- Haga clic en **Check Status** después de hacer clic en **Start** o **Stop** si el indicador de estado no se actualiza por sí solo, para confirmar que el contenedor alcanzó el estado esperado.
- Si el botón **Start** permanece en el estado **Busy** tras una desconexión inesperada, cierre y vuelva a abrir `Settings > Radio Setup...` para restablecer el botón.

## Relacionado

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
