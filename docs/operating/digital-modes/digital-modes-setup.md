# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo conectar WSJT-X, fldigi u otro software de modos digitales similar a AetherSDR para que puedan recibir audio del radio, enviar audio de regreso para TX y controlar el VFO. Para ello se necesitan dos puentes activos en AetherSDR: DAX (audio) y CAT (control de frecuencia y modo).

## Antes de comenzar

- AetherSDR está conectado al FLEX-8600 y al menos un slice (canal de recepción independiente) está activo.
- WSJT-X, fldigi o la aplicación de modos digitales elegida está instalada.
- Se conoce la letra de slice (A, B, C, …) que se utilizará para los modos digitales.

## Pasos

### Parte 1 — Habilitar audio DAX

1. Haga clic en el botón **DAX** del panel lateral derecho. Se abre el applet DAX Audio.
2. Haga clic en **Enable**. El botón se pone verde. AetherSDR inicia el puente de audio DAX y guarda la configuración como `AutoStartDAX`.
3. Observe el slice que aparece en el indicador **Slice-assignment status** junto al canal DAX que desea usar (por ejemplo, "Slice A" junto a **DAX 1:**). Si muestra —, asigne el slice a un canal DAX en los ajustes de slice del radio antes de continuar.
4. Opcionalmente, ajuste el control deslizante **DAX 1 gain+meter** para su canal RX. El valor predeterminado es 0.5; el rango válido es 0.0–1.0. Este valor se guarda como `DaxRxGain1` (o `DaxRxGain2`–`DaxRxGain4` para otros canales).
5. Opcionalmente, ajuste el control deslizante **TX gain+meter**. El valor predeterminado es 0.5; el rango válido es 0.0–1.0. Se guarda como `DaxTxGain`.
6. Para iniciar DAX automáticamente en cada arranque, vaya a `Settings > Autostart DAX with AetherSDR` y marque esa opción.

### Parte 2 — Habilitar control CAT

1. Haga clic en el botón **CAT** del panel lateral derecho. Se abre el applet CAT Control.
2. Verifique el campo de puerto **Base**. El valor predeterminado es `4532`. Los canales A–D se enlazan a los puertos 4532, 4533, 4534 y 4535. El rango válido es 1024–65535. Cambie el valor si otra aplicación ya usa el puerto 4532.
3. Haga clic en **Enable TCP**. El botón se pone verde. Se inician los cuatro servidores TCP compatibles con rigctld.
4. En Linux o macOS, haga clic en **Enable TTY** si su aplicación requiere un puerto de estilo serie. Los enlaces simbólicos PTY aparecen en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C`, `/tmp/AetherSDR-CAT-D`.
5. Para iniciar CAT automáticamente en cada arranque, vaya a `Settings > Autostart CAT with AetherSDR` y marque esa opción.

### Parte 3 — Configurar la aplicación de modos digitales

**WSJT-X**

1. En WSJT-X, abra **Settings > Radio**.
2. Establezca **Rig** en `Hamlib NET rigctl`.
3. Establezca **Network Server** en `localhost:4532` (o el puerto correspondiente al canal de slice elegido).
4. Abra **Settings > Audio** y establezca los dispositivos **Input** y **Output** en el canal DAX asignado a su slice (por ejemplo, `DAX 1`).

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
| **Base** (puerto TCP de CAT) | 4532 | 1024–65535 | `CatTcpPort` |

## Consejos

- Cada canal CAT (A/B/C/D) controla un slice. Si ejecuta dos programas de modos digitales simultáneamente, apunte el segundo programa al puerto 4533 y asígnelo al Slice B con un segundo canal DAX.
- Si introduce un valor fuera de rango en el campo **Base**, este se restablece automáticamente a `4532`.
- El indicador de estado TCP por canal en el applet CAT muestra cuántos clientes están conectados (por ejemplo, `:4532 (1 client)`). Úselo para confirmar que WSJT-X se ha conectado correctamente.

## Solución de problemas

- **WSJT-X reporta "Rig not found" o conexión rechazada** — Confirme que **Enable TCP** esté activo (el botón es verde) y que el puerto en WSJT-X coincida con el valor **Base** en AetherSDR. Verifique que ningún cortafuegos esté bloqueando las conexiones a localhost.
- **WSJT-X / fldigi no decodifican audio** — Confirme que **Enable** en el applet DAX esté activo. Verifique que el indicador de asignación de slice junto al canal DAX seleccionado muestre la letra de su slice y no —. Compruebe que el dispositivo de entrada de audio en su aplicación de modos digitales esté configurado con el canal DAX correcto.
- **El audio TX no llega al radio** — Verifique que el control deslizante **TX gain+meter** no esté en 0.0. Confirme que el indicador de slice TX en el applet DAX muestre su slice activo.
- **Los enlaces simbólicos PTY no aparecen (Linux/macOS)** — Confirme que **Enable TTY** esté activo. Las rutas `/tmp/AetherSDR-CAT-A` a `/tmp/AetherSDR-CAT-D` se crean cuando TTY está habilitado y el radio está conectado.

## Relacionados

- [Descripción general de DAX Audio](../../features/dax/overview.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de CAT Control](../../features/cat-control/overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar DAX automáticamente al arrancar](../../features/dax/autostart-dax-on-launch.md)
- [Iniciar servidores CAT automáticamente con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
- [Ajustar la ganancia RX de DAX por canal](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
