# Usar el teclado o un controlador MIDI para activar una llave telegráfica directa o paletas iambic

Esta página explica cómo enviar CW utilizando el teclado de la computadora o un controlador MIDI como una llave telegráfica directa o paletas iambic a través del applet Phone/CW. Esto le permite teclear la radio sin necesidad de hardware físico de paletas conectado a la FLEX-8600.

## Antes de comenzar

- La slice activa debe estar en modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando se selecciona el modo CW.
- El applet Phone/CW debe estar visible. Si no lo está, haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar la barra lateral.
- Para entrada MIDI, su controlador MIDI debe estar conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para asignar las entradas del controlador a las funciones de llave.

## Pasos

1. Seleccione un modo CW en la slice activa. El applet Phone/CW cambia al subpanel CW.
2. Decida si desea operar con llave directa o con paletas iambic. Para iambic, haga clic en **Iambic** para activarlo (resaltado). Para llave directa, deje **Iambic** inactivo.
3. Ajuste su velocidad de tecleo con el control deslizante **Speed (CW)** (5–100 WPM). También puede escribir un valor directamente en el campo de texto adyacente.
4. Elija cómo se activa la transmisión:
   - Para full break-in (QSK), haga clic en **Breakin** para activarlo. Los flancos de la llave desde el teclado o controlador MIDI activarán la transmisión inmediatamente; el retardo de break-in de la radio mantiene el relé entre caracteres.
   - Para PTT manual, deje **Breakin** inactivo. La entrada de la llave se pondrá en cola; active el PTT por separado para transmitir. Consulte [Configurar break-in OFF para que las teclas CW se encolen y el PTT sea manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md).
5. Si desea escuchar el tono lateral (sidetone) mientras teclea, haga clic en **Sidetone** para activarlo. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El tono lateral de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) y el monitor alimentado por DAX de la radio son controlados por este único botón y control deslizante. También puede escribir un valor de volumen directamente en el campo de texto adyacente.
6. Ajuste el **Delay (CW)** para el tiempo de retención del break-in (0–2000 ms). Puede usar el control deslizante o escribir un valor directamente en el campo de texto adyacente.
7. Ajuste el **Pitch < / >** a su frecuencia de tono lateral preferida (100–6000 Hz). Escriba un valor directamente en el campo de texto o haga clic en los botones **<** y **>** para avanzar en pasos de 10 Hz.
8. Comience a teclear desde el teclado o controlador MIDI. Con **Iambic** activo, las entradas de dit y dah se tratan como contactos de paletas. Con **Iambic** inactivo, cualquier entrada de llave actúa como un cierre de llave directa.

## Función de cada control

| Control              | Qué hace                                                                                                                                                                        | Valor predeterminado |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Iambic**           | Alterna el keyer de paletas iambic. Cuando está activo, las entradas del teclado/MIDI se tratan como contactos de paletas dit y dah. Cuando está inactivo, la entrada actúa como una llave directa. | —                    |
| **Breakin**          | Alterna el full break-in (QSK). Cuando está activo, los flancos de la llave activan la transmisión y el retardo de break-in mantiene el relé. Cuando está inactivo, las teclas se encolan y el PTT debe activarse manualmente. | —                    |
| **Speed (CW)**       | Establece la velocidad de tecleo aplicada a la entrada del teclado y MIDI. Escriba un valor (5–100) directamente en el campo de texto o use el control deslizante.              | 20 WPM               |
| **Delay (CW)**       | Establece el tiempo de retención del break-in CW después del último flanco de la llave antes de que caiga la transmisión. Escriba un valor (0–2000 ms) directamente en el campo de texto o use el control deslizante. | 500 ms               |
| **Sidetone**         | Activa el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente al unísono. | —                    |
| **Sidetone volume**  | Establece el volumen del monitor CW. Controla tanto los volúmenes de tono lateral del lado de la radio como del lado del cliente al unísono. Escriba un valor (0–100) directamente en el campo de texto o use el control deslizante. | 50                   |
| **Pitch < / >**      | Establece el tono del tono lateral y de la decodificación. Escriba un valor (100–6000 Hz) directamente en el campo de texto, o haga clic en los botones **<** y **>** para avanzar en pasos de 10 Hz. El tono sigue automáticamente el ajuste `cw_pitch` de la radio. | 600 Hz               |

## Consejos

- En la v0.9.8, las etiquetas de los valores **Delay (CW)**, **Speed (CW)**, **Sidetone volume** y **Pitch** son ahora campos de texto editables. Haga clic en cualquier valor y escriba un número directamente; esto coincide con el comportamiento de SmartSDR.
- El tono del tono lateral y la panorámica estéreo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no necesita reconfigurarlos después de cambiar el tono CW de la radio.
- Con **Breakin** OFF, la entrada de la llave desde el teclado o controlador MIDI se pone en cola. Esto es útil cuando desea componer caracteres antes de transmitir. Active el PTT manualmente para enviar la entrada encolada.
- Al hacer doble clic en el control deslizante **L / R pan (CW)** se vuelve a centrar en 50 (centro).

## Solución de problemas

- **El controlador MIDI no es reconocido** — Asegúrese de que el controlador esté conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para verificar que el dispositivo esté listado y las entradas estén asignadas.
- **El tecleo no activa la transmisión** — Verifique que **Breakin** esté activo si espera operación QSK. Si **Breakin** está inactivo, la radio espera un PTT manual para transmitir las teclas encoladas.
- **No se escucha el tono lateral al teclear** — Confirme que **Sidetone** esté activo y que **Sidetone volume** esté por encima de cero. También verifique que la slice activa esté en modo CW; el subpanel CW solo aparece en modo CW.
- **Las paletas iambic se comportan como llave directa** — Confirme que **Iambic** esté activo (resaltado) en el subpanel CW.

## Relacionado

- [Habilitar el tecleo con paletas iambic](enable-iambic-paddle-keying.md)
- [Configurar break-in OFF para que las teclas CW se encolen y el PTT sea manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md)
- [Establecer la velocidad de tecleo CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Activar el tono lateral CW de baja latencia (el botón Sidetone controla tanto la radio como la ruta local)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
