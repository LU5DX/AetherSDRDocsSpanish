# Uso del teclado o un controlador MIDI para activar un manipulador recto o paletas iambicas

Esta página explica cómo enviar CW usando el teclado de la computadora o un controlador MIDI como manipulador recto o paletas iambicas a través del applet Phone/CW. Esto le permite manipular el radio sin necesidad de conectar un manipulador físico al FLEX-8600.

## Antes de empezar

- El slice activo debe estar en modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando se selecciona el modo CW.
- El applet Phone/CW debe estar visible. Si no lo está, haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar la barra lateral.
- Para entrada MIDI, su controlador MIDI debe estar conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para asignar las entradas del controlador a funciones de manipulación.

## Pasos

1. Seleccione un modo CW en el slice activo. El applet Phone/CW cambia al subpanel CW.
2. Decida si desea operar con manipulador recto o con paletas iambicas. Para iambico, haga clic en **Iambic** para activarlo (resaltado). Para manipulador recto, deje **Iambic** inactivo.
3. Ajuste su velocidad de manipulación con el control deslizante **Speed (CW)** (5–100 WPM). También puede escribir un valor directamente en el campo de texto adyacente.
4. Elija cómo se activa la TX:
   - Para break-in completo (QSK), haga clic en **Breakin** para activarlo. Los flancos de manipulación desde el teclado o controlador MIDI activarán la TX inmediatamente; el retardo de break-in del radio mantiene el relé entre caracteres.
   - Para PTT manual, deje **Breakin** inactivo. La entrada de manipulación se pondrá en cola; active el PTT por separado para transmitir. Consulte [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md).
5. Si desea escuchar el tono local mientras manipula, haga clic en **Sidetone** para activarlo. Ajuste el control deslizante **Sidetone volume** a un nivel confortable. El tono local de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) y el monitor alimentado por DAX del radio son controlados por este único botón y control deslizante. También puede escribir un valor de volumen directamente en el campo de texto adyacente.
6. Ajuste el **Delay (CW)** para el tiempo de retención del break-in (0–2000 ms). Puede usar el control deslizante o escribir un valor directamente en el campo de texto adyacente.
7. Ajuste el **Pitch < / >** a su frecuencia de tono local preferida (100–6000 Hz). Escriba un valor directamente en el campo de texto o haga clic en los botones **<** y **>** para ajustar en pasos de 10 Hz.
8. Comience a manipular desde el teclado o el controlador MIDI. Con **Iambic** activo, las entradas de dit y dah se tratan como contactos de paletas. Con **Iambic** inactivo, cualquier entrada de tecla actúa como cierre de manipulador recto.

## Qué hace cada control

| Control               | Qué hace                                                                                                                                                                                                                                             | Valor predeterminado                                                                                                    |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **Iambic**            | Activa/desactiva el manipulador de paletas iambicas. Cuando está activo, las entradas del teclado/MIDI se tratan como contactos de paletas dit y dah. Cuando está inactivo, la entrada actúa como un manipulador recto.                                 | —                                                                                                                       |
| **Breakin**           | Activa/desactiva el break-in completo (QSK). Cuando está activo, los flancos de manipulación activan la TX y el retardo de break-in mantiene el relé. Cuando está inactivo, las teclas se ponen en cola y el PTT debe activarse manualmente.            | —                                                                                                                       |
| **Speed (CW)**        | Ajusta la velocidad de manipulación aplicada a la entrada del teclado y MIDI. Escriba un valor (5–100) directamente en el campo de texto o use el control deslizante.                                                                                 | 20 WPM                                                                                                                  |
| **Delay (CW)**        | Ajusta el tiempo de retención del break-in CW después del último flanco de manipulación antes de que la TX se desactive. Escriba un valor (0–2000 ms) directamente en el campo de texto o use el control deslizante.                                  | 500 ms                                                                                                                  |
| **Sidetone**          | Activa el monitor de tono local CW. Controla tanto el monitor alimentado por DAX del radio como el generador de tono local de baja latencia del lado del cliente de forma sincronizada.                                                               | —                                                                                                                       |
| **Sidetone volume**   | Ajusta el volumen del monitor CW. Controla los volúmenes del lado del radio y del tono local del lado del cliente de forma sincronizada. Escriba un valor (0–100) directamente en el campo de texto o use el control deslizante.                      | 50                                                                                                                      |
| **Pitch < / >**       | Ajusta el tono local y el tono de decodificación. Escriba un valor (100–6000 Hz) directamente en el campo de texto, o haga clic en los botones **<** y **>** para ajustar en pasos de 10 Hz. El tono sigue automáticamente el ajuste `cw_pitch` del radio. | 600 Hz                                                                                                                  |
| **ALC (Panel Phone)** | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB posterior al ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS.                                                | Reconfigurado desde HWALC (tensión RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. |
| **ALC (Panel CW)**    | Refleja el indicador ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Ambos indicadores usan escala dBFS (-20 a 0 dBFS), se llenan desde la derecha.                                            | Agregado en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight.         |

## Consejos

- En v0.9.8, las etiquetas de valor de **Delay (CW)**, **Speed (CW)**, **Sidetone volume** y **Pitch** ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente; esto coincide con el comportamiento de SmartSDR.
- El tono local y la panorámica estéreo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio; no necesita reconfigurarlos después de cambiar el tono CW del radio.
- Con **Breakin** desactivado, la entrada de manipulación desde el teclado o controlador MIDI se pone en cola. Esto es útil cuando desea componer caracteres antes de transmitir. Active el PTT manualmente para enviar la entrada en cola.
- Hacer doble clic en el control deslizante **L / R pan (CW)** lo centra de nuevo en 50 (centro).

## Solución de problemas

- **El controlador MIDI no se reconoce** — Asegúrese de que el controlador estaba conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para verificar que el dispositivo aparezca en la lista y que las entradas estén asignadas.
- **La manipulación no activa la TX** — Verifique que **Breakin** esté activo si espera operación QSK. Si **Breakin** está inactivo, el radio espera un PTT manual para transmitir las teclas en cola.
- **No se escucha tono local al manipular** — Confirme que **Sidetone** esté activo y que el **Sidetone volume** esté por encima de cero. Verifique también que el slice activo esté en modo CW; el subpanel CW solo aparece en modo CW.
- **Las paletas iambicas envían comportamiento de manipulador recto** — Confirme que **Iambic** esté activo (resaltado) en el subpanel CW.

## Relacionado

- [Enable iambic paddle keying](enable-iambic-paddle-keying.md)
- [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
