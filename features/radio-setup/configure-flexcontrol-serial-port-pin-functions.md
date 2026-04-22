# Configurar las funciones de los pines del puerto serie para FlexControl

Esta página explica cómo seleccionar un puerto serie para la interfaz de hardware FlexControl y asignar funciones y polaridad a los pines de salida DTR y RTS. Use estos ajustes al conectar un mando FlexControl o un paddle mediante un adaptador serie.

## Antes de comenzar

- AetherSDR debe compilarse con soporte para puerto serie. La pestaña Serial solo aparece cuando `HAVE_SERIALPORT` está habilitado. Si no ve una pestaña Serial en Radio Setup, su compilación no incluye esta función.
- Debe haber una conexión de radio activa. Radio Setup requiere una radio conectada.
- Identifique qué ruta de dispositivo serie corresponde a su FlexControl o adaptador serie (por ejemplo, `/dev/ttyUSB0` en Linux).

## Pasos

1. Abra `Settings > FlexControl...`. Esto abre el diálogo Radio Setup directamente en la pestaña Serial. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña Serial.
2. En la sección Port, haga clic en el combo box Port y seleccione su dispositivo serie de la lista. Si el dispositivo no aparece, haga clic en Refresh para volver a explorar. Para escribir una ruta directamente, edite el campo Path.
3. Configure los parámetros de la línea serie usando los combo boxes Baud, Data, Parity y Stop para que coincidan con su dispositivo.
4. En la fila DTR, abra el combo box Function y seleccione la función que desea asignar al pin DTR. Abra el combo box Polarity y seleccione la polaridad.
5. En la fila RTS, abra el combo box Function y seleccione la función para el pin RTS. Abra el combo box Polarity y seleccione la polaridad.
6. Si está conectando un paddle CW y necesita intercambiar dit y dah, active Paddle Swap (swap dit/dah).
7. Para que AetherSDR abra este puerto automáticamente cada vez que se inicie, active Auto-open serial port on startup.
8. En la sección FlexControl Tuning Knob, haga clic en Detect para confirmar que el mando es reconocido. Haga clic en Close para liberarlo.
9. Para que AetherSDR detecte el mando de sintonía automáticamente al arrancar, active Auto-detect on startup. Para invertir la dirección de sintonía, active Invert tuning direction.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Port / Refresh / Path | Combo box | Selecciona o especifica manualmente el dispositivo serie. Refresh vuelve a explorar los puertos disponibles. |
| Baud / Data / Parity / Stop | Combo boxes | Establece los parámetros de la línea serie para que coincidan con el dispositivo conectado. |
| DTR: Function / Polarity | Combo boxes | Asigna una función de señal y una polaridad activa al pin de salida DTR. |
| RTS: Function / Polarity | Combo boxes | Asigna una función de señal y una polaridad activa al pin de salida RTS. |
| Paddle Swap (swap dit/dah) | Casilla de verificación | Invierte las entradas de dit y dah del paddle conectado. |
| Auto-open serial port on startup | Casilla de verificación | Reabre el puerto configurado cada vez que AetherSDR se inicia. |
| FlexControl Tuning Knob: Detect / Close | Botones | Detect inicia el reconocimiento del mando FlexControl. Close libera la conexión con él. |
| Auto-detect on startup | Casilla de verificación | Detecta automáticamente el mando FlexControl cuando AetherSDR arranca. |
| Invert tuning direction | Casilla de verificación | Invierte la dirección del mando de sintonía. |

## Consejos

- Si abrió Radio Setup mediante `Settings > Radio Setup...` y la pestaña Serial no es visible, su compilación de AetherSDR no incluye soporte para `HAVE_SERIALPORT`.
- En Linux, las rutas de dispositivos serie suelen ser `/dev/ttyUSB0` o `/dev/ttyS0`. Es posible que su cuenta de usuario deba ser miembro del grupo `dialout` para acceder a estos dispositivos.

## Solución de problemas

- **La pestaña Serial no aparece en Radio Setup** — La pestaña solo se compila cuando `HAVE_SERIALPORT` está habilitado. Use una compilación que incluya soporte para puerto serie.
- **La lista de puertos está vacía** — No se encontraron dispositivos serie. Conecte el dispositivo y haga clic en Refresh para volver a explorar.
- **El mando FlexControl no se detecta después de hacer clic en Detect** — Verifique que el puerto y la velocidad en baudios correctos estén seleccionados y que el dispositivo esté físicamente conectado. Haga clic en Refresh en la lista de puertos e inténtelo de nuevo.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Descripción general de Radio Setup](overview.md)
