# Configurar break-in en OFF para que las pulsaciones CW se encolen y el PTT sea manual

Cuando el break-in está en OFF, los eventos de teclado CW y de controlador MIDI se encolan y se envían a la radio sin activar TX de forma automática. El PTT se activa manualmente para comenzar a transmitir. Use esta configuración cuando desee control total sobre el momento en que el transmisor transmite — por ejemplo, durante operación en concurso o cuando utiliza un amplificador lineal que requiere una secuencia de PTT deliberada.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión activa con la radio.
- Establezca el slice activo en un modo CW para que el applet cambie al panel CW. El control de break-in solo es visible en el subpanel CW.

## Pasos

1. Abra el applet Phone/CW. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha, o confirme que ya está visible en el Panel de Applets.
2. Verifique que se muestre el subpanel CW. Si en cambio se muestra el panel Phone, cambie el modo del slice activo a CW en la radio.
3. Localice el botón de alternancia **Breakin** en el subpanel CW.
4. Si **Breakin** está encendido (activo), haga clic en él para desactivarlo. El botón aparecerá apagado cuando el break-in esté deshabilitado.
5. Manipule CW con su teclado o controlador MIDI. Los caracteres se encolan y se envían a la radio, pero la radio no activa TX de forma automática.
6. Presione PTT manualmente para activar el transmisor antes o mientras el manipulador envía los caracteres encolados.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Breakin** | Alterna el break-in completo (QSK). Cuando está en ON, los flancos de manipulación activan TX y el retardo de break-in mantiene el relé abierto entre caracteres. Cuando está en OFF, los caracteres manipulados se encolan y el PTT debe activarse manualmente. | — | On / Off | — |
| **Delay (CW)** | Establece el tiempo de retención del break-in CW — cuánto tiempo permanece activado el relé después del último elemento. Relevante cuando Breakin está en ON. | — | 0–2000 ms (paso 10) | — |

## Consejos

- Con Breakin en OFF no se aplica ningún envolvente de PTT automático. La radio no transmitirá los caracteres encolados hasta que usted active PTT. Suelte PTT después de que el último carácter haya sido enviado para volver a RX.
- Si utiliza un amplificador externo, Breakin en OFF le da tiempo para cerrar el relé T/R del amplificador antes de que el manipulador comience a enviar.
- Para ajustar cuánto tiempo permanece activado el relé entre caracteres cuando vuelva a activar Breakin en ON, use el deslizador **Delay (CW)** (0–2000 ms).

## Solución de problemas

- **La radio transmite inmediatamente al presionar una tecla aunque Breakin parece estar en OFF** — Este era un problema conocido en versiones anteriores a v0.9.7, en las que un envolvente de PTT automático ignoraba la configuración de Breakin. Confirme que AetherSDR está en la versión v0.9.7 o posterior.
- **El panel CW no es visible; se muestran los controles de Phone en su lugar** — El applet cambia al panel CW automáticamente solo cuando el slice activo está en un modo CW. Cambie el modo del slice a CW en la radio.

## Relacionados

- [Establecer el retardo de break-in CW](set-cw-break-in-delay.md)
- [Usar teclado o MIDI para activar manipulador recto o paletas iámbicas](use-keyboard-or-midi-to-trigger-straight-key-or-iambic-paddles.md)
- [Habilitar manipulación con paleta iámbica](enable-iambic-paddle-keying.md)
- [Establecer la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
