# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar una referencia de reloj externa de 10 MHz en un FLEX-8600 conectado. Use una referencia externa cuando disponga de un oscilador disciplinado por GPS u otra fuente de precisión de 10 MHz y desee que el radio se sincronice con ella en lugar de con su oscilador interno.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Radio Setup requiere una conexión de radio activa.
- La señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel trasero del FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Localice el cuadro combinado `10 MHz Reference Source:`.
4. Seleccione `External` en el cuadro combinado. Para volver al oscilador interno, seleccione `Internal`.

## Qué hace cada control

| Control | Tipo | Rango válido |
|---|---|---|
| `10 MHz Reference Source:` | Cuadro combinado | `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de sincronización (Locked / Unlocked) se muestra junto al cuadro y se actualiza en tiempo real. |
| TX Follows Active Slice | Botón de presión | TX sigue al slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón de presión | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Deslizador (0–3) | Establece la nitidez del filtro (0=latencia mínima, 3=máxima nitidez) por modo; el deslizador se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Activa la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón de presión | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que fue rota en el firmware 4.2. Si el campo de IP está vacío y el radio ha detectado el TGXL, la IP detectada se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón de presión | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de presión | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Calibración de frecuencia (pestaña RX)

A partir de la v0.9.2.1, los controles de calibración de frecuencia en la pestaña `RX` son siempre visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (en verde). Cuando no hay GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (en ámbar). En versiones anteriores, los controles de calibración se ocultaban cuando se detectaba un GPSDO.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| `Cal Frequency (MHz):` | Campo de texto | Frecuencia utilizada para la calibración manual. Introduzca la frecuencia exacta de su señal de referencia en MHz. |
| `Start` | Botón de presión | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración. El botón se deshabilita y muestra "Busy" mientras la calibración está en progreso. Una etiqueta de estado junto al botón muestra el estado actual (Starting…, texto de progreso o resultado). El campo no debe estar vacío; si lo está, la etiqueta de estado le solicitará que introduzca una frecuencia antes de continuar. |
| `Freq Offset (ppb):` | Cuadro numérico | Desplazamiento de frecuencia manual en partes por mil millones. Ajústelo si necesita aplicar un desplazamiento conocido sin ejecutar el barrido de calibración automatizado. |

### Cómo ejecutar un barrido de calibración

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Introduzca la frecuencia exacta de su señal de referencia en el campo `Cal Frequency (MHz):`.
4. Haga clic en `Start`. El botón se deshabilita y muestra "Busy". Observe la etiqueta de estado para seguir el progreso.
5. Cuando finalice el barrido, la etiqueta de estado muestra el resultado y el botón `Start` se vuelve a habilitar.

## Consejos

- La pestaña `RX` también contiene el cuadro combinado `10 MHz Reference Source:`. Si está usando un oscilador disciplinado por GPS, cambie la fuente de referencia a `GPSDO` o `External` según corresponda antes de ejecutar la calibración.
- Si el campo `Cal Frequency (MHz):` está vacío al hacer clic en `Start`, la etiqueta de estado le solicitará que introduzca una frecuencia. En ese caso no se envía ningún comando al radio.

## Solución de problemas

- **La frecuencia del radio parece inestable o desplazada tras cambiar a External** — Es posible que la señal REF IN esté ausente, tenga un nivel demasiado bajo o no sea exactamente de 10 MHz. Verifique que la fuente externa esté funcionando y correctamente conectada antes de seleccionar `External`. Vuelva a `Internal` mientras realiza el diagnóstico.
- **El botón Start permanece deshabilitado o muestra "Busy" indefinidamente** — Esto puede ocurrir si el radio no responde al comando `radio pll_start`. Desconéctese y vuelva a conectarse al radio, luego inténtelo de nuevo.

## Relacionado

- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
