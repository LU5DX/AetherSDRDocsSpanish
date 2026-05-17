# Control Body/Drive para espesor de baja frecuencia

El control **Body/Drive** determina la intensidad con la que se excita el saturante o compresor de baja frecuencia. Aumentarlo añade más espesor de baja frecuencia y densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado TX o RX que desea ajustar. Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor padre Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Voice Processor** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").
- Cuando la etapa PUDU está desviada, el mosaico completo del applet se atenúa aproximadamente al 55 % de opacidad. Esto confirma que la etapa no está procesando. Vuelva a habilitar la etapa en el widget CHAIN para restaurar la opacidad total y el procesamiento activo.

## Pasos

1. Localice el grupo **Body** — la etiqueta de corchete que dice "Body" abarca los tres controles izquierdos.
2. Encuentre el primer control debajo de ese corchete, etiquetado **Drive**.
3. Gire **Drive** hasta el valor deseado. El control muestra el valor actual como `X.X dB`.
4. Para escribir un valor exacto, haga clic en el texto del valor del control. Aparecerá un pequeño editor en línea. Escriba el número deseado y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido. Presione Escape para cancelar la edición y revertir al valor anterior.
5. Suelte el control. El ajuste se guarda automáticamente.

## Qué hace cada control

| Control                         | Valor predeterminado | Rango válido        |
|---------------------------------|----------------------|---------------------|
| **Poo / Drive** (TX)            | 6.0 dB               | 0.0 a 24.0 dB       |
| **Poo / Drive** (RX)            | 6.0 dB               | 0.0 a 24.0 dB       |
| Corchete del grupo **Body**     | Etiqueta de grupo — los tres controles inferiores pertenecen al procesador de baja frecuencia (Drive, Tune, Mix). | |
| Logotipo AetherVoice            | Logotipo animado de marca que pulsa con el RMS de la señal húmeda. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |

El mapeo es lineal. Los valores más altos excitan con más fuerza el saturante de baja frecuencia (modo Even) o el compresor de graves (modo Odd), produciendo un mayor efecto de baja frecuencia al mismo nivel de mezcla **Poo / Mix**.

## Consejos

- El logotipo PooDoo pulsa con el RMS de la señal húmeda. Observe mientras gira **Drive** — la pulsación visible en el contenido de graves confirma que la etapa está procesando.
- Cuando la etapa PUDU está desviada, el mosaico del applet se atenúa al 55 % de opacidad. Este estado visual coincide con el atenuación de la curva EQ utilizada en otras partes de la cadena y no afecta los ajustes guardados.
- En el modo **Even**, los valores altos de Drive activan la saturación de baja frecuencia Big Bottom de forma más agresiva. En el modo **Odd**, los valores altos de Drive aumentan la compresión de graves feed-forward. Elija primero su modo, luego ajuste Drive. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan. Un Drive alto con un Mix bajo puede proporcionar un procesamiento intenso de baja frecuencia que se mezcla sutilmente. Consulte [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md).
- Para enfocar Drive en una frecuencia específica, ajuste **Poo / Tune** primero. Consulte [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).
- El editor de valores en línea admite el análisis numérico sensible a la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal) y un método alternativo que elimina caracteres no numéricos, por lo que agregar texto de unidad como "dB" funciona.

## Relacionado

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
