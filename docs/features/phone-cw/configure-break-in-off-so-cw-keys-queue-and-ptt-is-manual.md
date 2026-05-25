# Configurar y desactivar el modo Break-in para que las teclas CW se pongan en cola y el PTT sea manual

Cuando Breakin está APAGADO, los eventos de tecla CW del teclado y MIDI se ponen en cola y se envían al radio sin activar automáticamente la transmisión (TX). Usted activa el PTT manualmente para comenzar a transmitir. Utilice esta configuración cuando desee un control total sobre cuándo se activa el transmisor, por ejemplo, durante operaciones de concurso o al usar un amplificador lineal que necesita un secuenciamiento deliberado del PTT.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión activa con el radio.
- Configure el slice activo en un modo CW para que el applet cambie al panel CW. El control Breakin solo es visible en el subpanel CW.

## Pasos

1. Abra el applet Phone/CW. Haga clic en el botón **P/CW** en la barra lateral derecha o confirme que ya está visible en el Panel de Applets.
2. Verifique que se esté mostrando el subpanel CW. Si se muestra el panel Phone, cambie el modo del slice activo a CW en el radio.
3. Localice el botón de alternancia **Breakin** en el subpanel CW.
4. Si **Breakin** está encendido (activo), haga clic para desactivarlo. El botón aparecerá apagado cuando el break-in esté deshabilitado.
5. Telegrafíe CW usando su teclado o controlador MIDI. Los caracteres se ponen en cola y se envían al radio, pero el radio no activa TX automáticamente.
6. Presione PTT manualmente para activar el transmisor antes o mientras el keyer envía los caracteres en cola.

## Qué hace cada control

| Control            | Comportamiento                                                                                                                                                                                                                                                                                   | Predeterminado                                           |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| **Breakin**         | Alterna entre full break-in (QSK). Cuando está ENCENDIDO, los bordes de las teclas disparan TX y el retardo de break-in mantiene el relé abierto entre caracteres. Cuando está APAGADO, los caracteres tecleados se ponen en cola y el PTT debe activarse manualmente.                                                | —                                                        |
| **Delay (CW)**      | Define el tiempo de espera (hang time) del break-in CW — cuánto tiempo permanece el relé activado después del último elemento. Relevante cuando Breakin está ENCENDIDO. El control deslizante ajusta de 0 a 2000 ms en pasos de 10 ms. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–2000). | 500 ms                                                   |
| **Speed (CW)**      | Define la velocidad de telegrafía CW en palabras por minuto. El control deslizante ajusta de 5 a 100 WPM. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (5–100).                                                                                                            | 20 WPM                                                   |
| **Sidetone**        | Alterna el monitor de sidetone CW. Controla tanto el monitor alimentado por DAX del radio como el CwSidetoneGenerator local de baja latencia en conjunto. El tono y el pan siguen automáticamente las configuraciones `cw_pitch` y `mon_pan_cw` del radio. En la v26.5.3, el sidetone CW se enruta a la salida de audio seleccionada por el usuario en lugar de la salida predeterminada (#2899). | —                                                        |
| **Sidetone volume** | Define el volumen del monitor CW. Controla tanto el volumen del lado del radio (`mon_gain_cw`) como el volumen del generador de sidetone local en conjunto. El control deslizante ajusta de 0 a 100. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–100).                             | 50                                                       |
| **L / R pan (CW)**  | Define el paneo estéreo del monitor CW. Llama a `TransmitModel::setMonPanCw` y aplica paneo de potencia constante al generador de sidetone local. Haga doble clic para centrar en 50 (centro).                                                                                                       | 50                                                       |
| **Iambic**          | Alterna el keyer de paddle iámbico.                                                                                                                                                                                                                                                              | —                                                        |
| **Pitch < / >**     | Define el tono del sidetone CW. Haga clic en los botones **<** o **>** para aumentar/disminuir en pasos de 10 Hz, o haga clic en el QLineEdit y escriba un valor directamente (100–6000 Hz). Llama a `TransmitModel::setCwPitch`. En la v0.9.8, el QLineEdit acepta entrada directa escrita.                            | 600 Hz                                                   |
| ALC (en el panel Phone) | Muestra la lectura del control automático de nivel (ALC) de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío a -20 dBFS, lleno a 0 dBFS. En la v26.5.3, el medidor ALC se inicializa inmediatamente a -20 dBFS al inicio. | Cambiado de HWALC (tensión RCA) a medidor SW ALC en la v26.5.1 (#2552). Reflejado por un medidor idéntico en el subpanel CW. |
| ALC (en el panel CW)  | Refleja el medidor ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para lecturas consistentes entre voz y CW. En la v26.5.3, el medidor ALC se inicializa inmediatamente a -20 dBFS al inicio. | Añadido en la v26.5.1 (#2552) como parte de la división del medidor SW ALC. Usa el modo HGauge::setFillFromRight.               |
| **Compression**     | Muestra la cantidad de compresión de habla en dB a través de la lectura COMPPEAK de MeterModel. En la v26.5.3, la compresión se muestra como un valor positivo de 0 a 25 dB (0 = sin compresión, 25 = compresión total), invertido a -25 a 0 dB en la cara del medidor. | —                                                        |
| **Level**           | Muestra el nivel de pico del micrófono en dBFS. En la v26.5.3, el nivel del micrófono se suprime durante la recepción cuando la opción "Medidor de nivel durante recepción" está desactivada, independientemente de la fuente del micrófono. | —                                                        |

## Consejos

- Con Breakin APAGADO, no se aplica ningún sobre de PTT automático. El radio no transmitirá los caracteres en cola hasta que usted active el PTT. Suelte el PTT después de que se envíe el último carácter para volver a RX.
- Si está usando un amplificador externo, Breakin APAGADO le da tiempo para cerrar el relé T/R del amplificador antes de que el keyer comience a enviar.
- Para ajustar cuánto tiempo permanece el relé activado entre caracteres cuando posteriormente vuelva a encender Breakin, use el control deslizante **Delay (CW)** (0–2000 ms) o escriba un valor en el QLineEdit adyacente.
- En la v26.5.3, el sidetone CW se enruta automáticamente al dispositivo de salida de audio seleccionado en las configuraciones de Audio de AetherSDR, ya no a la salida predeterminada del sistema. Verifique su selección de salida de audio si no escucha sidetone.

## Solución de problemas

- **El radio transmite inmediatamente cuando se presiona una tecla, incluso con Breakin aparentemente apagado** — Este era un problema conocido en versiones anteriores a la v0.9.7, donde un sobre de PTT automático anulaba la configuración Breakin. Confirme que AetherSDR esté en la v0.9.7 o posterior.
- **El panel CW no está visible; se muestran los controles Phone** — El applet cambia al subpanel CW automáticamente solo cuando el slice activo está en un modo CW. Cambie el modo del slice a CW en el radio.
- **El control deslizante Delay vuelve después de escribir un valor** — Esto se corrigió en la v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión del radio no fuerce el control deslizante a retroceder.
- **El medidor ALC muestra una lectura congelada** — En la v26.5.3, el medidor ALC se inicializa a -20 dBFS en la construcción. Si la lectura permanece en -20 dBFS, verifique que el radio esté transmitiendo y que haya una señal de audio presente.
- **El medidor de nivel del micrófono muestra -150 dBFS durante la recepción** — En la v26.5.3, el medidor de nivel se suprime durante la recepción cuando la opción "Medidor de nivel durante recepción" está desactivada en las configuraciones de TransmitModel. Para ver el nivel del micrófono durante la recepción, active esa opción.
- **No escucho sidetone CW** — En la v26.5.3, verifique que la salida de audio correcta esté seleccionada en las configuraciones de Audio de AetherSDR. El sidetone ahora se enruta a la salida de audio del usuario, no a la salida predeterminada del sistema (#2899).

## Relacionados

- [Ajustar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Usar teclado o MIDI para activar llave recta o paletas iámbicas](use-keyboard-or-midi-to-trigger-straight-key-or-iambic-paddles.md)
- [Habilitar telegrafía iámbica de paleta](enable-iambic-paddle-keying.md)
- [Definir velocidad de telegrafía CW en WPM](set-cw-keying-speed-in-wpm.md)
- Ver controles del applet Phone/CW
