# Ajuste de la cantidad para un de-essing más transparente

El mando Amount define la atenuación máxima que aplica el de-esser cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto permite domar la aspereza sin que el audio suene procesado o bombeado.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser desde el Aetherial Audio Channel Strip. El editor flotante (anteriormente accesible haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en el applet.
- Ajuste primero Freq y Thresh para que el de-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Haga que alguien transmita por el micrófono — o lea una frase sibilante en voz alta — para que el de-esser esté disparando activamente.
2. Observe la barra de reducción de ganancia. Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca indica el punto de −6 dB.
3. Gire el mando Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra de reducción de ganancia solo alcance la marca de −6 dB en los picos más fuertes de "S". Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de reducción de ganancia está fija cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pequeños pasos hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Edición inline de valores

Cada mando en el applet Aetherial De-Esser admite entrada numérica directa. Haga clic en la etiqueta del valor del mando para abrir una pequeña superposición de editor de texto. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido del mando.

- El editor acepta formatos numéricos según la configuración regional (p. ej., "12,5" en configuraciones con coma decimal).
- Si escribe texto adicional (p. ej., "12.5 ms" o "−6 dB"), el editor elimina los caracteres no numéricos y analiza el número.
- Presione Escape para cancelar la edición y revertir al valor anterior.
- El desplazamiento con la rueda del ratón sigue funcionando mientras el editor está enfocado, reenviándose al mando para su ajuste.
- Cuando no está enfocado, el editor aparece idéntico a una etiqueta de valor pintada: un sutil borde oscuro interno y un borde cian aparecen al enfocarse para indicar el modo de edición.

## Qué hace cada control

| Control                          | Valor predeterminado | Rango válido                            |
|----------------------------------|----------------------|-----------------------------------------|
| Curva de respuesta de sidechain  | —                    | —                                       |
| Barra de reducción de ganancia   | —                    | 0 a 24 dB GR                            |
| Freq                             | 6000 Hz              | 1000 a 12000 Hz                         |
| Q                                | 2.00                 | 0.5 a 5.0                               |
| Thresh                           | −30.0 dB             | −60.0 a 0.0 dB                          |
| Amount                           | −6.0 dB              | −24.0 a 0.0 dB                          |
| Ataque (solo en channel strip)   | 1.0 ms               | 0.1 a 30.0 ms                           |
| Liberación (solo en channel strip)| 100 ms              | 10.0 a 500.0 ms                         |
| Slope                            | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) |

## Curva de respuesta de sidechain

El indicador de curva de respuesta de sidechain muestra la respuesta del filtro paso banda con un punto vivo en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas de los ejes usan `QStaticText` para un renderizado eficiente y muestran frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

El widget de curva ahora usa colores conscientes del tema a través del contexto de contenedor `applet/deess`. El color de la curva se dibuja en el color de acento de peligro del tema, y el indicador de umbral usa el color de acento tenue del tema.

## Control de Slope

Un botón Slope aparece en la parte inferior de la columna izquierda de mandos en el Aetherial Audio Channel Strip (paneles TX y RX). Cada clic cicla a través de 12 → 24 → 36 → 48 dB/oct (1 a 4 biquads paso banda en cascada).

- Mayor pendiente = muesca más estrecha alrededor de la frecuencia sibilante = menos daño colateral en la banda media en frases con muchas "S".
- El botón muestra el valor actual como "N dB/oct" (p. ej., "24 dB/oct").
- El ajuste se guarda por separado para TX y RX como `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

Para ajustar la pendiente:

1. Haga clic repetidamente en el botón Slope para recorrer los valores disponibles.
2. Observe la actualización en tiempo real de la curva de respuesta de sidechain para ver la muesca estrechada.
3. Deténgase cuando el de-esser apunte solo a la sibilancia sin afectar la energía del habla cercana.

**Nota:** El applet Aetherial De-Esser acoplado omite los controles de Ataque, Liberación y Slope. Estos solo están disponibles en el panel Aetherial Audio Channel Strip.

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Panel de Applets acoplado. Se abre desde la cadena TX en el Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Accesible a través del lado RX del Aetherial Audio Channel Strip. Usa su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes de RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc. El botón Slope en el panel RX usa `ClientDeEssRxSlopeStages`.

## Atenuación al bypass

Cuando la etapa DESS está en bypass mediante un solo clic en el widget CHAIN, todo el applet se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación usado en la curva de EQ y proporciona una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para reactivar la etapa y restaurar la opacidad completa.

## Mejoras de rendimiento

En v26.7.4, el widget de curva de respuesta de sidechain se repinta en cada tick de animación, independientemente de si la animación se ha estabilizado o si se solicitó explícitamente un repintado. Esto garantiza actualizaciones visuales suaves durante la medición de reducción de ganancia y los ajustes de frecuencia.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra de reducción de ganancia señala este nivel, lo que facilita su uso como referencia durante el ajuste.
- Apunte a que la barra de reducción de ganancia se mueva notablemente en los sonidos "S" y "T", pero que nunca llegue al extremo de 24 dB. La reducción de ganancia intensa en ese extremo es audible como un ceceo o pérdida de señal.
- Estrechar la banda de sidechain con Q antes de finalizar Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Estreche o ensanche la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero — representan reducción, no aumento.
- Use la edición inline de valores para entrada numérica precisa en lugar de ajustar fino girando el mando.
- Ajuste Slope para estrechar la muesca de sidechain — esto preserva el habla de banda media mientras corta agresivamente las sibilantes.

## Solución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra de reducción de ganancia nunca se mueve** — El de-esser no está disparando. Verifique que Thresh esté ajustado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Ajuste el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de reducción de ganancia está fija en 24 dB constantemente** — Thresh está demasiado bajo, lo que hace que el de-esser dispare en todo el habla, no solo en la sibilancia. Suba Thresh primero, luego reevalúe Amount.
- **El applet aparece atenuado u oscurecido** — La etapa DESS está en bypass. Haga clic una vez en la etapa en el widget CHAIN para reactivarla.
- **El editor inline no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del mando. Los valores fuera de rango se ajustan automáticamente. Si el valor se revierte, verifique si hay espacios extra o caracteres que no se hayan eliminado.
- **El habla de banda media suena apagada o atenuada** — Es posible que Slope esté demasiado bajo. Aumente Slope a 36 o 48 dB/oct para estrechar la muesca de sidechain y preservar la energía de banda media.

## Conciencia del tema

En v26.6.1, todo el applet Aetherial De-Esser y sus sub-widgets se volvieron conscientes del tema:

- El contenedor del applet se registra como `applet/deess` para anulaciones de tema por contenedor.
- Los componentes del mando (anillo de fondo, arco, asa, etiqueta y texto del valor) leen de los espacios de nombres del tema `color.knob.*` y `color.text.*`.
- La curva de respuesta de sidechain lee de `color.background.*`, `color.text.label`, `color.accent.danger` y `color.accent.dim`.

Esto significa que si está usando un tema personalizado, los colores del de-esser pueden diferir de las capturas de pantalla de este manual. Consulte la documentación de su tema para personalizaciones de color específicas.

## Relacionados

- [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estreche o ensanche la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass del de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Visión general del Aetherial De-Esser](overview.md)
