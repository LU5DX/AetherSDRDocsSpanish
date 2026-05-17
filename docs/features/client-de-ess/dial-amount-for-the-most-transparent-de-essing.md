# Cantidad para un des-esser lo más transparente posible

El mando Amount establece la atenuación máxima que aplica el des-esser cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto permite domar la aspereza sin que el audio suene procesado o bombeado.

## Antes de empezar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. La applet permanece oculta hasta que la etapa esté activa.
- Abra la applet Aetherial De-Esser a través de la Aetherial Audio Channel Strip. El editor flotante (antes accesible haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en la applet.
- Ajuste primero Freq y Thresh para que el des-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md) y [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Pida a alguien que transmita por el micrófono — o lea una frase con sibilantes en voz alta — para que el des-esser se active.
2. Observe la barra Gain-reduction. Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca señala el punto de −6 dB.
3. Gire el mando Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que la aspereza desaparezca.
4. Retroceda en sentido horario hasta que la barra Gain-reduction solo alcance la marca de −6 dB en los picos de "S" más fuertes. Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra Gain-reduction llega al tope cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pasos pequeños hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Edición inline de valores

Cada mando en la applet Aetherial De-Esser admite entrada numérica directa. Haga clic en la etiqueta de valor del mando para abrir un pequeño editor de texto superpuesto. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido del mando.

- El editor acepta formatos numéricos según la configuración regional (p. ej., "12,5" en locales con coma decimal).
- Si escribe texto adicional (p. ej., "12.5 ms" o "−6 dB"), el editor elimina los caracteres no numéricos y analiza el número.
- Presione Escape para cancelar la edición y volver al valor anterior.
- La rueda del ratón sigue funcionando mientras el editor está enfocado, reenviándose al mando para ajuste.
- Cuando no está enfocado, el editor aparece idéntico a una etiqueta de valor pintada — un sutil borde oscuro interior y un borde cian aparecen al enfocarse para indicar el modo de edición.

## Qué hace cada control

| Control                     | Por defecto | Rango válido   | Comportamiento                                                                                                                                                    |
|-----------------------------|-------------|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta sidechain | —           | —              | Respuesta del filtro paso banda con un punto móvil en la frecuencia central. En modo compacto, sin etiquetas de eje; en modo completo muestra etiquetas de frecuencia (100, 500, 1k, 2k, 3k, 4k, 5k, 6k, 8k, 10k, 12k). |
| Barra Gain-reduction        | —           | 0 a 24 dB GR   | Franja horizontal rojo suave, relleno desde la derecha. La escala llega a 24 dB; una marca señala los −6 dB típicos. Se actualiza a ~30 Hz.                       |
| Freq                        | 6000 Hz     | 1000 a 12000 Hz| Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. Etiqueta '6.0 kHz' por encima de 1 kHz, 'N Hz' por debajo.                          |
| Q                           | 2,00        | 0,5 a 5,0      | Mapeo lineal. Establece el ancho de banda — Q más alto = banda más estrecha. Etiqueta 'X.XX'.                                                                     |
| Thresh                      | −30,0 dB    | −60,0 a 0,0 dB | Mapeo lineal. Nivel por encima del cual el des-esser comienza a atenuar.                                                                                          |
| Amount                      | −6,0 dB     | −24,0 a 0,0 dB | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción.                               |
| Attack                      | 1,0 ms      | 0,1 a 30,0 ms  | Mapeo exponencial (0,1 × 300^n). Establece la velocidad de respuesta. Presente solo en el panel StripDeEssPanel de la Channel Strip. La applet acoplada omite este mando. |
| Release                     | 100 ms      | 10,0 a 500,0 ms| Mapeo exponencial (10 × 50^n). Establece la velocidad de retorno. Presente solo en el panel StripDeEssPanel de la Channel Strip. La applet acoplada omite este mando. |

## Curva de respuesta sidechain

El indicador de curva de respuesta sidechain muestra la respuesta del filtro paso banda con un punto móvil en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas de eje usan `QStaticText` para un renderizado eficiente y muestran frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Applet Panel acoplado. Se abre desde la cadena TX en la Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Se accede a través del lado RX de la Aetherial Audio Channel Strip. Usa su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc.

## Atenuación por bypass

Cuando la etapa DESS está en bypass mediante un solo clic en el widget CHAIN, toda la applet se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación usado en la curva del ecualizador y proporciona una clara indicación visual de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para re-habilitar la etapa y restaurar la opacidad completa.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra Gain-reduction señala este nivel, facilitando su uso como referencia durante el ajuste.
- Busque que la barra Gain-reduction se mueva notablemente en los sonidos "S" y "T", pero que nunca llegue al tope de 24 dB. Una reducción de ganancia intensa en ese extremo es audible como un ceceo o una caída de volumen.
- Estrechar la banda sidechain con Q antes de finalizar Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero — representan reducción, no aumento.
- Use la edición inline de valores para una entrada numérica precisa en lugar de ajustar girando el mando.

## Solución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra Gain-reduction nunca se mueve** — El des-esser no se está disparando. Verifique que Thresh esté ajustado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra Gain-reduction llega constantemente al tope de 24 dB** — Thresh está demasiado bajo, lo que hace que el des-esser se dispare en todo el habla, no solo en sibilancias. Suba Thresh primero, luego reevalúe Amount.
- **La applet aparece atenuada u opaca** — La etapa DESS está en bypass. Haga clic una vez en la etapa en el widget CHAIN para re-habilitarla.
- **El editor inline no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del mando. Los valores fuera de rango se limitan automáticamente. Si el valor se revierte, verifique si hay espacios adicionales o caracteres que no se hayan eliminado.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
- [Aetherial De-Esser overview](overview.md)
