# Cantidad de atenuación para un de-essing más transparente

El mando Amount establece la atenuación máxima que aplica el de-esser cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto le permite controlar la aspereza sin que el audio suene procesado o comprimido.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser a través de Aetherial Audio Channel Strip. El editor flotante (anteriormente accesible haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en el applet.
- Ajuste primero Freq y Thresh para que el de-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Pida a alguien que transmita por el micrófono — o lea una frase con muchas eses en voz alta — para que el de-esser esté disparando activamente.
2. Observe la barra de Gain-reduction. Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca señala el punto de −6 dB.
3. Gire el mando Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra de Gain-reduction solo alcance la marca de −6 dB en los picos de "S" más fuertes. Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de Gain-reduction está fija cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pasos pequeños hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Edición de valor en línea

Cada mando en el applet Aetherial De-Esser admite entrada numérica directa. Haga clic en la etiqueta de valor del mando para abrir un pequeño editor de texto superpuesto. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido del mando.

- El editor acepta formatos numéricos según la configuración regional (por ejemplo, "12,5" en configuraciones con coma decimal).
- Si escribe texto adicional (por ejemplo, "12.5 ms" o "−6 dB"), el editor elimina los caracteres no numéricos y analiza el número.
- Presione Escape para cancelar la edición y volver al valor anterior.
- La rueda del ratón sigue funcionando mientras el editor está enfocado, reenviándose al mando para ajuste.
- Cuando no está enfocado, el editor se ve idéntico a una etiqueta de valor pintada — un sutil borde oscuro interior y un borde cian aparecen al enfocarse para indicar el modo de edición.

## Función de cada control

| Control                        | Predeterminado                                                                                                                                                                                    | Rango válido                                                                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de respuesta de sidechain | —                                                                                                                                                                                                 | —                                                                                                                                                                              |
| Barra de Gain-reduction        | —                                                                                                                                                                                                 | 0 a 24 dB GR                                                                                                                                                                   |
| Freq                           | 6000 Hz                                                                                                                                                                                           | 1000 a 12000 Hz                                                                                                                                                                |
| Q                              | 2.00                                                                                                                                                                                              | 0,5 a 5,0                                                                                                                                                                      |
| Thresh                         | −30.0 dB                                                                                                                                                                                          | −60.0 a 0.0 dB                                                                                                                                                                 |
| Amount                         | −6.0 dB                                                                                                                                                                                           | −24.0 a 0.0 dB                                                                                                                                                                 |
| Attack (solo en channel strip) | 1.0 ms                                                                                                                                                                                            | 0,1 a 30,0 ms                                                                                                                                                                  |
| Release (solo en channel strip)| 100 ms                                                                                                                                                                                            | 10.0 a 500.0 ms                                                                                                                                                                |
| Slope                          | 24 dB/oct (2 etapas)                                                                                                                                                                              | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas)                                                                                                                                       |

## Curva de respuesta de sidechain

El indicador de curva de respuesta de sidechain muestra la respuesta del filtro paso banda con un punto móvil en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas de eje usan `QStaticText` para un renderizado eficiente y muestran frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

## Control de Slope

Un botón Slope aparece en la parte inferior de la columna izquierda de mandos en Aetherial Audio Channel Strip (paneles TX y RX). Recorre 12 → 24 → 36 → 48 dB/oct (1 a 4 biquads paso banda en cascada) cada vez que hace clic en él.

- Mayor pendiente = muesca más estrecha alrededor de la frecuencia sibilante = menos atenuación colateral en mid-band en frases con muchas eses.
- El botón muestra el valor actual como "N dB/oct" (por ejemplo, "24 dB/oct").
- El ajuste se guarda por separado para TX y RX como `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

Para ajustar la pendiente:

1. Haga clic repetidamente en el botón Slope para recorrer los valores disponibles.
2. Observe la curva de respuesta de sidechain actualizarse en tiempo real para ver la muesca estrechada.
3. Deténgase cuando el de-esser apunte solo a la sibilancia sin afectar la energía cercana del habla.

**Nota:** El applet Aetherial De-Esser acoplado omite los controles Attack, Release y Slope. Estos solo están disponibles en el panel Aetherial Audio Channel Strip.

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Applet Panel acoplado. Se abre desde la cadena TX en Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Accesible a través del lado RX de Aetherial Audio Channel Strip. Usa su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc. El botón Slope en el panel RX usa `ClientDeEssRxSlopeStages`.

## Atenuación por bypass

Cuando la etapa DESS se omite con un solo clic en el widget CHAIN, todo el applet se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para re-activar la etapa y restaurar la opacidad completa.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra de Gain-reduction señala este nivel, lo que facilita su uso como referencia durante el ajuste.
- Procure que la barra de Gain-reduction se mueva notablemente en los sonidos "S" y "T", pero que nunca llegue al extremo de 24 dB. Una reducción de ganancia intensa en ese extremo se escucha como un ceceo o una caída de audio.
- Estrechar la banda de sidechain con Q antes de finalizar Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Estreche o ensanche la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount son siempre negativos o cero — representan reducción, no aumento.
- Use la edición de valor en línea para una entrada numérica precisa en lugar de ajustar finamente girando el mando.
- Ajuste Slope para apretar la muesca de sidechain — esto preserva la energía de mid-band mientras corta agresivamente las sibilantes.

## Solución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra de Gain-reduction nunca se mueve** — El de-esser no está disparando. Verifique que Thresh esté ajustado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de Gain-reduction se fija constantemente en 24 dB** — Thresh está demasiado bajo, lo que hace que el de-esser se dispare con todo el habla, no solo con la sibilancia. Suba Thresh primero y luego re-evalúe Amount.
- **El applet se ve desvaído o atenuado** — La etapa DESS está en bypass. Haga clic una vez en la etapa en el widget CHAIN para re-activarla.
- **El editor en línea no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del mando. Los valores fuera de rango se limitan automáticamente. Si el valor se revierte, verifique que no haya espacios adicionales o caracteres que no se hayan eliminado.
- **El habla de mid-band suena sorda o atenuada** — Slope puede estar demasiado bajo. Aumente Slope a 36 o 48 dB/oct para estrechar la muesca de sidechain y preservar la energía de mid-band.

## Relacionados

- [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estreche o ensanche la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la GR en vivo mientras lee una frase con sibilancia](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omita el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Descripción general de Aetherial De-Esser](overview.md)
