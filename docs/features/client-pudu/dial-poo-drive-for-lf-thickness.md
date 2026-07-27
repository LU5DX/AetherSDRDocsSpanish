# Control Body/Drive para grosor de bajas frecuencias

El mando **Body/Drive** controla la intensidad con la que se excita el saturador o compresor de bajas frecuencias. Al aumentarlo, se añade más grosor en bajas frecuencias y densidad armónica a la banda baja procesada.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en el widget CHAIN para el lado TX o RX que desee ajustar. Consulte [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md).
- Abra el applet: en el contenedor principal Aetherial Audio (TXDSP), localice el subcontenedor **Aetherial TX Voice Processor** o **Aetherial RX Poodoo™**. Si está oculto, haga doble clic en la etapa PUDU del widget CHAIN para abrir el editor correspondiente ("Aetherial Poodoo™ — TX" o "Aetherial Poodoo™ — RX").
- Cuando la etapa PUDU está en bypass, todo el mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. Esto confirma que la etapa no está procesando. Vuelva a habilitar la etapa en el widget CHAIN para restaurar la opacidad completa y el procesamiento activo.

## Pasos

1. Localice el grupo **Body** — la etiqueta del corchete que dice "Body" abarca los tres mandos del lado izquierdo.
2. Encuentre el primer mando debajo de ese corchete, etiquetado **Drive**.
3. Gire **Drive** al valor deseado. El mando muestra el valor actual como `X.X dB`.
4. Para escribir un valor preciso, haga clic en el texto del valor del mando. Aparece un pequeño editor integrado. Escriba el número deseado y presione Enter, o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido. Presione Escape para cancelar la edición y revertir al valor anterior.
5. Suelte el mando. El ajuste se guarda automáticamente.

## Función de cada control

| Control              | Valor predeterminado                                                                          | Rango válido                            |
|----------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------|
| **Poo / Drive** (TX) | 6.0 dB                                                                                        | 0.0 a 24.0 dB                           |
| **Poo / Drive** (RX) | 6.0 dB                                                                                        | 0.0 a 24.0 dB                           |
| Corchete grupo **Body** | Etiqueta del grupo: los tres mandos inferiores pertenecen al procesador de bajas frecuencias (Drive, Tune, Mix). |                                         |
| Logotipo AetherVoice | Logotipo animado de marca que pulsa con el RMS de la señal húmeda. Muestra la marca 'AetherVoice™'. | Widget PooDooLogo — altura mínima 40 píxeles. |
| **Even**             | Selecciona el modelado asimétrico de linaje Aphex — armónicos predominantemente pares, más cálidos, con saturación Big Bottom en LF. | Botón de opción exclusivo con 'Odd'. Al seleccionarlo, el botón se vuelve de color ámbar (color PooDoo). |
| **Odd**              | Selecciona el modelado simétrico tanh de linaje Behringer — armónicos puramente impares, más brillantes, con un compresor de graves feed-forward. | Botón de opción exclusivo con 'Even'. |
| **Poo / Tune**       | 100 Hz                                                                                        | 50 a 160 Hz                             |
| **Poo / Mix**        | 30 %                                                                                          | 0.0 a 1.0 (mostrado como porcentaje)    |
| Corchete grupo **Clarity** | Etiqueta del grupo: los tres mandos inferiores pertenecen al procesador de altas frecuencias (Tune, Air, Mix). |                                         |
| **Doo / Tune**       | 5000 Hz                                                                                       | 1000 a 10000 Hz (mapeo logarítmico)     |
| **Doo / Air**        | 6.0 dB                                                                                        | 0.0 a 24.0 dB                           |
| **Doo / Mix**        | 30 %                                                                                          | 0.0 a 1.0 (mostrado como porcentaje)    |

El mapeo es lineal. Los valores más altos excitan con más intensidad el saturador de bajas frecuencias (modo **Even**) o el compresor de graves (modo **Odd**), produciendo un mayor efecto LF en el mismo nivel de mezcla **Poo / Mix**.

## Consejos

- El logotipo PooDoo pulsa con el RMS de la señal húmeda. Obsérvelo mientras gira **Drive**; un pulso visible en el contenido de graves confirma que la etapa está procesando.
- Cuando la etapa PUDU está en bypass, el mosaico del applet se atenúa al 55 % de opacidad. Este estado visual coincide con la atenuación de la curva EQ utilizada en otras partes de la cadena y no afecta los ajustes guardados.
- En el modo **Even**, los valores altos de Drive activan la saturación Big Bottom de LF de forma más agresiva. En el modo **Odd**, los valores altos de Drive aumentan la compresión de graves feed-forward. Seleccione primero su modo y luego ajuste Drive. Consulte [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md).
- Drive y **Poo / Mix** interactúan. Un Drive alto con un Mix bajo puede proporcionar un procesamiento de graves intenso que se mezcla de forma sutil. Consulte [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md).
- Para enfocar el Drive en una frecuencia específica, ajuste primero **Poo / Tune**. Consulte [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md).
- El editor de valor integrado admite el análisis de números según la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal) y un mecanismo de respaldo que elimina caracteres no numéricos, por lo que añadir texto de unidad como "dB" funciona.
- Los colores de los componentes del mando (anillo de fondo, arco frontal, asa) ahora se leen del espacio de nombres de tema `color.knob.*` dedicado. El contenedor del applet PUDU (`applet/pudu`) puede proporcionar anulaciones de color por applet; el color frontal del mando en PUDU puede diferir de los mandos estándar. Esto no afecta la interacción del usuario.
- Ambos botones de modo (**Even**, **Odd**) ahora utilizan un estilo unificado sin apariencia de botón de edición dedicado. El resaltado ámbar se aplica solo cuando se selecciona un botón de modo.

## Relacionados

- [Aetherial TX Voice Processor / Aetherial RX Poodoo overview](overview.md)
- [Pick Aphex (Even) vs Behringer (Odd) character](pick-aphex-even-vs-behringer-odd-character.md)
- [Tune Poo to the fundamental of your voice (TX) or to bring out RX program lows](tune-poo-to-the-fundamental-of-your-voice-tx-or-to-bring-out-rx-program-lows.md)
- [Blend the Poo enhancement with Mix](blend-the-poo-enhancement-with-mix.md)
- [Bypass PUDU from either chain](bypass-pudu-from-either-chain.md)
