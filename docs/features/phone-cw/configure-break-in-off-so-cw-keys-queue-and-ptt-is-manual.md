# Configurar y desactivar la operación Break-in para que las pulsaciones CW se encolen y el PTT sea manual

Cuando Breakin está DESACTIVADO, los eventos de pulsación CW del teclado y MIDI se encolan y se envían a la radio sin activar automáticamente la transmisión (TX). Usted activa el PTT manualmente para comenzar a transmitir. Utilice esta configuración cuando desee tener control total sobre cuándo el transmisor comienza a transmitir, por ejemplo, durante operaciones de concurso o al usar un amplificador lineal que necesita un secuenciamiento deliberado del PTT.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión activa con la radio.
- Configure el slice activo en un modo CW para que el applet cambie al panel CW. El control Breakin solo es visible en el subpanel CW.

## Pasos

1. Abra el applet Phone/CW. Haga clic en el botón **P/CW** en la barra lateral derecha o confirme que ya está visible en el Panel de Applets.
2. Verifique que se muestre el subpanel CW. Si se muestra el panel Phone, cambie el modo del slice activo a CW en la radio.
3. Localice el botón de alternancia **Breakin** en el subpanel CW.
4. Si **Breakin** está iluminado (activo), haga clic para desactivarlo. El botón aparecerá apagado cuando el break-in esté deshabilitado.
5. Pulse CW usando su teclado o controlador MIDI. Los caracteres se encolan y se envían a la radio, pero la radio no activa TX automáticamente.
6. Presione PTT manualmente para activar el transmisor antes o mientras el keyer envía los caracteres encolados.

## Qué hace cada control

| Control            | Comportamiento                                                                                                                                                                                                                                                                                   | Valor predeterminado                                     |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| **Breakin**         | Alterna entre full break-in (QSK). Cuando está ACTIVADO, los flancos de las pulsaciones disparan TX y el retardo de break-in mantiene el relé abierto entre caracteres. Cuando está DESACTIVADO, los caracteres pulsados se encolan y el PTT debe activarse manualmente.                                                | —                                                        |
| **Delay (CW)**      | Define el tiempo de espera (hang time) del break-in CW — cuánto tiempo permanece activado el relé después del último elemento. Relevante cuando Breakin está ACTIVADO. El control deslizante ajusta de 0 a 2000 ms en pasos de 10 ms. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–2000). | 500 ms                                                   |
| **Speed (CW)**      | Define la velocidad de pulsación CW en palabras por minuto. El control deslizante ajusta de 5 a 100 WPM. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (5–100).                                                                                                            | 20 WPM                                                   |
| **Sidetone**        | Alterna el monitor de sidetone CW. Controla tanto el monitor alimentado por DAX de la radio como el CwSidetoneGenerator local de baja latencia de forma conjunta. El tono y el paneo siguen automáticamente las configuraciones de radio `cw_pitch` y `mon_pan_cw`.                                                | —                                                        |
| **Sidetone volume** | Define el volumen del monitor CW. Controla tanto el volumen del lado de la radio (`mon_gain_cw`) como el volumen del generador de sidetone local de forma conjunta. El control deslizante ajusta de 0 a 100. En la v0.9.8, puede hacer clic en el QLineEdit adyacente y escribir un valor directamente (0–100).                             | 50                                                       |
| **L / R pan (CW)**  | Define el paneo estéreo del monitor CW. Llama a `TransmitModel::setMonPanCw` y aplica un paneo de potencia constante al generador de sidetone local. Haga doble clic para centrar en 50 (centro).                                                                                                       | 50                                                       |
| **Iambic**          | Alterna el keyer de paddle iámbico.                                                                                                                                                                                                                                                              | —                                                        |
| **Pitch < / >**     | Define el tono del sidetone CW. Haga clic en los botones **<** o **>** para aumentar/disminuir en pasos de 10 Hz, o haga clic en el QLineEdit y escriba un valor directamente (100–6000 Hz). Llama a `TransmitModel::setCwPitch`. En la v0.9.8, el QLineEdit acepta entrada directa escrita.                            | 600 Hz                                                   |
| ALC (en el panel Phone)| Muestra la lectura del control automático de nivel (ALC) de MeterModel::swAlcChanged (pico SSB post-ALC de software en dBFS). Se llena de derecha a izquierda: vacío en -20 dBFS, lleno en 0 dBFS.                                                                                             | Cambiado de HWALC (tensión RCA) a medidor SW ALC en la v26.5.1 (#2552). Reflejado por un medidor idéntico en el subpanel CW. |
| ALC (en el panel CW)  | Refleja el medidor ALC del panel Phone; ambos leen de MeterModel::swAlcChanged para obtener lecturas coherentes entre voz y CW.                                                                                                                                                                        | Añadido en la v26.5.1 (#2552) como parte de la división del medidor SW ALC. Utiliza el modo HGauge::setFillFromRight.               |

## Consejos

- Con Breakin DESACTIVADO, no se aplica ningún sobre de PTT automático. La radio no transmitirá los caracteres encolados hasta que usted active el PTT. Suelte el PTT después de que se haya enviado el último carácter para volver a RX.
- Si está utilizando un amplificador externo, Breakin DESACTIVADO le da tiempo para cerrar el relé T/R del amplificador antes de que el keyer comience a enviar.
- Para ajustar cuánto tiempo permanece activado el relé entre caracteres cuando posteriormente vuelva a activar Breakin, use el control deslizante **Delay (CW)** (0–2000 ms) o escriba un valor en el QLineEdit adyacente.

## Solución de problemas

- **La radio transmite inmediatamente cuando se presiona una tecla, incluso con Breakin aparentemente desactivado** — Este era un problema conocido en versiones anteriores a la v0.9.7, donde un sobre de PTT automático anulaba la configuración Breakin. Confirme que AetherSDR esté en la v0.9.7 o posterior.
- **El panel CW no está visible; se muestran los controles Phone** — El applet cambia al subpanel CW automáticamente solo cuando el slice activo está en un modo CW. Cambie el modo del slice a CW en la radio.
- **El control deslizante Delay vuelve atrás después de escribir un valor** — Esto se corrigió en la v0.9.8 (#2428). El valor ahora se almacena en caché inmediatamente para que la emisión de la radio no fuerce el control deslizante a retroceder.

## Relacionados

- [Ajustar el retardo de break-in CW](set-cw-break-in-delay.md)
- [Usar teclado o MIDI para activar llave directa o paddles iámbicos](use-keyboard-or-midi-to-trigger-straight-key-or-iambic-paddles.md)
- [Habilitar la pulsación con paddle iámbico](enable-iambic-paddle-keying.md)
- [Configurar la velocidad de pulsación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Ver controles del applet Phone/CW](view-phone-cw-applet-controls.md)
