# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo conectar AetherSDR con programas de modos digitales como WSJT-X o fldigi. Se necesitan dos cosas funcionando en conjunto: DAX para transportar audio entre la radio y el programa externo, y control CAT para que el programa externo pueda leer y establecer la frecuencia y el modo.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600 (el ícono de radio en la barra de título muestra una conexión activa).
- WSJT-X, fldigi u otro programa de modos digitales está instalado y cerrado por ahora. Configure AetherSDR primero y luego inicie el programa externo.
- Decida qué slice (canal de recepción) usará para los modos digitales y anote su letra (A, B, C o D).

## Pasos

### 1. Habilitar audio DAX

1. Haga clic en el botón **DAX** del panel lateral derecho. Aparece el applet de audio DAX.
2. Haga clic en **Enable**. El botón se vuelve verde. AetherSDR inicia el puente de audio DAX y guarda `AutoStartDAX` = `True`.
3. Verifique el indicador de asignación de slice junto a **DAX 1** (o el canal que planea usar). Debe mostrar **Slice A** (o la letra que corresponde a su slice digital). Si muestra **—**, asigne el slice a ese canal DAX en la configuración de slices de su radio.
4. Si el nivel de audio de recepción en su programa externo es demasiado bajo o alto, arrastre el control deslizante **DAX 1 gain+meter** hacia la izquierda o la derecha. El valor predeterminado es 0.5 (rango 0.0–1.0); el valor se guarda como `DaxRxGain1`.
5. Si necesita transmitir audio (FT8, fldigi), ajuste el control deslizante **TX gain+meter** al nivel deseado. El valor predeterminado es 0.5 (rango 0.0–1.0); se guarda como `DaxTxGain`.

### 2. Habilitar el control CAT

1. Haga clic en el botón **CAT** del panel lateral derecho. Aparece el applet de control CAT.
2. Verifique el campo **Base**. El puerto predeterminado es `4532`. Los canales se asignan al puerto, puerto+1, puerto+2 y puerto+3 (es decir, canal A = 4532, B = 4533, y así sucesivamente). Cámbielo solo si otro programa ya está usando el puerto 4532; el valor se guarda como `CatTcpPort`.
3. Haga clic en **Enable TCP**. El botón se vuelve verde. AetherSDR inicia cuatro servidores TCP compatibles con rigctld.
4. En Linux o macOS, si su programa espera un puerto serie en lugar de una conexión TCP, haga clic también en **Enable TTY**. Aparecen enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C` y `/tmp/AetherSDR-CAT-D`.

### 3. Configurar el programa externo

**WSJT-X**

- En WSJT-X, abra **File > Settings > Radio**.
- Establezca **Rig** en `rigctld (rigctld)` o `Hamlib NET rigctl`.
- Establezca **Network Server** en `localhost` y **Port** en `4532` (o el puerto base que configuró en el paso 2, con el desplazamiento correspondiente a la letra del canal que está usando).
- En **Audio** de WSJT-X, establezca **Input** en el dispositivo de audio virtual DAX RX para el canal 1 y **Output** en el dispositivo de audio virtual DAX TX.

**fldigi**

- En fldigi, abra **Configure > Rig Control > hamlib**.
- Establezca **Rig** en `Hamlib NET rigctl` y **Device** en `localhost:4532`.
- En **Configure > Sound Card**, seleccione el dispositivo de audio virtual del canal DAX 1 para captura y reproducción.

> Los nombres exactos de los dispositivos de audio virtual DAX dependen del sistema operativo y del subsistema de audio. En Linux con PipeWire aparecen como entradas AetherSDR DAX en el mezclador de audio del sistema.

### 4. Recibir decodificaciones de WSJT-X como marcadores en el panadapter (opcional)

1. Abra **Settings > SpotHub...**.
2. Haga clic en la pestaña **WSJT-X**.
3. Confirme o establezca los campos **Address:** y **Port:** para que coincidan con la configuración multidifusión de WSJT-X (`WsjtxAddress`, `WsjtxPort`).
4. Haga clic en **Start**. AetherSDR comienza a recibir transmisiones decodificadas y las muestra en el panadapter.
5. Active **Auto-start on startup (WSJT-X)** para iniciar el receptor automáticamente; se guarda como `WsjtxAutoStart`.

### 5. Inicio automático en lanzamientos futuros

- Para iniciar el puente DAX automáticamente: **Settings > Autostart DAX with AetherSDR** (guarda `AutoStartDAX`).
- Para iniciar los servidores CAT automáticamente: **Settings > Autostart CAT with AetherSDR** (guarda `AutoStartCAT`).

## Qué hace cada control

| Control | Ubicación | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** (DAX) | Applet DAX | Off | On/Off | `AutoStartDAX` |
| **DAX 1 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxTxGain` |
| **Enable TCP** | Applet CAT | Off | On/Off | — |
| **Enable TTY** | Applet CAT | Off | On/Off | — |
| **Base** (puerto) | Applet CAT | 4532 | 1024–65535 | `CatTcpPort` |
| **Start / Stop** (WSJT-X) | SpotHub > pestaña WSJT-X | — | — | — |
| **Auto-start on startup (WSJT-X)** | SpotHub > pestaña WSJT-X | — | On/Off | `WsjtxAutoStart` |

## Consejos

- El indicador de asignación de slice junto a cada canal DAX muestra **—** cuando no hay ningún slice enrutado y **Slice A**–**Slice H** cuando hay uno asignado. Confirme que el slice correcto está asignado antes de iniciar el programa externo.
- Los valores fuera de rango en el campo de puerto **Base** vuelven automáticamente a `4532`.
- Si ejecuta varios programas digitales simultáneamente, asigne cada uno a un canal DAX diferente y a un canal CAT diferente (A, B, C o D) usando el desplazamiento de puerto correspondiente.
- Las casillas de verificación de filtro de spots de WSJT-X — **CQ**, **CQ POTA** y **Calling Me** — permiten restringir qué decodificaciones aparecen en el panadapter. Se guardan como `WsjtxFilterCQ`, `WsjtxFilterPOTA` y `WsjtxFilterCallingMe`.

## Solución de problemas

- **WSJT-X reporta "Rig control error"** — Confirme que **Enable TCP** está activo (el botón está verde) en el applet CAT y que el puerto en WSJT-X coincide con el valor de **Base** (predeterminado `4532`). Verifique que ningún cortafuegos esté bloqueando las conexiones TCP en localhost.
- **Sin audio en WSJT-X** — Confirme que **Enable** en el applet DAX está verde y que el indicador de asignación de slice junto a DAX 1 muestra su slice digital y no **—**. Verifique también que WSJT-X apunta al dispositivo de audio virtual DAX correcto.
- **El audio de TX no llega a la radio** — Verifique que el control deslizante **TX gain+meter** no esté en 0.0 y que su slice digital tenga privilegios de TX (el indicador de asignación TX en el applet DAX muestra la letra de su slice y no **—**).
- **Los puertos TTY de CAT no aparecen** — **Enable TTY** solo está disponible en Linux y macOS. En Windows, use TCP (`localhost:4532`) en su lugar.

## Relacionados

- [Habilitar DAX para enrutar audio del slice a WSJT-X / FLDigi / otro programa digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X controlen la radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS abran un puerto CAT de tipo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar la ganancia DAX RX por canal](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](../../features/dax/set-dax-tx-gain.md)
- [Inicio automático de DAX al lanzar AetherSDR](../../features/dax/autostart-dax-on-launch.md)
- [Inicio automático de los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Audio DAX](../../features/dax/set-dax-rx-gain-per-channel.md)
