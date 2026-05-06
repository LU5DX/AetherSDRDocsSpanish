# Usar el teclado o un controlador MIDI como manipulador recto o paletas iámbricas

Esta página explica cómo enviar CW usando el teclado de la computadora o un controlador MIDI como manipulador recto o paletas iámbricas a través del applet Phone/CW. Esto permite manipular el radio sin necesidad de conectar hardware físico de paletas al FLEX-8600.

## Antes de comenzar

- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel de CW cuando se selecciona el modo CW.
- El applet Phone/CW debe estar visible. Si no lo está, haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar la barra lateral.
- Para entrada MIDI, su controlador MIDI debe estar conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para asignar las entradas del controlador a las funciones de manipulación.

## Pasos

1. Seleccione un modo CW en el slice activo. El applet Phone/CW cambia al subpanel de CW.
2. Decida si desea operación con manipulador recto o paletas iámbricas. Para iámbrico, haga clic en **Iambic** para activarlo (resaltado). Para manipulador recto, deje **Iambic** inactivo.
3. Ajuste su velocidad de manipulación con el control deslizante **Speed (CW)** (5–100 WPM).
4. Elija cómo se activa TX:
   - Para ruptura total (QSK), haga clic en **Breakin** para activarlo. Los flancos de manipulación del teclado o controlador MIDI activarán TX inmediatamente; el retardo de ruptura del radio mantiene el relé entre caracteres.
   - Para PTT manual, deje **Breakin** inactivo. La entrada de manipulación se pondrá en cola; active PTT por separado para transmitir. Consulte [Configurar ruptura OFF para que las teclas CW se pongan en cola y el PTT sea manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md).
5. Si desea sidetone mientras manipula, haga clic en **Sidetone** para habilitarlo. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El sidetone de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) y el monitor alimentado por DAX del radio están controlados ambos por este único botón y control deslizante.
6. Comience a manipular desde el teclado o el controlador MIDI. Con **Iambic** activo, las entradas de dit y dah se tratan como contactos de paleta. Con **Iambic** inactivo, cualquier entrada de tecla actúa como un cierre de manipulador recto.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Iambic** | Activa o desactiva el manipulador de paletas iámbricas. Cuando está activo, las entradas de teclado/MIDI se tratan como contactos de paleta de dit y dah. Cuando está inactivo, la entrada actúa como manipulador recto. | — | On / Off | — |
| **Breakin** | Activa o desactiva la ruptura total (QSK). Cuando está activo, los flancos de manipulación activan TX y el retardo de ruptura mantiene el relé. Cuando está inactivo, las teclas se ponen en cola y el PTT debe activarse manualmente. | — | On / Off | — |
| **Speed (CW)** | Establece la velocidad de manipulación aplicada a la entrada de teclado y MIDI. | — | 5–100 WPM | — |
| **Delay (CW)** | Establece el tiempo de espera de ruptura CW después del último flanco de manipulación antes de que TX caiga. | — | 0–2000 ms (paso 10) | — |
| **Sidetone** | Habilita el monitor de sidetone CW. Controla en sincronía tanto el monitor alimentado por DAX del radio como el generador de sidetone de baja latencia del lado del cliente. | — | On / Off | — |
| **Sidetone volume** | Ajusta el volumen del monitor CW. Controla en sincronía los volúmenes de sidetone del lado del radio y del lado del cliente. | — | 0–100 | — |
| **Pitch < / >** | Avanza el tono de sidetone y decodificación en pasos de 10 Hz. El tono sigue automáticamente la configuración `cw_pitch` del radio. | 600 Hz | 100–6000 Hz (paso 10) | — |

## Consejos

- El tono y el paneo estéreo del sidetone siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` del radio; no es necesario reconfigurarlos después de cambiar el tono CW del radio.
- Con **Breakin** OFF, la entrada de tecla del teclado o controlador MIDI se pone en cola. Esto es útil cuando desea componer caracteres antes de transmitir. Active PTT manualmente para enviar la entrada en cola.
- Hacer doble clic en el control deslizante **L / R pan (CW)** lo recentra en 50 (centro).

## Solución de problemas

- **El controlador MIDI no es reconocido** — Asegúrese de que el controlador estaba conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para verificar que el dispositivo aparece en la lista y que las entradas están asignadas.
- **La manipulación no activa TX** — Verifique que **Breakin** esté activo si espera operación QSK. Si **Breakin** está inactivo, el radio espera un PTT manual para transmitir las teclas en cola.
- **No se escucha sidetone al manipular** — Confirme que **Sidetone** esté activo y que **Sidetone volume** esté por encima de cero. Verifique también que el slice activo esté en modo CW; el subpanel de CW solo aparece en modo CW.
- **Las paletas iámbricas envían comportamiento de manipulador recto** — Confirme que **Iambic** esté activo (resaltado) en el subpanel de CW.

## Relacionados

- [Habilitar manipulación con paletas iámbricas](enable-iambic-paddle-keying.md)
- [Configurar ruptura OFF para que las teclas CW se pongan en cola y el PTT sea manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md)
- [Ajustar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Ajustar el retardo de ruptura CW](set-cw-break-in-delay.md)
- [Habilitar el sidetone CW de baja latencia (el botón Sidetone controla tanto el radio como la ruta local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
