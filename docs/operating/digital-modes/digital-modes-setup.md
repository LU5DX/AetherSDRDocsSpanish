# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo conectar WSJT-X, fldigi o software similar de modos digitales a AetherSDR para que puedan recibir audio de la radio, enviar audio para TX y controlar el VFO. Necesita dos puentes ejecutándose en AetherSDR: DAX (audio) y CAT (control de frecuencia y modo).

## Antes de empezar

- AetherSDR está conectado al FLEX-8600 y al menos un slice está activo.
- WSJT-X, fldigi o su aplicación de modos digitales elegida está instalada.
- Usted sabe qué letra de slice (A, B, C, …) piensa usar para modos digitales.

## Pasos

### Parte 1 — Activar audio DAX

1. Haga clic en el botón **DAX** de la bandeja en la barra lateral derecha. Se abre el applet de audio DAX.
2. Haga clic en **Enable**. El botón se vuelve verde. AetherSDR inicia el puente de audio DAX y persiste la configuración como `AutoStartDAX`.
3. Observe el slice que se muestra en el indicador **Slice-assignment status** junto al canal DAX que desea usar (por ejemplo, "Slice A" junto a **DAX 1:**). Si muestra —, asigne el slice a un canal DAX en la configuración de slices de su radio antes de continuar.
4. Opcionalmente, ajuste el control deslizante **DAX 1 gain+meter** para su canal de RX. El valor predeterminado es 0.5; el rango válido es 0.0–1.0. Esto se persiste como `DaxRxGain1` (o `DaxRxGain2`–`DaxRxGain4` para otros canales).
5. Opcionalmente, ajuste el control deslizante **TX gain+meter**. El valor predeterminado es 0.5; el rango válido es 0.0–1.0. Se persiste como `DaxTxGain`.
6. Para iniciar DAX automáticamente en cada inicio, vaya a `Settings > Autostart DAX with AetherSDR` y marque ese elemento.

### Parte 2 — Activar control CAT

1. Haga clic en el botón **CAT** de la bandeja en la barra lateral derecha. Se abre el applet de control CAT.
2. Verifique el campo del puerto **Base**. El valor predeterminado es `4532`. Los canales A–D se vinculan a los puertos 4532, 4533, 4534, 4535. El rango válido es 1024–65535. Cambie el valor si otra aplicación ya usa el puerto 4532.
3. Haga clic en **Enable TCP**. El botón se vuelve verde. Se inician los cuatro servidores TCP compatibles con rigctld.
4. En Linux o macOS, haga clic en **Enable TTY** si su aplicación requiere un puerto de tipo serie. Los enlaces simbólicos PTY aparecen en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C`, `/tmp/AetherSDR-CAT-D`.
5. Para iniciar CAT automáticamente en cada inicio, vaya a `Settings > Autostart CAT with AetherSDR` y marque ese elemento.

### Parte 3 — Configurar su aplicación de modos digitales

**WSJT-X**

1. En WSJT-X, abra **Settings > Radio**.
2. Establezca **Rig** en `Hamlib NET rigctl`.
3. Establezca **Network Server** en `localhost:4532` (o el puerto que coincida con el canal de su slice elegido).
4. Abra **Settings > Audio** y configure los dispositivos de **Input** y **Output** en el canal DAX asignado a su slice (por ejemplo, `DAX 1`).

**fldigi**

1. En fldigi, abra **Configure > Rig Control > Hamlib**.
2. Establezca **Device** en `Net rigctl` y **Port/Address** en `localhost:4532`.
3. Abra **Configure > Sound Card** y seleccione el canal DAX para entrada y salida.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|
| **Enable** (DAX) | desactivado | activado/desactivado | `AutoStartDAX` |
| **DAX 1 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4 gain+meter** | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX gain+meter** | 0.5 | 0.0–1.0 | `DaxTxGain` |
| **Enable TCP** (CAT) | desactivado | activado/desactivado | — |
| **Enable TTY** (CAT) | desactivado | activado/desactivado | — |
| **Base** (puerto TCP CAT) | 4532 | 1024–65535 | `CatTcpPort` |

## Consejos

- Cada canal CAT (A/B/C/D) controla un slice. Si ejecuta dos programas de modos digitales simultáneamente, apunte el segundo programa al puerto 4533 y asígnelo al Slice B con un segundo canal DAX.
- Si ingresa un valor fuera de rango en el campo **Base**, se restablece automáticamente a `4532`.
- El indicador de estado TCP por canal en el applet CAT muestra cuántos clientes están conectados (por ejemplo, `:4532 (1 client)`). Úselo para confirmar que WSJT-X se ha conectado correctamente.

## Solución de problemas

- **WSJT-X reporta "Rig not found" o conexión rechazada** — Confirme que **Enable TCP** esté activo (el botón está verde) y que el puerto en WSJT-X coincida con el valor **Base** en AetherSDR. Verifique que ningún cortafuegos esté bloqueando las conexiones de localhost.
- **No se decodifica audio en WSJT-X / fldigi** — Confirme que **Enable** en el applet DAX esté activo. Verifique que el estado de asignación de slice junto al canal DAX que seleccionó muestre la letra de su slice y no —. Asegúrese de que el dispositivo de entrada de audio en su aplicación de modos digitales esté configurado en el canal DAX correcto.
- **El audio de TX no llega a la radio** — Verifique que el control deslizante **TX gain+meter** no esté en 0.0. Confirme que el indicador de slice TX en el applet DAX muestre su slice activo.
- **Los enlaces simbólicos PTY no aparecen (Linux/macOS)** — Confirme que **Enable TTY** esté activo. Las rutas `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D` se crean cuando TTY está activado y la radio está conectada.

## Relacionados

- [DAX Audio overview](../../features/dax/overview.md)
- [Enable DAX to route slice audio to WSJT-X / FLDigi / other digital software](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [CAT Control overview](../../features/cat-control/overview.md)
- [Enable CAT TCP so N1MM, Log4OM, WSJT-X can control the radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Enable CAT PTY so Linux/macOS apps can open a serial-style CAT port](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Autostart DAX on launch](../../features/dax/autostart-dax-on-launch.md)
- [Autostart CAT servers with AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Change the base TCP port](../../features/cat-control/change-the-base-tcp-port.md)
- [Set DAX RX gain per channel](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Start WSJT-X UDP listener and filter for CQ, POTA or calls to me](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
