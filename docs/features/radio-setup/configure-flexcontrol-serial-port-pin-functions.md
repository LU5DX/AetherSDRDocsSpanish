# Configurar las funciones de los pines del puerto serie de FlexControl

Esta página explica cómo asignar funciones a los pines de salida DTR y RTS — y configurar los pines de entrada CTS y DSR — en el puerto serie utilizado por la interfaz de hardware FlexControl. Úsela cuando necesite que AetherSDR controle PTT, manipulación u otras señales a través de las líneas de control de un puerto serie.

## Antes de comenzar

- AetherSDR debe compilarse con soporte para puerto serie (`HAVE_SERIALPORT`). Si la pestaña Serial no aparece en Radio Setup, su versión no incluye esta función.
- La radio debe estar conectada. Radio Setup requiere una conexión activa con la radio.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...`. Esto abre el cuadro de diálogo Radio Setup directamente en la pestaña **Serial**. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el combo **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a escanear si el puerto no aparece. También puede escribir la ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los combos **Baud**, **Data**, **Parity** y **Stop** para que coincidan con su hardware.
4. En la fila DTR, establezca el combo **Function** con la función de señal deseada para el pin DTR y, a continuación, configure el combo **Polarity** con la polaridad correcta.
5. En la fila RTS, establezca el combo **Function** con la función de señal deseada para el pin RTS y, a continuación, configure el combo **Polarity** con la polaridad correcta.
6. Si el cableado de su paddle invierte el dit y el dah, marque **Paddle Swap (swap dit/dah)**.
7. Si desea que el puerto se abra automáticamente cada vez que AetherSDR inicie, marque **Auto-open serial port on startup**.
8. En la sección **FlexControl Tuning Knob**, haga clic en **Detect** para detectar el control giratorio FlexControl en el puerto seleccionado, o en **Close** para liberarlo.
9. Si desea que el control giratorio FlexControl se detecte automáticamente al iniciar, marque **Auto-detect on startup**. Para invertir la dirección de sintonía del control giratorio, marque **Invert tuning direction**.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Port** / **Refresh** / **Path** | Combo | Selecciona el dispositivo serie. Refresh vuelve a escanear los puertos disponibles. Path permite introducir la ruta directamente como texto. |
| **Baud** / **Data** / **Parity** / **Stop** | Combos | Establecen los parámetros de la línea serie para que coincidan con el hardware conectado. |
| **DTR: Function** / **Polarity** | Combos | Asignan la función de señal y la polaridad activa para el pin de salida DTR. |
| **RTS: Function** / **Polarity** | Combos | Asignan la función de señal y la polaridad activa para el pin de salida RTS. |
| **Paddle Swap (swap dit/dah)** | Casilla | Intercambia el dit y el dah en la entrada del paddle. |
| **Auto-open serial port on startup** | Casilla | Reabre el puerto serie configurado automáticamente al iniciar AetherSDR. |
| **FlexControl Tuning Knob: Detect** | Botón | Intenta detectar un control giratorio FlexControl en el puerto actualmente seleccionado. |
| **FlexControl Tuning Knob: Close** | Botón | Libera la conexión con el control giratorio FlexControl. |
| **Auto-detect on startup** | Casilla | Detecta automáticamente el control giratorio FlexControl al iniciar AetherSDR. |
| **Invert tuning direction** | Casilla | Invierte la dirección de sintonía de frecuencia del control giratorio FlexControl. |

## Solución de problemas

- **La pestaña Serial no aparece en Radio Setup** — AetherSDR no se compiló con `HAVE_SERIALPORT`. Utilice una versión que incluya soporte para puerto serie.
- **El puerto no aparece en la lista Port** — Haga clic en **Refresh** para volver a escanear. Confirme que el dispositivo esté físicamente conectado y que su cuenta de usuario tenga permiso para acceder al puerto (en Linux, esto normalmente requiere pertenecer al grupo `dialout` o `tty`).
- **El control giratorio FlexControl no se detecta** — Confirme que el puerto correcto está seleccionado y haga clic en **Detect** nuevamente. Verifique que ninguna otra aplicación tenga el puerto abierto.

## Temas relacionados

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Descripción general de Radio Setup](overview.md)
