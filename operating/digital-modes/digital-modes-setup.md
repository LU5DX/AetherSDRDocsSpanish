# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo conectar WSJT-X, fldigi u otro software de modos digitales a su FLEX-8600 a través de AetherSDR. Intervienen dos funciones de AetherSDR: DAX (enrutamiento de audio) y CAT Control (control de frecuencia y modo).

## Antes de comenzar

- AetherSDR está conectado a su radio FLEX-8600.
- El slice que utilizará para modos digitales ya está creado y sintonizado en la banda correcta.
- WSJT-X, fldigi o la aplicación de modos digitales de su preferencia está instalada.

## Pasos

### Parte 1 — Enrutar audio con DAX

1. Haga clic en el botón **DAX** del panel lateral derecho. Aparece el applet DAX Audio.
2. Haga clic en **Enable**. El botón se vuelve verde. AetherSDR inicia el puente de audio DAX y guarda este estado como `AutoStartDAX`.
3. Localice la fila de canal (**DAX 1**, **DAX 2**, **DAX 3** o **DAX 4**) cuyo indicador de asignación de slice muestre el slice que está usando (por ejemplo, `Slice A`). Si aún no hay ningún slice asignado, asigne uno desde la configuración de slices del radio.
4. Anote el número de canal DAX. Ingresará ese canal como dispositivo de audio en su software de modos digitales.
5. Arrastre el control **DAX 1 gain+meter** (o el canal que haya elegido) para ajustar la ganancia de RX. El valor predeterminado es `0.5`; el rango válido es `0.0`–`1.0`. Ajuste hasta que el software digital reciba un nivel de señal limpio.
6. Arrastre el control **TX gain+meter** para ajustar el nivel de audio de transmisión. El valor predeterminado es `0.5`; el rango válido es `0.0`–`1.0`.
7. En su software de modos digitales, seleccione el canal DAX correspondiente como dispositivo de entrada y salida de audio. En Linux aparecen como dispositivos PipeWire o ALSA con el nombre del canal DAX; en macOS aparecen como dispositivos CoreAudio.

### Parte 2 — Conectar el control CAT

1. Haga clic en el botón **CAT** del panel lateral derecho. Aparece el applet CAT Control.
2. Verifique el campo **Base**. El puerto predeterminado es `4532`. Los canales A hasta D se vinculan a Base, Base+1, Base+2 y Base+3. Cambie el valor solo si el puerto 4532 ya está en uso en su sistema; el rango válido es `1024`–`65535`. El valor se guarda como `CatTcpPort`.
3. Haga clic en **Enable TCP**. El botón se vuelve verde. AetherSDR inicia servidores TCP compatibles con rigctld en los cuatro puertos.
4. En Linux o macOS, si su software requiere un puerto CAT de estilo serie, haga clic también en **Enable TTY**. Se crean enlaces simbólicos en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`.
5. En su software de modos digitales, configure la interfaz de radio:
   - **Rig model:** seleccione Hamlib NET rigctl (o equivalente).
   - **Network address:** `localhost` (o la máquina que ejecuta AetherSDR).
   - **Port:** el puerto Base para el slice A (`4532` de forma predeterminada), o Base+1 para el slice B, y así sucesivamente.
   - Alternativamente, apunte el software a la ruta PTY (por ejemplo `/tmp/AetherSDR-CAT-A`) si usa **Enable TTY**.

### Parte 3 — Conectar los decodificados de WSJT-X al panadapter (opcional)

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. Configure **Address:** y **Port:** para que coincidan con el destino al que WSJT-X está configurado para enviar mensajes UDP (el valor predeterminado de WSJT-X es multidifusión `224.0.0.1` o `localhost`, puerto `2237`). Estos valores se guardan como `WsjtxAddress` y `WsjtxPort`.
4. Haga clic en **Start**. AetherSDR comienza a escuchar los mensajes UDP de WSJT-X.
5. Active los filtros que desee: marque **CQ** para mostrar solo llamadas CQ, **CQ POTA** para llamadas POTA, o **Calling Me** para mostrar solo los decodificados dirigidos a su indicativo. Estos se guardan como `WsjtxFilterCQ`, `WsjtxFilterPOTA` y `WsjtxFilterCallingMe`.
6. Las transmisiones decodificadas aparecen en la consola **WSJT-X Decodes** y como spots en el panadapter.
7. Para mantener el receptor activo tras reinicios, active **Auto-start on startup (WSJT-X)**. Esto se guarda como `WsjtxAutoStart`.

## Qué hace cada control

### Applet DAX Audio

| Control | Predeterminado | Rango | Clave de configuración | Función |
|---|---|---|---|---|
| Enable | Off | On/Off | `AutoStartDAX` | Inicia el puente de audio DAX. Interruptor principal para todos los flujos de RX y TX. |
| DAX 1–4 gain+meter | `0.5` | `0.0`–`1.0` | `DaxRxGain1`–`DaxRxGain4` | Ajusta la ganancia de RX en cada canal DAX. Arrastre para modificar. |
| TX gain+meter | `0.5` | `0.0`–`1.0` | `DaxTxGain` | Ajusta el nivel de audio de transmisión para el flujo DAX TX. |
| Indicador de asignación de slice | — | `—` o `Slice A`–`H` | — | Muestra qué slice está enrutado a cada canal DAX. |

### Applet CAT Control

| Control | Predeterminado | Rango | Clave de configuración | Función |
|---|---|---|---|---|
| Enable TCP | Off | On/Off | — | Inicia los cuatro servidores TCP rigctld en Base hasta Base+3. |
| Enable TTY | Off | On/Off | — | Crea enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `-D` (solo Linux/macOS). |
| Base | `4532` | `1024`–`65535` | `CatTcpPort` | Puerto TCP base. Los valores fuera de rango vuelven automáticamente a `4532`. Los servidores se reinician automáticamente si ya estaban en ejecución. |

### SpotHub — pestaña WSJT-X

| Control | Predeterminado | Clave de configuración | Función |
|---|---|---|---|
| Address: | — | `WsjtxAddress` | Dirección de enlace UDP para los mensajes de WSJT-X. |
| Port: | — | `WsjtxPort` | Puerto UDP para los mensajes de WSJT-X. |
| Auto-start on startup (WSJT-X) | — | `WsjtxAutoStart` | Inicia el receptor automáticamente al arrancar AetherSDR. |
| CQ | — | `WsjtxFilterCQ` | Muestra solo las llamadas CQ de los decodificados de WSJT-X. |
| CQ POTA | — | `WsjtxFilterPOTA` | Muestra las llamadas CQ POTA. |
| Calling Me | — | `WsjtxFilterCallingMe` | Muestra solo los decodificados dirigidos a su indicativo. |
| Spot Life: | — | `WsjtxSpotLife` | Segundos que los spots de WSJT-X permanecen visibles en el panadapter. |

## Consejos

- Para que DAX se inicie automáticamente cada vez que se abra AetherSDR, use `Settings > Autostart DAX with AetherSDR` en lugar de hacer clic en **Enable** en cada sesión.
- Para que los servidores CAT se inicien automáticamente, use `Settings > Autostart CAT with AetherSDR`.
- Los indicadores de fila de canal en el applet CAT Control muestran cuántos clientes están conectados (por ejemplo, `:4532 (1 client)`). Úselos para confirmar que WSJT-X o fldigi se ha conectado correctamente.
- Si ejecuta más de una aplicación de modos digitales simultáneamente, cada una debe usar un canal DAX diferente y un canal CAT diferente (A, B, C o D).

## Solución de problemas

- **El software digital no recibe audio** — Confirme que **Enable** está activo en el applet DAX Audio (el botón está verde). Verifique que el indicador de asignación de slice en el canal DAX correcto muestre su slice en lugar de `—`. Compruebe que el software esté usando el dispositivo DAX correcto.
- **El software CAT no puede conectarse** — Confirme que **Enable TCP** está activo. Verifique que el puerto configurado en el software externo coincida con el valor de **Base** (o Base+N para el canal correcto). Asegúrese de que ningún cortafuegos esté bloqueando el puerto en localhost.
- **No se encuentra la ruta PTY** — **Enable TTY** solo está disponible en Linux y macOS. Confirme que el botón está activo. Los enlaces simbólicos aparecen en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`.
- **No aparecen decodificados de WSJT-X en el panadapter** — Confirme que se hizo clic en **Start** en `Settings > SpotHub... > WSJT-X`. Verifique que **Address:** y **Port:** en AetherSDR coincidan con el destino UDP configurado en WSJT-X.

## Relacionados

- [Activar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Activar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Activar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Inicio automático de DAX al arrancar](../../features/dax/autostart-dax
