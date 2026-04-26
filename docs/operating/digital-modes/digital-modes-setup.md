# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo configurar AetherSDR para que programas de modos digitales como WSJT-X y fldigi puedan recibir audio y controlar el FLEX-8600. Se describe cómo habilitar el puente de audio DAX y los servidores de control CAT.

## Antes de comenzar

- AetherSDR está conectado a su FLEX-8600 (el indicador de conexión de radio muestra estado activo).
- El slice que desea usar para modos digitales ya está creado y sintonizado en la frecuencia y el modo correctos.
- WSJT-X, fldigi u otro programa de modos digitales está instalado.

## Pasos

### 1. Habilitar el enrutamiento de audio DAX

1. Haga clic en el botón **DAX** del panel lateral derecho. Aparece el applet de audio DAX.
2. Haga clic en **Enable**. El botón se vuelve verde. AetherSDR inicia el puente de audio DAX y persiste este estado como `AutoStartDAX`.
3. Verifique el indicador de asignación de slice junto al canal DAX que desea utilizar (por ejemplo, **DAX 1**). Muestra **—** (sin asignar) o **Slice A..H**. Si es necesario, asigne el slice correcto a un canal DAX desde la configuración de slices del radio.
4. Arrastre el control deslizante **DAX 1 gain+meter** para establecer la ganancia de RX de ese canal. El valor predeterminado es 0.5; el rango válido es 0.0–1.0. Este valor se persiste como `DaxRxGain1`.
5. Si su programa también transmite (por ejemplo, FT8 en WSJT-X), arrastre el control deslizante **TX gain+meter** para establecer el nivel de TX del DAX. El valor predeterminado es 0.5; rango válido 0.0–1.0. Se persiste como `DaxTxGain`.

### 2. Habilitar el control CAT

1. Haga clic en el botón **CAT** del panel lateral derecho. Aparece el applet de control CAT.
2. Para usar una conexión TCP (requerida para WSJT-X y la mayoría del software digital en todas las plataformas): haga clic en **Enable TCP**. El botón se vuelve verde. AetherSDR inicia cuatro servidores TCP compatibles con rigctld en los puertos **Base** hasta **Base+3** (puerto base predeterminado: **4532**, persistido como `CatTcpPort`).
3. En Linux o macOS, si su programa espera un dispositivo de puerto serie: haga clic en **Enable TTY**. AetherSDR crea enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C` y `/tmp/AetherSDR-CAT-D`.
4. Para cambiar el puerto TCP base, edite el campo **Base** y presione Enter. Rango válido: 1024–65535. Los valores fuera de rango vuelven a 4532. Los servidores en ejecución se reinician automáticamente en el nuevo puerto.

### 3. Configurar el programa de modos digitales

**WSJT-X:**
- Configure la interfaz de radio como **Hamlib NET rigctl**, host `localhost`, puerto `4532` (o el puerto que corresponda a la fila del canal del slice en el applet CAT).
- Configure el dispositivo de entrada de audio como el canal DAX RX que asignó (por ejemplo, **DAX 1** en la lista de dispositivos de audio del sistema).
- Configure el dispositivo de salida de audio como el dispositivo DAX TX.

**fldigi:**
- En la configuración de audio, seleccione el canal DAX como dispositivo de captura y reproducción de audio.
- Para el control del radio, use **Hamlib**, seleccione **NET rigctl** e ingrese `localhost:4532`.

### 4. (Opcional) Mostrar decodificaciones de WSJT-X en el panadapter

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. Ingrese la dirección de enlace UDP en **Address:** y el puerto en **Port:** para que coincidan con lo que WSJT-X está configurado para transmitir (persistidos como `WsjtxAddress` y `WsjtxPort`).
4. Haga clic en **Start**. El estado del receptor cambia a **Listening**.
5. Habilite **Auto-start on startup** para que AetherSDR inicie el receptor automáticamente en el próximo arranque (persistido como `WsjtxAutoStart`).
6. Use las casillas **CQ**, **CQ POTA** y **Calling Me** para filtrar qué decodificaciones aparecen como spots en el panadapter (persistidos como `WsjtxFilterCQ`, `WsjtxFilterPOTA`, `WsjtxFilterCallingMe`).

### 5. (Opcional) Inicio automático de DAX y CAT al arrancar

- Para iniciar DAX automáticamente: `Settings > Autostart DAX with AetherSDR`.
- Para iniciar CAT TCP automáticamente: `Settings > Autostart rigctld with AetherSDR`.
- Para iniciar CAT TTY automáticamente (Linux/macOS): `Settings > Autostart CAT with AetherSDR`.

## Función de cada control

| Control | Predeterminado | Rango | Clave persistida | Descripción |
|---|---|---|---|---|
| **Enable** (DAX) | Off | On/Off | `AutoStartDAX` | Interruptor principal del puente de audio DAX. |
| **DAX 1 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain1` | Ganancia de RX para el canal DAX 1. |
| **DAX 2 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain2` | Ganancia de RX para el canal DAX 2. |
| **DAX 3 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain3` | Ganancia de RX para el canal DAX 3. |
| **DAX 4 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain4` | Ganancia de RX para el canal DAX 4. |
| **TX gain+meter** | 0.5 | 0.0–1.0 | `DaxTxGain` | Ganancia de TX para la transmisión DAX TX. |
| **Enable TCP** | Off | On/Off | — | Inicia los cuatro servidores TCP rigctld. |
| **Enable TTY** | Off | On/Off | — | Crea enlaces simbólicos PTY (solo Linux/macOS). |
| **Base** | 4532 | 1024–65535 | `CatTcpPort` | Puerto TCP base; los canales usan Base, Base+1, Base+2, Base+3. |

## Consejos

- La asignación de canal DAX (qué slice alimenta qué canal DAX) es visible en el indicador de asignación de slice junto a cada fila de canal. Muestra **—** cuando no está asignado o **Slice A–H** cuando está activo.
- El estado TCP por canal en el applet CAT muestra cuántos clientes están conectados (por ejemplo, `:4532 (1 client)`), lo cual es útil para confirmar que WSJT-X se ha conectado correctamente.
- Si ejecuta más de un programa digital simultáneamente, asigne cada uno a un canal DAX diferente y a un canal CAT diferente (Base+1, Base+2, etc.).

## Resolución de problemas

- **WSJT-X reporta "Hamlib error" o no puede conectarse** — Confirme que **Enable TCP** está activo (el botón es verde) en el applet CAT. Verifique que el puerto en WSJT-X coincida con el valor de **Base**. Compruebe que ningún firewall esté bloqueando las conexiones a `localhost`.
- **No se recibe audio en WSJT-X o fldigi** — Confirme que **Enable** está activo en el applet DAX y que el indicador de asignación de slice del canal muestra el slice correcto en lugar de **—**. Verifique que la aplicación esté usando el dispositivo de audio DAX correcto.
- **Los enlaces simbólicos PTY no aparecen** — **Enable TTY** solo está disponible en Linux y macOS. Confirme que el botón está activo. Los enlaces simbólicos aparecen en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`.
- **Las decodificaciones de WSJT-X no aparecen en el panadapter** — Confirme que el receptor WSJT-X de SpotHub está en estado **Listening** y que la dirección y el puerto UDP coinciden con la configuración de "Reporting" en WSJT-X.

## Relacionados

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otro software digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones Linux/macOS puedan abrir un puerto CAT tipo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar el receptor UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Inicio automático de DAX al arrancar](../../features/dax/autostart-dax-on-launch.md)
- [Inicio automático de los servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Establecer la ganancia de RX DAX por canal](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Establecer la ganancia de TX DAX](../../features/dax/set-dax-tx-gain.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
