# Usar el teclado o un controlador MIDI para simular un manipulador recto o paletas iambicas

Esta página explica cómo enviar CW usando el teclado de la computadora o un controlador MIDI como un manipulador recto o paletas iambicas a través del applet Phone/CW. Esto permite accionar el PTT del radio sin necesidad de tener un manipulador físico conectado al FLEX-8600.

## Antes de comenzar

- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando se selecciona el modo CW.
- El applet Phone/CW debe estar visible. Si no lo está, haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha, o vaya a `View > Applet Panel` para mostrar la barra lateral.
- Para entrada MIDI, su controlador MIDI debe estar conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para asignar las entradas del controlador a las funciones de accionamiento.

## Pasos

1. Seleccione un modo CW en el slice activo. El applet Phone/CW cambiará al subpanel CW.
2. Decida si desea operar como manipulador recto o como paletas iambicas. Para iambico, haga clic en **Iambic** para activarlo (resaltado). Para manipulador recto, deje **Iambic** inactivo.
3. Ajuste su velocidad de accionamiento con el control deslizante **Speed (CW)** (5–100 WPM). También puede escribir un valor directamente en el campo de texto adyacente.
4. Elija cómo se activa la transmisión (TX):
   - Para break-in completo (QSK), haga clic en **Breakin** para activarlo. Los flancos de accionamiento desde el teclado o el controlador MIDI activarán la TX inmediatamente; el retardo de break-in del radio mantiene el relé entre caracteres.
   - Para PTT manual, deje **Breakin** inactivo. La entrada de accionamiento se pondrá en cola; active el PTT por separado para transmitir. Consulte [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md).
5. Si desea escuchar el tono de prueba (sidetone) mientras acciona, haga clic en **Sidetone** para habilitarlo. Ajuste el control deslizante **Sidetone volume** a un nivel cómodo. El tono de prueba de baja latencia del lado del cliente (aproximadamente 10 ms de latencia) y el monitor alimentado por DAX del radio son controlados por este mismo botón y control deslizante. También puede escribir un valor de volumen directamente en el campo de texto adyacente. En v26.5.3, el tono de prueba CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899).
6. Ajuste el **Delay (CW)** para el tiempo de espera del break-in (0–2000 ms). Puede usar el control deslizante o escribir un valor directamente en el campo de texto adyacente.
7. Ajuste el **Pitch < / >** a su frecuencia de tono de prueba preferida (100–6000 Hz). Escriba un valor directamente en el campo de texto o haga clic en los botones **<** y **>** para cambiar en pasos de 10 Hz.
8. Comience a accionar desde el teclado o el controlador MIDI. Con **Iambic** activo, las entradas de dit y dah se tratan como contactos de paletas. Con **Iambic** inactivo, cualquier entrada del teclado actúa como el cierre de un manipulador recto.

## Función de cada control

| Control             | Qué hace                                                                                                                                                                                                                             | Valor predeterminado                                                                                                     |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **Iambic**          | Activa/desactiva el keyer de paletas iambicas. Cuando está activo, las entradas del teclado/MIDI se tratan como contactos de paletas dit y dah. Cuando está inactivo, la entrada actúa como un manipulador recto.                     | —                                                                                                                        |
| **Breakin**         | Activa/desactiva el break-in completo (QSK). Cuando está activo, los flancos de accionamiento activan la TX y el retardo de break-in mantiene el relé. Cuando está inactivo, las claves se ponen en cola y el PTT debe activarse manualmente. | —                                                                                                                        |
| **Speed (CW)**      | Establece la velocidad de accionamiento aplicada a la entrada del teclado y MIDI. Escriba un valor (5–100) directamente en el campo de texto o use el control deslizante.                                                            | 20 WPM                                                                                                                   |
| **Delay (CW)**      | Establece el tiempo de espera del break-in CW después del último flanco de accionamiento antes de que la TX se desactive. Escriba un valor (0–2000 ms) directamente en el campo de texto o use el control deslizante.                  | 500 ms                                                                                                                   |
| **Sidetone**        | Habilita el monitor de tono de prueba CW. Controla tanto el monitor alimentado por DAX del radio como el generador de tono de prueba de baja latencia del lado del cliente de forma sincronizada.                                    | —                                                                                                                        |
| **Sidetone volume** | Establece el volumen del monitor CW. Controla los volúmenes del tono de prueba tanto del lado del radio como del lado del cliente de forma sincronizada. Escriba un valor (0–100) directamente en el campo de texto o use el control deslizante. | 50                                                                                                                       |
| **Pitch < / >**     | Establece el tono de prueba y la frecuencia de decodificación. Escriba un valor (100–6000 Hz) directamente en el campo de texto, o haga clic en los botones **<** y **>** para cambiar en pasos de 10 Hz. El tono sigue automáticamente la configuración `cw_pitch` del radio. | 600 Hz                                                                                                                   |
| **ALC (Phone panel)** | Muestra la lectura del control automático de nivel desde MeterModel::swAlcChanged (pico SSB post-ALC por software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. El indicador se inicializa a -20 dBFS al construirse. | Reconfigurado desde HWALC (voltaje RCA) al medidor SW ALC en v26.5.1 (#2552). Reflejado por un indicador idéntico en el subpanel CW. La constante de piso `kAlcGaugeFloorDbfs` del indicador está establecida en -20.0. Inicializado al valor de piso al construirse en v26.5.3. |
| **ALC (CW panel)**    | Refleja el indicador ALC del panel Phone; ambos leen desde MeterModel::swAlcChanged para lecturas consistentes en voz y CW. Ambos indicadores usan la escala dBFS (-20 a 0 dBFS), se llenan desde la derecha. El indicador se inicializa a -20 dBFS al construirse. | Añadido en v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight. Inicializado al valor de piso al construirse en v26.5.3. |

## Consejos

- En v0.9.8, las etiquetas de valor de **Delay (CW)**, **Speed (CW)**, **Sidetone volume** y **Pitch** son ahora campos de texto editables. Haga clic en cualquier valor y escriba un número directamente; esto coincide con el comportamiento de SmartSDR.
- El tono de prueba y la panorámica estéreo siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio; no necesita reconfigurarlos después de cambiar el tono CW del radio.
- Con **Breakin** desactivado, la entrada de accionamiento desde el teclado o el controlador MIDI se pone en cola. Esto es útil cuando desea componer caracteres antes de transmitir. Active el PTT manualmente para enviar la entrada en cola.
- Un doble clic en el control deslizante **L / R pan (CW)** lo centra nuevamente en 50 (centro).
- En v26.5.3, el medidor de nivel de micrófono se suprime durante la recepción cuando el usuario deshabilita el medidor de nivel durante la recepción (mediante `met_in_rx`). El método `applyLevelMeterReceiveGate()` se llama en cambios de estado de TX y cambios de actividad RADE para asegurar que el medidor se suprima correctamente. El indicador de Compresión ahora muestra la cantidad de compresión como un valor positivo de 0 a 25 dB, invertido a -25 a 0 dB en la cara del indicador.
- En v26.6.1, el applet Phone/CW y sus controles se han actualizado para usar el sistema de temas de la aplicación (`ThemeManager`) para el estilo. Todos los controles deslizantes, etiquetas y botones ahora heredan sus colores del tema activo en lugar de valores fijos. Si ha creado temas personalizados, verifique que los colores de los controles deslizantes y botones estén definidos apropiadamente.

## Solución de problemas

- **El controlador MIDI no es reconocido** — Asegúrese de que el controlador estuviera conectado antes de iniciar AetherSDR. Abra `Settings > MIDI Mapping...` para verificar que el dispositivo esté listado y que las entradas estén asignadas.
- **El accionamiento no activa la TX** — Verifique que **Breakin** esté activo si espera operación QSK. Si **Breakin** está inactivo, el radio espera un PTT manual para transmitir las claves en cola.
- **No se escucha el tono de prueba al accionar** — Confirme que **Sidetone** esté activo y que **Sidetone volume** esté por encima de cero. También verifique que el slice activo esté en modo CW; el subpanel CW solo aparece en modo CW. En v26.5.3, verifique que la salida de audio seleccionada por el usuario esté correctamente configurada en `Settings > Audio Output`.
- **Las paletas iambicas se comportan como manipulador recto** — Confirme que **Iambic** esté activo (resaltado) en el subpanel CW.
- **Los colores del control deslizante o la etiqueta se ven incorrectos después de actualizar** — Esto puede indicar un tema incompleto o incompatible. Vaya a `Settings > Theme` y seleccione un tema incorporado para restablecerlo, o actualice su definición de tema personalizado con las claves de color apropiadas para controles deslizantes y botones.

## Relacionados

- [Enable iambic paddle keying](enable-iambic-paddle-keying.md)
- [Configure break-in OFF so CW keys queue and PTT is manual](configure-break-in-off-so-cw-keys-queue-and-ptt-is-manual.md)
- [Set CW keying speed in WPM](set-cw-keying-speed-in-wpm.md)
- [Set CW break-in delay](set-cw-break-in-delay.md)
- [Enable the low-latency CW sidetone (Sidetone button drives both radio and local path)](enable-the-low-latency-cw-sidetone-sidetone-button-drives-both-radio-and-local-path.md)
- [Change CW pitch / sidetone frequency](change-cw-pitch-sidetone-frequency.md)
