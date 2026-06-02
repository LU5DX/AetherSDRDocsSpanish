# Control de Drive del Cuerpo para Grosor en Bajas Frecuencias

El control **Body / Drive** ajusta la intensidad con la que se conduce el saturardor o compresor de bajas frecuencias. Incrementarlo añade más grosor en bajas frecuencias y densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado TX o RX que desea ajustar. Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor principal Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Voice Processor** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU en el widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").
- Cuando la etapa PUDU está desviada, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto confirma que la etapa no está procesando. Vuelva a habilitar la etapa en el widget CHAIN para restaurar la opacidad completa y el procesamiento activo.

## Pasos

1. Localice el grupo **Body** — la etiqueta de corchete que dice "Body" abarca los tres controles giratorios del lado izquierdo.
2. Encuentre el primer control giratorio debajo de ese corchete, etiquetado **Drive**.
3. Gire **Drive** al valor deseado. El control muestra el valor actual como `X.X dB`.
4. Para escribir un valor preciso, haga clic en el texto del valor del control. Aparecerá un pequeño editor en línea. Escriba el número deseado y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido. Presione Escape para cancelar la edición y volver al valor anterior.
5. Suelte el control. La configuración se guarda automáticamente.

## Qué hace cada control

| Control                  | Valor predeterminado                                                                    | Rango válido                              |
|--------------------------|-----------------------------------------------------------------------------------------|-------------------------------------------|
| **Poo / Drive** (TX)     | 6.0 dB                                                                                  | 0.0 a 24.0 dB                             |
| **Poo / Drive** (RX)     | 6.0 dB                                                                                  | 0.0 a 24.0 dB                             |
| Corchete del grupo **Body** | Etiqueta de grupo — los tres controles debajo pertenecen al procesador de bajas frecuencias (Drive, Tune, Mix). |                                           |
| Logotipo AetherVoice     | Logotipo animado de marca que late con el RMS de la señal húmeda. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima de 40 px. |
| **Even**                 | Selecciona la conformación asimétrica de la línea Aphex — armónicos predominantemente pares, más cálidos, con saturación Big Bottom en bajas frecuencias. | Botón de opción exclusivo con 'Odd'. |
| **Odd**                  | Selecciona la conformación simétrica tanh de la línea Behringer — armónicos puramente impares, más brillantes, con un compresor de graves feed-forward. | Botón de opción exclusivo con 'Even'. |
| **Poo / Tune**           | 100 Hz                                                                                  | 50 a 160 Hz                              |
| **Poo / Mix**            | 30 %                                                                                    | 0.0 a 1.0 (mostrado como porcentaje)     |
| **Doo / Tune**           | 5000 Hz                                                                                 | 1000 a 10000 Hz (mapeo logarítmico)      |
| **Doo / Air**            | 6.0 dB                                                                                  | 0.0 a 24.0 dB                            |
| **Doo / Mix**            | 30 %                                                                                    | 0.0 a 1.0 (mostrado como porcentaje)     |
| Corchete del grupo **Clarity** | Etiqueta de grupo — los tres controles debajo pertenecen al procesador de altas frecuencias (Tune, Air, Mix). |                                           |

El mapeo es lineal. Los valores más altos conducen más intensamente el saturardor de bajas frecuencias (modo **Even**) o el compresor de graves (modo **Odd**), produciendo un mayor efecto en bajas frecuencias con el mismo nivel de mezcla **Poo / Mix**.

## Consejos

- El logotipo PooDoo late con el RMS de la señal húmeda. Obsérvelo mientras gira **Drive**: un latido visible en el contenido de graves confirma que la etapa está procesando.
- Cuando la etapa PUDU está desviada, el mosaico del applet se atenúa al 55 % de opacidad. Este estado visual coincide con la atenuación de la curva EQ utilizada en otras partes de la cadena y no afecta las configuraciones guardadas.
- En el modo **Even**, los valores altos de Drive activan la saturación Big Bottom en bajas frecuencias de forma más agresiva. En el modo **Odd**, los valores altos de Drive aumentan la compresión de graves feed-forward. Primero elija su modo, luego ajuste Drive. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan. Un Drive alto con un Mix bajo puede proporcionar un procesamiento intenso de graves que se mezcla sutilmente. Consulte [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md).
- Para centrar el Drive en una frecuencia específica, ajuste primero **Poo / Tune**. Consulte [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).
- El editor de valores en línea admite el análisis de números con reconocimiento de configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal) y un mecanismo de respaldo que elimina caracteres no numéricos, por lo que agregar texto de unidad como "dB" funciona.
- Los colores del componente del control giratorio (anillo de fondo, arco de primer plano, mango) ahora se leen del espacio de nombres de tema dedicado `color.knob.*`. El contenedor del applet PUDU (`applet/pudu`) puede proporcionar anulaciones de color por applet — el primer plano del control en PUDU puede diferir de los controles estándar. Esto no afecta la interacción del usuario.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
