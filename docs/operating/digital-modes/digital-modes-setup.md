# Configuración de modos digitales (FT8, WSJT-X, fldigi)

Esta página explica cómo configurar AetherSDR para que programas de modos digitales como WSJT-X o fldigi puedan recibir audio del radio, transmitir audio de vuelta a él y controlar el VFO. Se necesitan dos puentes: DAX para audio y CAT para control de frecuencia y modo.

## Antes de comenzar

- AetherSDR está en ejecución y conectado a su FLEX-8600.
- Al menos un slice está activo en el panadapter.
- WSJT-X, fldigi u otro programa de modos digitales de su elección está instalado.

## Pasos

### Parte 1 — Habilitar audio DAX

1. Haga clic en el botón **DAX** de la barra lateral derecha. Aparece el applet DAX Audio.
2. Haga clic en **Enable**. El botón se pone verde. AetherSDR inicia el puente de audio DAX.
3. Observe qué fila de canal muestra el slice que desea usar. El indicador de asignación de slice para ese canal muestra **Slice A** (o la letra que corresponda). Si todavía muestra **—**, asigne un canal DAX a su slice en la configuración de slice del radio.
4. En el applet DAX, arrastre el control deslizante **DAX 1 gain+meter** (o el canal que corresponda a su slice) para ajustar el nivel de RX. El valor predeterminado es 0.5; el rango válido es 0.0–1.0.
5. Arrastre el control deslizante **TX gain+meter** para ajustar el nivel del audio que regresa al radio. El valor predeterminado es 0.5; el rango válido es 0.0–1.0.
6. En su programa de modos digitales, seleccione el canal DAX RX como dispositivo de entrada de audio y el canal DAX TX como dispositivo de salida de audio. El nombre exacto del dispositivo depende del subsistema de audio de su sistema operativo.

### Parte 2 — Habilitar control CAT

1. Haga clic en el botón **CAT** de la barra lateral derecha. Aparece el applet CAT Control.
2. Verifique el campo **Base**. El puerto predeterminado es `4532`. Los canales A hasta D se vinculan a port, port+1, port+2, port+3. Cambie el valor solo si otra aplicación ya está usando el puerto 4532; el rango válido es 1024–65535.
3. Haga clic en **Enable TCP**. El botón se pone verde. AetherSDR inicia cuatro servidores TCP compatibles con rigctld.
4. En Linux o macOS, haga clic en **Enable TTY** si su programa requiere un puerto CAT de estilo serial. Los enlaces simbólicos aparecen en `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C` y `/tmp/AetherSDR-CAT-D`.
5. En WSJT-X, fldigi o su programa de registro, configure el equipo como **Hamlib NET rigctl** y apúntelo a `localhost:4532` (o el puerto que aparece en la fila del canal A). Para la ruta TTY, ingrese el enlace simbólico que se muestra en la fila del canal, por ejemplo `/tmp/AetherSDR-CAT-A`.

### Parte 3 (opcional) — Mostrar decodificaciones de WSJT-X en el panadapter

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **WSJT-X**.
3. Confirme que los campos **Address:** y **Port:** coincidan con la dirección de multidifusión UDP y el puerto configurados en WSJT-X (el valor predeterminado de WSJT-X es `224.0.0.1`, puerto `2237`; ajuste según su configuración de WSJT-X).
4. Haga clic en **Start**. El indicador de estado cambia a **Listening**.
5. Las llamadas decodificadas aparecen en la consola **WSJT-X Decodes** y como spots en el panadapter.
6. Para filtrar lo que se muestra, marque **CQ**, **CQ POTA** o **Calling Me** según sea necesario.

### Parte 4 (opcional) — Inicio automático al arrancar

- Para iniciar DAX automáticamente cuando AetherSDR se abra, marque `Settings > Autostart DAX with AetherSDR`. Esto se guarda como `AutoStartDAX`.
- Para iniciar los servidores TCP y TTY de CAT automáticamente, marque `Settings > Autostart CAT with AetherSDR`. Esto se guarda como `AutoStartCAT`.

## Qué hace cada control

| Control | Ubicación | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable** (maestro DAX) | Applet DAX | Apagado | On/Off | `AutoStartDAX` |
| **DAX 1 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain1` |
| **DAX 2 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain2` |
| **DAX 3 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain3` |
| **DAX 4 gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxRxGain4` |
| **TX gain+meter** | Applet DAX | 0.5 | 0.0–1.0 | `DaxTxGain` |
| Indicador de asignación de slice | Applet DAX | — | — o Slice A–H | — |
| **Enable TCP** | Applet CAT | Apagado | On/Off | — |
| **Enable TTY** | Applet CAT | Apagado | On/Off | — |
| **Base** (puerto TCP) | Applet CAT | 4532 | 1024–65535 | `CatTcpPort` |
| **Address:** (UDP de WSJT-X) | SpotHub, pestaña WSJT-X | — | — | `WsjtxAddress` |
| **Port:** (UDP de WSJT-X) | SpotHub, pestaña WSJT-X | — | 1–65535 | `WsjtxPort` |
| **Start / Stop** (WSJT-X) | SpotHub, pestaña WSJT-X | — | — | — |
| Filtro **CQ** | SpotHub, pestaña WSJT-X | — | On/Off | `WsjtxFilterCQ` |
| Filtro **CQ POTA** | SpotHub, pestaña WSJT-X | — | On/Off | `WsjtxFilterPOTA` |
| Filtro **Calling Me** | SpotHub, pestaña WSJT-X | — | On/Off | `WsjtxFilterCallingMe` |
| **Spot Life:** | SpotHub, pestaña WSJT-X | — | — | `WsjtxSpotLife` |

## Consejos

- Cada canal CAT controla un slice. El canal A corresponde al primer slice, el B al segundo, y así sucesivamente. Si ejecuta dos instancias de modos digitales simultáneamente, apunte cada una a un puerto diferente (4532 y 4533).
- Si cambia el puerto **Base** mientras **Enable TCP** está activo, AetherSDR reinicia automáticamente los cuatro servidores en los nuevos puertos.
- Las decodificaciones de WSJT-X aparecen en la superposición de spots del panadapter solo mientras el listener WSJT-X de SpotHub está en ejecución. Si el panadapter no muestra nada, verifique que el listener indique **Listening** y que WSJT-X esté configurado para enviar mensajes de estado UDP a la misma dirección y puerto.

## Solución de problemas

- **El canal DAX RX muestra "—" y no llega audio al programa** — El slice no ha sido asignado a ese canal DAX. Asigne un canal DAX al slice mediante los controles de slice del radio y confirme que el indicador se actualice para mostrar **Slice A** (o la letra correspondiente).
- **WSJT-X reporta "Hamlib error" o no puede conectarse** — Confirme que **Enable TCP** está activo (el botón está verde) y que WSJT-X apunta al puerto correcto. Verifique que ninguna regla del firewall bloquee TCP en localhost en el puerto 4532.
- **Enable TTY no aparece o está desactivado** — Los enlaces simbólicos PTY solo están disponibles en Linux y macOS. En Windows, use únicamente TCP.
- **El puerto Base vuelve a 4532** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un número de puerto válido y presione Enter para confirmar.

## Relacionado

- [Habilitar DAX para enrutar audio de slice a WSJT-X / FLDigi / otros programas digitales](../../features/dax/enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](../../features/cat-control/enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serial](../../features/cat-control/enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Iniciar el listener UDP de WSJT-X y filtrar por CQ, POTA o llamadas dirigidas a mí](../../features/dx-cluster/start-wsjt-x-udp-listener-and-filter-for-cq-pota-or-calls-to-me.md)
- [Ajustar la ganancia DAX RX por canal](../../features/dax/set-dax-rx-gain-per-channel.md)
- [Ajustar la ganancia DAX TX](../../features/dax/set-dax-tx-gain.md)
- [Inicio automático de DAX al arrancar](../../features/dax/autostart-dax-on-launch.md)
- [Inicio automático de servidores CAT con AetherSDR](../../features/cat-control/autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](../../features/cat-control/change-the-base-tcp-port.md)
