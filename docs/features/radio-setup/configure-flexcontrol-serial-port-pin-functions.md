# Configurar las funciones de los pines del puerto serie de FlexControl

Esta página explica cómo asignar funciones a los pines de salida DTR y RTS en una conexión de puerto serie de FlexControl. Use estas configuraciones para controlar dispositivos externos, como un manipulador CW o una línea PTT, mediante las señales de control del puerto serie.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte para puerto serie (`HAVE_SERIALPORT`). Si la pestaña Serial no es visible en Radio Setup, su versión no incluye esta función.
- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...`. Esto abre el diálogo Radio Setup directamente en la pestaña **Serial**. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo de puerto serie. Haga clic en **Refresh** si su puerto no aparece en la lista, o escriba la ruta directamente en el campo **Path**.
3. Configure **Baud**, **Data**, **Parity** y **Stop** para que coincidan con el dispositivo conectado al puerto serie.
4. En la fila **DTR**, abra el cuadro combinado **Function** y seleccione la función que desea que realice DTR. Luego configure el cuadro combinado **Polarity** para ese pin.
5. En la fila **RTS**, abra el cuadro combinado **Function** y seleccione la función que desea que realice RTS. Luego configure el cuadro combinado **Polarity** para ese pin.
6. Si utiliza un paddle y necesita intercambiar dit y dah, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto serie automáticamente cada vez que se inicia, marque **Auto-open serial port on startup**.
8. Si hay un mando de sintonía FlexControl conectado, haga clic en **Detect** para identificarlo. Haga clic en **Close** para liberarlo. Para detectar el mando automáticamente al iniciar, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Rango válido / notas |
|---|---|---|---|---|
| Port / Refresh / Path | Cuadro combinado | Selecciona o introduce manualmente la ruta del dispositivo serie. **Refresh** vuelve a escanear los puertos disponibles. | — | Depende del sistema |
| Baud / Data / Parity / Stop | Cuadros combinados | Parámetros de la línea serie. Deben coincidir con el dispositivo conectado. | — | — |
| DTR: Function | Cuadro combinado | Asigna la función que se activa en el pin de salida DTR. | — | Opciones según las capacidades del dispositivo |
| DTR: Polarity | Cuadro combinado | Establece la lógica activa en alto o activa en bajo para DTR. | — | — |
| RTS: Function | Cuadro combinado | Asigna la función que se activa en el pin de salida RTS. | — | Opciones según las capacidades del dispositivo |
| RTS: Polarity | Cuadro combinado | Establece la lógica activa en alto o activa en bajo para RTS. | — | — |
| Paddle Swap (swap dit/dah) | Casilla de verificación | Intercambia las entradas dit y dah de un paddle conectado. | Sin marcar | — |
| Auto-open serial port on startup | Casilla de verificación | Reabre el puerto configurado automáticamente cuando se inicia AetherSDR. | Sin marcar | — |
| FlexControl Tuning Knob: Detect | Botón | Detecta un mando FlexControl en el puerto seleccionado. | — | — |
| FlexControl Tuning Knob: Close | Botón | Libera el mando FlexControl. | — | — |
| Auto-detect on startup | Casilla de verificación | Detecta el mando FlexControl automáticamente al iniciar. | — | — |
| Invert tuning direction | Casilla de verificación | Invierte la dirección de rotación del mando de sintonía. | — | — |

## Solución de problemas

- **La pestaña Serial no aparece** — Su versión de AetherSDR no incluye `HAVE_SERIALPORT`. Instale u obtenga una versión que incluya soporte para puerto serie.
- **El puerto no aparece en la lista** — Haga clic en **Refresh**. Confirme que el dispositivo está conectado y que su cuenta de usuario del sistema operativo tiene permiso para acceder al puerto serie (en Linux, el usuario normalmente debe pertenecer al grupo `dialout`).
- **Las funciones de los pines no tienen efecto** — Confirme que la configuración de **Polarity** coincide con lo que espera el dispositivo conectado. Algunos dispositivos requieren lógica activa en bajo.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
