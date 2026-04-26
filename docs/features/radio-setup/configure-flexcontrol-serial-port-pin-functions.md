# Configurar las funciones de los pines del puerto serie para FlexControl

Esta página explica cómo seleccionar un puerto serie para el mando FlexControl y asignar funciones de señal a sus pines de hardware. Esto se hace para usar un mando de sintonía FlexControl con AetherSDR a través de una conexión serie, o para controlar las líneas PTT y de manipulación mediante los pines DTR y RTS del puerto serie.

## Antes de comenzar

- El radio debe estar conectado. La pestaña Serial solo está disponible cuando AetherSDR está conectado a un FLEX-8600.
- El soporte para puerto serie debe estar compilado en su versión de AetherSDR (`HAVE_SERIALPORT`). Si no ve `Settings > FlexControl...` en el menú, su versión no incluye soporte para puerto serie.
- El dispositivo serie debe estar físicamente conectado y visible para el sistema operativo antes de abrir el diálogo.

## Pasos

1. Haga clic en `Settings > FlexControl...`. Esto abre el diálogo Radio Setup directamente en la pestaña Serial. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Si el dispositivo no aparece, haga clic en **Refresh** para volver a escanear. También puede escribir una ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con su hardware.
4. Para cada pin de salida que desee configurar, localice la fila **DTR** o **RTS**, establezca el cuadro combinado **Function** en la función de señal deseada y luego establezca el cuadro combinado **Polarity** en la polaridad apropiada.
5. Si está usando un paddle con este puerto serie y necesita intercambiar dit y dah, marque **Paddle Swap (swap dit/dah)**.
6. Para que AetherSDR reabra este puerto automáticamente cada vez que inicie, marque **Auto-open serial port on startup**.
7. Para detectar un mando de sintonía FlexControl conectado, haga clic en **Detect** en la sección FlexControl Tuning Knob. Para liberar el puerto, haga clic en **Close**.
8. Para que el mando FlexControl se detecte automáticamente al inicio, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.
9. Haga clic en **Close** en la barra de botones del diálogo cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Port** | Cuadro combinado | Selecciona el dispositivo serie de la lista de puertos detectados. |
| **Refresh** | Botón | Vuelve a escanear los puertos serie disponibles y actualiza la lista **Port**. |
| **Path** | Campo | Muestra o reemplaza la ruta al dispositivo serie seleccionado. |
| **Baud** | Cuadro combinado | Establece la velocidad en baudios para la conexión serie. |
| **Data** | Cuadro combinado | Establece el número de bits de datos. |
| **Parity** | Cuadro combinado | Establece el modo de paridad. |
| **Stop** | Cuadro combinado | Establece el número de bits de parada. |
| **DTR: Function** | Cuadro combinado | Asigna la función de señal que transporta el pin DTR. |
| **DTR: Polarity** | Cuadro combinado | Establece la polaridad activa alta o activa baja para DTR. |
| **RTS: Function** | Cuadro combinado | Asigna la función de señal que transporta el pin RTS. |
| **RTS: Polarity** | Cuadro combinado | Establece la polaridad activa alta o activa baja para RTS. |
| **Paddle Swap (swap dit/dah)** | Casilla de verificación | Intercambia las entradas de dit y dah para el paddle conectado. |
| **Auto-open serial port on startup** | Casilla de verificación | Reabre este puerto serie automáticamente cuando AetherSDR se inicia. |
| **Detect** | Botón | Detecta un mando de sintonía FlexControl conectado en el puerto configurado. |
| **Close** | Botón | Libera la conexión con el mando FlexControl. |
| **Auto-detect on startup** | Casilla de verificación | Detecta automáticamente el mando FlexControl cuando AetherSDR inicia. |
| **Invert tuning direction** | Casilla de verificación | Invierte la dirección del cambio de frecuencia al girar el mando FlexControl. |

## Resolución de problemas

- **La pestaña Serial no aparece en Radio Setup** — Su versión de AetherSDR no incluye soporte para puerto serie (`HAVE_SERIALPORT`). Tampoco verá `Settings > FlexControl...` en el menú. Obtenga una versión que incluya esta función.
- **Su dispositivo no aparece en la lista Port** — Haga clic en **Refresh**. Si aún no aparece, confirme que el dispositivo está conectado y que el sistema operativo le ha asignado un puerto. En Linux, verifique que su cuenta de usuario tenga permiso para acceder al dispositivo (típicamente mediante membresía en el grupo `dialout`).
- **Detect no reporta ningún mando FlexControl** — Confirme que la velocidad en baudios y los parámetros serie coinciden con los requisitos del hardware FlexControl y que el puerto correcto está seleccionado antes de hacer clic en **Detect**.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
