# Usar el teclado o un controlador MIDI para simular un manipulador recto o paletas iambicas

Esta página explica cómo enviar CW usando el teclado de la computadora o un controlador MIDI como un manipulador recto o paletas iambicas a través del applet Phone/CW. Esto permite teclear la radio sin necesidad de tener un manipulador físico conectado al FLEX-8600.

## Antes de comenzar

- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel de CW cuando se selecciona el modo CW.
- El applet Phone/CW debe estar visible. Si no lo está, haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar la barra lateral.
- Para la entrada MIDI, su controlador MIDI debe estar conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para asignar las entradas del controlador a las funciones de tecleo.

## Pasos

1. Seleccione un modo CW en el slice activo. El applet Phone/CW cambia al subpanel de CW.
2. Decida si desea operar con un manipulador recto o con paletas iambicas. Para iambico, haga clic en **Iambic** para activarlo (resaltado). Para manipulador recto, deje **Iambic** inactivo.
3. Ajuste su velocidad de tecleo con el deslizador **Speed (CW)** (5–100 WPM). También puede escribir un valor directamente en el campo de texto adyacente.
4. Elija cómo se activa la transmisión (TX):
   - Para break-in completo (QSK), haga clic en **Breakin** para activarlo. Los flancos de tecleo desde el teclado o controlador MIDI activarán la TX inmediatamente; el retardo de break-in de la radio mantiene el relé entre caracteres.
   - Para PTT manual, deje **Breakin** inactivo. La entrada de tecleo se pondrá en cola; active el PTT por separado para transmitir. Consulte [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md).
5. Si desea escuchar el tono lateral (sidetone) mientras teclea, haga clic en **Sidetone** para activarlo. Ajuste el deslizador **Sidetone volume** a un nivel cómodo. El tono lateral de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) y el monitor alimentado por DAX de la radio son controlados por este único botón y deslizador. También puede escribir un valor de volumen directamente en el campo de texto adyacente. En la v26.5.3, el tono lateral de CW se enruta a la salida de audio seleccionada por el usuario en lugar de a la salida predeterminada (#2899).
6. Ajuste el **Delay (CW)** para el tiempo de retención de break-in (0–2000 ms). Puede usar el deslizador o escribir un valor directamente en el campo de texto adyacente.
7. Ajuste el **Pitch < / >** a su frecuencia de tono lateral preferida (100–6000 Hz). Escriba un valor directamente en el campo de texto o haga clic en los botones **<** y **>** para incrementar o decrementar en pasos de 10 Hz.
8. Comience a teclear desde el teclado o el controlador MIDI. Con **Iambic** activo, las entradas de dit y dah se tratan como contactos de paletas. Con **Iambic** inactivo, cualquier entrada de tecla actúa como un cierre de manipulador recto.

## Qué hace cada control

| Control             | Qué hace                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                     |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Iambic**          | Alterna el keyer de paletas iambicas. Cuando está activo, las entradas del teclado/MIDI se tratan como contactos de paletas dit y dah. Cuando está inactivo, la entrada actúa como un manipulador recto.                                                                                                    | —                                                                                                                        |
| **Breakin**         | Alterna el break-in completo (QSK). Cuando está activo, los flancos de tecleo activan la TX y el retardo de break-in mantiene el relé. Cuando está inactivo, las teclas se ponen en cola y el PTT debe activarse manualmente.                                                                                 | —                                                                                                                        |
| **Speed (CW)**      | Establece la velocidad de tecleo aplicada a la entrada del teclado y MIDI. Escriba un valor (5–100) directamente en el campo de texto o use el deslizador.                                                                                                                                                  | 20 WPM                                                                                                                   |
| **Delay (CW)**      | Establece el tiempo de retención de break-in de CW después del último flanco de tecleo antes de que la TX se desactive. Escriba un valor (0–2000 ms) directamente en el campo de texto o use el deslizador.                                                                                                  | 500 ms                                                                                                                   |
| **Sidetone**        | Habilita el monitor de tono lateral de CW. Controla tanto el monitor alimentado por DAX de la radio como el generador de tono lateral de baja latencia del lado del cliente de forma sincronizada.                                                                                                          | —                                                                                                                        |
| **Sidetone volume** | Establece el volumen del monitor de CW. Controla los volúmenes de tono lateral del lado de la radio y del cliente de forma sincronizada. Escriba un valor (0–100) directamente en el campo de texto o use el deslizador.                                                                                     | 50                                                                                                                       |
| **Pitch < / >**     | Establece el tono del sidetone y de la decodificación. Escriba un valor (100–6000 Hz) directamente en el campo de texto, o haga clic en los botones **<** y **>** para incrementar o decrementar en pasos de 10 Hz. El tono sigue automáticamente la configuración `cw_pitch` de la radio.                      | 600 Hz                                                                                                                   |
| **ALC (Panel Phone)** | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El medidor se inicializa a -20 dBFS al crearse.                                                                    | Se reemplazó de HWALC (voltaje RCA) al medidor SW ALC en la v26.5.1 (#2552). Reflejado por un medidor idéntico en el subpanel CW. La constante de suelo `kAlcGaugeFloorDbfs` del medidor se establece en -20.0. Inicializado al valor de suelo al crearse en la v26.5.3. |
| **ALC (Panel CW)**    | Refleja el medidor ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Ambos medidores usan la escala dBFS (-20 a 0 dBFS), se llenan desde la derecha. El medidor se inicializa a -20 dBFS al crearse.                                                           | Añadido en la v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. Inicializado al valor de suelo al crearse en la v26.5.3. |

## Consejos

- En la v0.9.8, las etiquetas de valor de **Delay (CW)**, **Speed (CW)**, **Sidetone volume** y **Pitch** ahora son campos de texto editables. Haga clic en cualquier valor y escriba un número directamente; esto coincide con el comportamiento de SmartSDR.
- El tono del sidetone y la panoramización estéreo siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` de la radio; no es necesario reconfigurarlos después de cambiar el tono CW de la radio.
- Con **Breakin** DESACTIVADO, la entrada de tecleo desde el teclado o controlador MIDI se pone en cola. Esto es útil cuando desea componer caracteres antes de transmitir. Active el PTT manualmente para enviar la entrada en cola.
- Hacer doble clic en el deslizador **L / R pan (CW)** lo centra en 50 (centro).
- En la v26.5.3, el medidor de nivel de micrófono se suprime durante la recepción cuando el usuario deshabilita el medidor de nivel durante la recepción (a través de `met_in_rx`). Se llama al método `applyLevelMeterReceiveGate()` en los cambios de estado de TX y en los cambios de actividad de RADE para asegurar que el medidor se suprima correctamente. El medidor de Compresión ahora muestra la cantidad de compresión como un valor positivo de 0 a 25 dB, invertido a -25 a 0 dB en la cara del medidor.

## Solución de problemas

- **El controlador MIDI no es reconocido** — Asegúrese de que el controlador esté conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para verificar que el dispositivo esté listado y que las entradas estén asignadas.
- **El tecleo no activa la TX** — Verifique que **Breakin** esté activo si espera una operación QSK. Si **Breakin** está inactivo, la radio espera un PTT manual para transmitir las teclas en cola.
- **No se escucha el tono lateral (sidetone) al teclear** — Confirme que **Sidetone** esté activo y que **Sidetone volume** esté por encima de cero. También verifique que el slice activo esté en modo CW; el subpanel CW solo aparece en modo CW. En la v26.5.3, verifique que la salida de audio seleccionada por el usuario esté configurada correctamente en `Settings > Audio Output`.
- **Las paletas iambicas se comportan como manipulador recto** — Confirme que **Iambic** esté activo (resaltado) en el subpanel CW.

## Relacionado

- [Enable iambic paddle keying](enable-iambic-paddle-keying.md)
- [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
