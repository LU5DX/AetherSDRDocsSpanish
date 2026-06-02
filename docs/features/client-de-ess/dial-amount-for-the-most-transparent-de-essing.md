# Ajuste de Cantidad para un de-essing más transparente

El control Amount ajusta la atenuación máxima que aplica el de-esser cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto permite domar la aspereza sin que el audio suene procesado o con bombeo.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser desde el Aetherial Audio Channel Strip. El editor flotante (accesible anteriormente haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en el applet.
- Ajuste primero Freq y Thresh para que el de-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Pida a alguien que transmita con el micrófono — o lea una frase con muchas "eses" en voz alta — para que el de-esser se active.
2. Observe la barra de Gain-reduction. Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca señala el punto de −6 dB.
3. Gire el control Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que la aspereza desaparezca.
4. Retroceda en sentido horario hasta que la barra de Gain-reduction solo alcance la marca de −6 dB en los picos más fuertes de "S". Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de Gain-reduction se queda fija cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pasos pequeños hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Edición de valor en línea

Cada control del applet Aetherial De-Esser admite entrada numérica directa. Haga clic en la etiqueta de valor del control para abrir un editor de texto pequeño superpuesto. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se limita automáticamente al rango válido del control.

- El editor acepta formatos numéricos según la configuración regional (por ejemplo, "12,5" en regiones que usan coma decimal).
- Si escribe texto adicional (p. ej., "12.5 ms" o "−6 dB"), el editor elimina los caracteres no numéricos y analiza el número.
- Presione Escape para cancelar la edición y volver al valor anterior.
- La rueda del ratón sigue funcionando mientras el editor está enfocado, y se transmite al control para su ajuste.
- Cuando no está enfocado, el editor se ve idéntico a una etiqueta de valor pintada, con un sutil borde oscuro interior y un borde cian que aparece al enfocarse para indicar el modo de edición.

## Qué hace cada control

| Control                           | Valor predeterminado | Rango válido                             |
|-----------------------------------|----------------------|------------------------------------------|
| Curva de respuesta del sidechain  | —                    | —                                        |
| Barra de Gain-reduction           | —                    | 0 a 24 dB GR                             |
| Freq                              | 6000 Hz              | 1000 a 12000 Hz                          |
| Q                                 | 2.00                 | 0.5 a 5.0                                |
| Thresh                            | −30.0 dB             | −60.0 a 0.0 dB                           |
| Amount                            | −6.0 dB              | −24.0 a 0.0 dB                           |
| Attack (solo en channel strip)    | 1.0 ms               | 0.1 a 30.0 ms                            |
| Release (solo en channel strip)   | 100 ms               | 10.0 a 500.0 ms                          |
| Slope                             | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas)  |

## Curva de respuesta del sidechain

El indicador de curva de respuesta del sidechain muestra la respuesta del filtro paso banda con un punto móvil en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas de eje usan `QStaticText` para un renderizado eficiente y muestran frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

El widget de curva ahora usa colores adaptados al tema mediante el contexto de contenedor `applet/deess`. El color de la curva se dibuja en el color de acento de peligro del tema, y el indicador de umbral usa el color de acento tenue del tema.

## Control Slope

Un botón Slope aparece en la parte inferior de la columna izquierda de controles en el Aetherial Audio Channel Strip (paneles TX y RX). Cicla a través de 12 → 24 → 36 → 48 dB/oct (1 a 4 biquads de paso banda en cascada) cada vez que hace clic en él.

- Mayor pendiente = muesca más estrecha alrededor de la frecuencia sibilante = menos daño colateral en frecuencias medias en frases con muchas "eses".
- El botón muestra el valor actual como "N dB/oct" (p. ej., "24 dB/oct").
- El ajuste se guarda por separado para TX y RX como `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

Para ajustar la pendiente:

1. Haga clic en el botón Slope repetidamente para ciclar por los valores disponibles.
2. Observe la curva de respuesta del sidechain actualizarse en tiempo real para ver la muesca estrecharse.
3. Deténgase cuando el de-esser apunte solo a la sibilancia sin afectar la energía del habla cercana.

**Nota:** El applet Aetherial De-Esser acoplado omite los controles Attack, Release y Slope. Estos solo están disponibles en el panel Aetherial Audio Channel Strip.

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Applet Panel acoplado. Se abre desde la cadena TX en el Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Se accede a través del lado RX del Aetherial Audio Channel Strip. Utiliza su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc. El botón Slope en el panel RX usa `ClientDeEssRxSlopeStages`.

## Atenuación por bypass

Cuando la etapa DESS se desvía (bypass) mediante un solo clic en el widget CHAIN, todo el applet se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación usado en la curva EQ y proporciona una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para re-habilitar la etapa y restaurar la opacidad completa.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra de Gain-reduction señala este nivel, lo que facilita su uso como referencia durante el ajuste.
- Apunte a que la barra de Gain-reduction se mueva notablemente en los sonidos "S" y "T", pero que nunca llegue al extremo de 24 dB. Una reducción de ganancia fuerte en ese extremo se percibe como un ceceo o una pérdida de señal.
- Reducir la banda del sidechain con Q antes de finalizar Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Estrechar o ensanchar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero: representan reducción, no realce.
- Utilice la edición de valor en línea para una entrada numérica precisa en lugar de un ajuste fino girando el control.
- Ajuste Slope para apretar la muesca del sidechain — esto preserva el habla en frecuencias medias mientras corta agresivamente las sibilancias.

## Solución de problemas

- **El audio suena hueco o como un ceceo en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra de Gain-reduction nunca se mueve** — El de-esser no se está activando. Verifique que Thresh esté por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de Gain-reduction se queda fija constantemente en 24 dB** — Thresh está demasiado bajo, lo que hace que el de-esser se active en todo el habla, no solo en la sibilancia. Suba Thresh primero, luego reevalúe Amount.
- **El applet se ve descolorido o atenuado** — La etapa DESS está en bypass. Haga clic en la etapa en el widget CHAIN una vez para re-habilitarla.
- **El editor en línea no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del control. Los valores fuera de rango se limitan automáticamente. Si el valor se revierte, verifique si hay espacios adicionales o caracteres que no se hayan eliminado.
- **El habla en frecuencias medias suena apagada o atenuada** — La pendiente Slope puede ser demasiado baja. Aumente Slope a 36 o 48 dB/oct para estrechar la muesca del sidechain y preservar la energía en frecuencias medias.

## Adaptación al tema

En la v26.6.1, todo el applet Aetherial De-Esser y sus sub-widgets se adaptan al tema:

- El contenedor del applet se registra como `applet/deess` para anulaciones de tema por contenedor.
- Los componentes del control (anillo de fondo, arco, manija, texto de etiqueta y valor) leen de los espacios de nombres del tema `color.knob.*` y `color.text.*`.
- La curva de respuesta del sidechain lee de `color.background.*`, `color.text.label`, `color.accent.danger` y `color.accent.dim`.

Esto significa que si está utilizando un tema personalizado, los colores del de-esser pueden diferir de las capturas de pantalla de este manual. Consulte la documentación de su tema para personalizaciones de color específicas.

## Relacionados

- [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ensanchar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la GR en vivo mientras lee una frase con muchas "eses"](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Desviar el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Visión general del Aetherial De-Esser](overview.md)
