# Configurar las funciones de los pines del puerto serie de FlexControl

Esta página explica cómo seleccionar y configurar el puerto serie utilizado por un dispositivo FlexControl, establecer los parámetros de línea y asignar funciones a los pines de salida DTR y RTS. Siga estas instrucciones si está conectando un mando FlexControl o un accesorio controlado por puerto serie a AetherSDR.

## Antes de comenzar

- La radio debe estar conectada. La pestaña Serial solo está disponible cuando AetherSDR tiene una conexión de radio activa.
- La pestaña Serial solo está presente en versiones que incluyen soporte para puerto serie. Si no la ve, su versión no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...`. Esto abre el diálogo Radio Setup directamente en la pestaña Serial. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su puerto serie de la lista. Si su puerto no aparece, haga clic en **Refresh** para volver a buscar. Para ingresar una ruta manualmente, escríbala en el campo **Path**.
3. Establezca los parámetros de línea usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con su dispositivo.
4. Para cada uno de los pines de salida **DTR** y **RTS**, establezca la **Function** deseada usando su cuadro combinado y luego establezca la **Polarity** usando el cuadro combinado adyacente.
5. Si las conexiones del paddle están invertidas, marque **Paddle Swap (swap dit/dah)**.
6. Para que AetherSDR abra este puerto cada vez que inicia, marque **Auto-open serial port on startup**.
7. Para detectar un mando de sintonía FlexControl conectado, haga clic en **Detect**. Para liberar el mando, haga clic en **Close**.
8. Para que AetherSDR detecte el mando FlexControl automáticamente al iniciar, marque **Auto-detect on startup**.
9. Para invertir la dirección de sintonía del mando, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Port** | Cuadro combinado | Selecciona el dispositivo serie de los puertos detectados. |
| **Refresh** | Botón | Vuelve a buscar puertos serie disponibles y actualiza la lista **Port**. |
| **Path** | Campo | Muestra o reemplaza la ruta del dispositivo para el puerto seleccionado. |
| **Baud** | Cuadro combinado | Establece la velocidad en baudios para la conexión serie. |
| **Data** | Cuadro combinado | Establece el número de bits de datos. |
| **Parity** | Cuadro combinado | Establece el modo de paridad. |
| **Stop** | Cuadro combinado | Establece el número de bits de parada. |
| **DTR: Function** | Cuadro combinado | Asigna la función lógica que se maneja en el pin DTR. |
| **DTR: Polarity** | Cuadro combinado | Establece la polaridad activa-alta o activa-baja para DTR. |
| **RTS: Function** | Cuadro combinado | Asigna la función lógica que se maneja en el pin RTS. |
| **RTS: Polarity** | Cuadro combinado | Establece la polaridad activa-alta o activa-baja para RTS. |
| **Paddle Swap (swap dit/dah)** | Casilla de verificación | Intercambia las entradas dit y dah del paddle. |
| **Auto-open serial port on startup** | Casilla de verificación | Vuelve a abrir el puerto configurado cada vez que AetherSDR inicia. |
| **Detect** | Botón | Intenta detectar un mando de sintonía FlexControl en el puerto seleccionado. |
| **Close** | Botón | Libera la conexión del mando FlexControl. |
| **Auto-detect on startup** | Casilla de verificación | Ejecuta automáticamente la detección del mando cuando AetherSDR inicia. |
| **Invert tuning direction** | Casilla de verificación | Invierte la dirección del mando de sintonía FlexControl. |

## Consejos

- Use **Refresh** cada vez que conecte un adaptador USB serie después de que el diálogo ya esté abierto, para que el nuevo dispositivo aparezca en la lista **Port**.
- Si usa el mando FlexControl, active **Auto-detect on startup** junto con **Auto-open serial port on startup** para que todo esté listo sin pasos manuales después de cada inicio.

## Solución de problemas

- **La pestaña Serial no es visible** — Su versión de AetherSDR no incluye soporte para puerto serie (`HAVE_SERIALPORT` no estaba habilitado en el momento de la compilación). Obtenga una versión que incluya esta función.
- **El puerto no aparece en la lista** — Haga clic en **Refresh**. En Linux, confirme que su cuenta de usuario tiene permiso para acceder al dispositivo (generalmente mediante la pertenencia al grupo `dialout`). En Windows, verifique que el dispositivo aparezca en el Administrador de dispositivos.
- **El mando FlexControl no se detecta** — Confirme que el puerto correcto está seleccionado y que el puerto está abierto. Haga clic en **Detect** nuevamente. Si el mando fue conectado después de abrir el diálogo, haga clic primero en **Refresh**.

## Relacionado

- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
