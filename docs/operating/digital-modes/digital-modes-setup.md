# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo conectar WSJT-X, fldigi u otro software de modos digitales a AetherSDR para que el audio y el control del equipo funcionen correctamente. Es necesario enrutar el audio de recepción desde el equipo (mediante DAX) y proporcionar al software digital una forma de controlar la frecuencia y el modo (mediante CAT).

## Antes de comenzar

- AetherSDR está conectado a un equipo FLEX-8600.
- Al menos un slice (canal de recepción independiente) está activo en la banda que desea operar.
- Su software digital (WSJT-X, fldigi, etc.) está instalado y aún no se encuentra en ejecución.

## Pasos

### 1. Habilitar el puente de audio DAX

1. Haga clic en el botón **DAX** de la barra lateral derecha para abrir el applet DAX Audio.
2. Haga clic en **Enable**. El botón se pone verde. Esto inicia el puente de audio para todos los canales DAX.
3. Tome nota del canal que muestra su slice en el indicador de asignación de slice (p. ej., "Slice A"). Ese es el número de canal que debe usar en la configuración del dispositivo de audio de su software digital.
4. Si el nivel de audio es demasiado bajo o demasiado alto, arrastre el medidor/deslizador de ese canal hacia la izquierda o la derecha. La ganancia predeterminada es 0.5 (rango 0.0–1.0); el valor se guarda como `DaxRxGain1` hasta `DaxRxGain4`.
5. Para el audio de transmisión, arrastre el medidor/deslizador **TX** para ajustar la ganancia DAX de transmisión. El valor predeterminado es 0.5; se guarda como `DaxTxGain`.

### 2. Habilitar el control CAT

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control.
2. Elija cómo se conectará su software digital:

   - **TCP (todas las plataformas):** Haga clic en **Enable TCP**. AetherSDR inicia cuatro servidores TCP compatibles con rigctld. El canal A escucha en el puerto base, B en base+1, C en base+2 y D en base+3. El puerto base predeterminado es `4532`, guardado como `CatTcpPort`.
   - **Puerto serie virtual PTY (solo Linux/macOS):** Haga clic en **Enable TTY**. AetherSDR crea enlaces simbólicos en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C` y `/tmp/AetherSDR-CAT-D`.

3. Confirme que la fila del canal correspondiente a su slice muestre un puerto o una ruta PTY y un recuento de clientes.

### 3. Configurar el software digital

#### WSJT-X

- **Rig:** Seleccione "Hamlib NET rigctl".
- **Network server:** `localhost:4532` (o el puerto correspondiente al canal de su slice).
- **Audio input:** Seleccione el dispositivo de audio virtual DAX RX para el canal indicado en el paso 1.
- **Audio output:** Seleccione el dispositivo de audio virtual DAX TX.
- **PTT method:** Ajuste a "CAT" o "RTS" según su preferencia; el PTT por CAT funciona sobre la misma conexión rigctld.

#### fldigi

- **Rig control:** Seleccione "hamlib" y configure el equipo como "Hamlib NET rigctl" en `localhost:4532`.
- **Audio capture/playback:** Seleccione el dispositivo del canal DAX correspondiente a su slice.

### 4. (Opcional) Configurar la visualización de spots de WSJT-X en el panadapter

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. Configure **Address:** y **Port:** para que coincidan con la dirección multicast UDP y el puerto configurados en WSJT-X (los valores predeterminados de WSJT-X son `224.0.0.1` y puerto `2237`; los valores se guardan como `WsjtxAddress` y `WsjtxPort`).
4. Haga clic en **Start**. El botón cambia a **Stop** cuando el receptor está activo.
5. Use las casillas **CQ**, **CQ POTA** y **Calling Me** para filtrar qué decodificaciones aparecen como spots en el panadapter.
6. Para mantener el receptor en ejecución automáticamente, habilite **Auto-start on startup (WSJT-X)**; se guarda como `WsjtxAutoStart`.

### 5. (Opcional) Inicio automático de DAX y CAT en cada arranque

- Para iniciar DAX automáticamente: `Settings > Autostart DAX with AetherSDR`. Se guarda como `AutoStartDAX`.
- Para iniciar CAT TCP automáticamente: `Settings > Autostart rigctld with AetherSDR`. Se guarda como `AutoStartRigctld` (solo Linux/macOS para TTY: `Settings > Autostart CAT with AetherSDR`, se guarda como `AutoStartCAT`).

## Qué hace cada control

| Control | Dónde | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** (DAX principal) | Applet DAX | Off | On/Off | `AutoStartDAX` |
| Ganancia+medidor DAX 1–4 | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain1`–`DaxRxGain4` |
| Ganancia+medidor TX | Applet DAX | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice | Applet DAX | — | — o Slice A–H | (ninguna) |
| **Enable TCP** | Applet CAT | Off | On/Off | (ninguna; puerto base: `CatTcpPort`) |
| **Enable TTY** | Applet CAT | Off | On/Off | (ninguna) |
| **Base** (puerto TCP) | Applet CAT | 4532 | 1024–65535 | `CatTcpPort` |
| **Start / Stop** (UDP WSJT-X) | SpotHub > pestaña WSJT-X | — | — | (ninguna) |
| **Address:** (WSJT-X) | SpotHub > pestaña WSJT-X | — | — | `WsjtxAddress` |
| **Port:** (WSJT-X) | SpotHub > pestaña WSJT-X | — | 1–65535 | `WsjtxPort` |
| **Auto-start on startup (WSJT-X)** | SpotHub > pestaña WSJT-X | — | On/Off | `WsjtxAutoStart` |
| Filtro **CQ** | SpotHub > pestaña WSJT-X | — | On/Off | `WsjtxFilterCQ` |
| Filtro **CQ POTA** | SpotHub > pestaña WSJT-X | — | On/Off | `WsjtxFilterPOTA` |
| Filtro **Calling Me** | SpotHub > pestaña WSJT-X | — | On/Off | `WsjtxFilterCallingMe` |
| **Spot Life:** | SpotHub > pestaña WSJT-X | — | — | `WsjtxSpotLife` |

## Consejos

- Cada canal CAT (A–D) es independiente. Si ejecuta dos programas digitales simultáneamente, apunte el segundo al puerto `4533` (o `/tmp/AetherSDR-CAT-B`) y enrute su audio al canal DAX 2.
- El indicador de estado TCP por canal muestra "(stopped)", ":\<port\> (1 client)" o ":\<port\> (N clients)". Confirme que su software se haya conectado antes de llamar CQ.
- Los valores fuera de rango introducidos en el campo **Base** se corrigen automáticamente a `4532`.

## Solución de problemas

- **WSJT-X muestra "Rig not responding"** — Confirme que **Enable TCP** esté activo (botón iluminado en verde) en el applet CAT y que el puerto configurado en WSJT-X coincida con el valor de **Base** (predeterminado `4532`). Verifique que ningún firewall bloquee las conexiones TCP en localhost.
- **No se decodifica audio en WSJT-X o fldigi** — Confirme que **Enable** esté activo en el applet DAX. Compruebe que el indicador de asignación de slice en el canal DAX correcto muestre su slice activo y no "—". Ajuste el deslizador de ganancia DAX RX si el medidor de nivel no se mueve.
- **No aparece la ruta PTY** — **Enable TTY** está disponible solo en Linux y macOS. Confirme que AetherSDR tenga permiso para crear archivos en `/tmp`.
- **Los decodificados de WSJT-X no aparecen en el panadapter** — Verifique que el botón **Start / Stop** en SpotHub muestre el receptor como iniciado, y que **Address:** y **Port:** coincidan con los ajustes de reporte UDP dentro de WSJT-X.

## Relacionados

- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Habilitar CAT TCP para que N1MM, Log4OM y WSJT-X puedan controlar el equipo](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de tipo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas propias](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar la ganancia DAX RX por canal](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](../../features/dax/set-dax-tx-gain.md)
- [Inicio automático de DAX al arrancar](../../features/dax/autostart-dax-on-launch.md)
- [Inicio automático de los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto base](../../features/cat-control/change-the-base
