# Configurar el break-in desactivado para que las teclas CW se encolen y el PTT sea manual

Cuando el Breakin (break-in) está DESACTIVADO, los eventos de teclado CW y MIDI se encolan y se envían al equipo sin activar la transmisión automáticamente. Usted activa el PTT manualmente para comenzar a transmitir. Use esta opción cuando desee tener control total sobre cuándo el transmisor se activa, por ejemplo, durante concursos o cuando utiliza un amplificador lineal que necesita una secuencia de PTT deliberada.

## Antes de comenzar

- Conéctese a un equipo FLEX-8600. El applet Phone/CW requiere una conexión activa al equipo.
- Configure el slice activo en un modo CW para que el applet cambie al panel CW. El control Breakin solo es visible en el subpanel CW.

## Pasos

1. Abra el applet Phone/CW. Haga clic en el botón de la bandeja **P/CW** en la barra lateral derecha, o confirme que ya está visible en el Panel de Applets.
2. Verifique que se muestre el subpanel CW. Si en su lugar se muestra el panel Phone, cambie el modo del slice activo a CW en el equipo.
3. Localice el botón de alternancia **Breakin** en el subpanel CW.
4. Si **Breakin** está iluminado (activo), haga clic en él para desactivarlo. El botón aparecerá sin iluminar cuando el break-in esté deshabilitado.
5. Teclee CW usando su teclado o controlador MIDI. Los caracteres se encolan y se envían al equipo, pero el equipo no activa la transmisión automáticamente.
6. Presione PTT manualmente para activar el transmisor antes o mientras el keyer envía los caracteres encolados.

## Qué hace cada control

| Control                | Comportamiento                                                                                                                                                                                                                                                                                                                            | Valor predeterminado |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Breakin**            | Alterna el break-in completo (QSK). Cuando está ACTIVADO, los flancos de la tecla activan la transmisión y el retardo de break-in mantiene el relé abierto entre caracteres. Cuando está DESACTIVADO, los caracteres tecleados se encolan y se debe activar el PTT manualmente.                                                           | —                    |
| **Delay (CW)**         | Establece el tiempo de retención del break-in CW: cuánto tiempo permanece activado el relé después del último elemento. Relevante cuando Breakin está ACTIVADO. El control deslizante se ajusta de 0 a 2000 ms en pasos de 10 ms. En v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–2000).       | 500 ms               |
| **Speed (CW)**         | Establece la velocidad de tecleo CW en palabras por minuto. El control deslizante se ajusta de 5 a 100 WPM. En v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (5–100).                                                                                                                                | 20 WPM               |
| **Sidetone**           | Alterna el monitor de tono lateral CW. Controla tanto el monitor alimentado por DAX del equipo como el generador de tono lateral de baja latencia del lado del cliente de forma sincronizada. El tono y la panorámica siguen automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del equipo.                                            | —                    |
| **Sidetone volume**    | Establece el volumen del monitor CW. Controla tanto el volumen del lado del equipo (`mon_gain_cw`) como el del tono lateral del lado del cliente de forma sincronizada. El control deslizante se ajusta de 0 a 100. En v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–100).                       | 50                   |
| **L / R pan (CW)**     | Establece la panorámica estéreo del monitor CW. Llama a `TransmitModel::setMonPanCw` y aplica una panorámica de potencia constante al generador de tono lateral local. Haga doble clic para volver a centrar en 50 (centro).                                                                                                              | 50                   |
| **Iambic**             | Alterna el keyer de paleta iámbica.                                                                                                                                                                                                                                                                                                       | —                    |
| **Pitch < / >**        | Establece el tono del tono lateral CW. Haga clic en los botones **<** o **>** para ajustar en pasos de 10 Hz, o haga clic en el QLineEdit y escriba un valor directamente (100–6000 Hz). Llama a `TransmitModel::setCwPitch`. En v0.9.8, el QLineEdit acepta la entrada directa escrita.                                                    | 600 Hz               |

## Consejos

- Con Breakin DESACTIVADO, no se aplica ningún sobre de PTT automático. El equipo no transmitirá los caracteres encolados hasta que usted active el PTT. Suelte el PTT después de que se haya enviado el último carácter para volver a recepción.
- Si utiliza un amplificador externo, Breakin DESACTIVADO le da tiempo para cerrar el relé T/R del amplificador antes de que el keyer comience a enviar.
- Para ajustar cuánto tiempo permanece activado el relé entre caracteres cuando luego vuelva a activar Breakin, use el control deslizante **Delay (CW)** (0–2000 ms) o escriba un valor en el QLineEdit adyacente.

## Solución de problemas

- **El equipo transmite inmediatamente al presionar una tecla aunque Breakin parezca desactivado** — Este era un problema conocido en versiones anteriores a v0.9.7, donde un sobre de PTT automático anulaba la configuración de Breakin. Confirme que AetherSDR sea v0.9.7 o posterior.
- **El panel CW no es visible; se muestran los controles Phone** — El applet cambia al panel CW automáticamente solo cuando el slice activo está en un modo CW. Cambie el modo del slice a CW en el equipo.
- **El control deslizante Delay vuelve a su posición después de escribir un valor** — Esto se corrigió en v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión del equipo no devuelva el control deslizante a su posición anterior.

## Relacionado

- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Usar el teclado o MIDI para activar tecla recta o paletas iámbicas](use-keyboard-or-midi-to-trigger-straight-key-or-iambic-paddles.md)
- [Habilitar el tecleo con paleta iámbica](enable-iambic-paddle-keying.md)
- [Establecer la velocidad de tecleo CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Ver los controles del applet Phone/CW](view-phone-cw-applet-controls.md)
