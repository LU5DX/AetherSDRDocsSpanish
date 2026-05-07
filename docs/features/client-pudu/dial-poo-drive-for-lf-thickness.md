# Control de cuerpo de graves con Drive

El mando **Body / Drive** controla la intensidad con que se acciona el saturizador o compresor de baja frecuencia. Al aumentarlo, se añade más cuerpo en graves y densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar activada en el widget CHAIN para el lado TX o RX que desee ajustar. Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor principal Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Voice Processor** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU del widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").
- Cuando la etapa PUDU está desviada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto confirma que la etapa no está procesando. Vuelva a activar la etapa en el widget CHAIN para restaurar la opacidad total y el procesamiento activo.

## Pasos

1. Localice el grupo **Poo**: la etiqueta de corchete que dice "Poo" abarca los tres mandos del lado izquierdo.
2. Encuentre el primer mando bajo ese corchete, etiquetado como **Drive**.
3. Gire **Drive** al valor deseado. El mando muestra el valor actual como `X.X dB`.
4. Suelte el mando. El ajuste se guarda automáticamente.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| **Poo / Drive** (TX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduTxPooDriveDb` |
| **Poo / Drive** (RX) | 6.0 dB | 0.0 a 24.0 dB | `ClientPuduRxPooDriveDb` |

La asignación es lineal. Los valores más altos accionan con más fuerza el saturizador de baja frecuencia (modo Even) o el compresor de graves (modo Odd), produciendo un mayor efecto de LF en el mismo nivel de mezcla **Poo / Mix**.

## Consejos

- El logotipo del PooDoo pulsa con el RMS de la señal húmeda. Obsérvelo mientras gira **Drive** — un parpadeo visible en el contenido de graves confirma que la etapa está procesando.
- Cuando la etapa PUDU está desviada, el mosaico del applet se atenúa al 55 % de opacidad. Este estado visual coincide con la atenuación de la curva EQ utilizada en otras partes de la cadena y no afecta a los ajustes guardados.
- En el modo **Even**, los valores altos de Drive activan la saturación Big Bottom de LF de forma más agresiva. En el modo **Odd**, los valores altos de Drive aumentan la compresión de graves feed-forward. Elija primero su modo y luego ajuste Drive. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan. Un Drive alto con un Mix bajo puede proporcionar un procesamiento pesado de graves que se mezcla sutilmente. Consulte [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md).
- Para enfocar el Drive en una frecuencia específica, ajuste primero **Poo / Tune**. Consulte [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
