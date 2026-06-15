# Cantidad de atenuación para un de-essing más transparente

El control Cantidad (Amount) establece la máxima atenuación que aplica el de-esser cuando los picos de sibilancias superan el umbral. Ajustar el valor correcto permite domar la aspereza sin que el audio suene procesado o bombeado.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet está oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser desde el Aetherial Audio Channel Strip. El editor flotante (antes accesible haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en el applet.
- Ajuste primero Freq y Thresh para que el de-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq para localizar el pico de sibilancias](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Pida a alguien que transmita por el micrófono, o lea en voz alta una frase con muchas sibilancias, para que el de-esser esté disparando activamente.
2. Observe la barra de Reducción de Ganancia (Gain-reduction). Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca indica el punto de −6 dB.
3. Gire el control Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra de Reducción de Ganancia solo alcance la marca de −6 dB en los picos más fuertes de "S". Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de Reducción de Ganancia llega al tope cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pasos pequeños hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Edición inline de valores

Cada control del applet Aetherial De-Esser admite entrada numérica directa. Haga clic en la etiqueta de valor del control para abrir una pequeña superposición de editor de texto. Escriba un valor y presione Enter o haga clic fuera para confirmar. El valor se ajusta automáticamente al rango válido del control.

- El editor acepta formatos numéricos según la configuración regional (ej. "12,5" en configuraciones que usan coma decimal).
- Si escribe texto adicional (ej. "12.5 ms" o "−6 dB"), el editor elimina los caracteres no numéricos y analiza el número.
- Presione Escape para cancelar la edición y volver al valor anterior.
- La rueda del ratón sigue funcionando mientras el editor está enfocado, enviándose al control para ajuste.
- Cuando no está enfocado, el editor se ve idéntico a una etiqueta de valor pintada — un sutil borde oscuro interior y un borde cian aparecen al enfocarse para indicar el modo de edición.

## Qué hace cada control

| Control                      | Valor predeterminado | Rango válido                             |
|------------------------------|----------------------|------------------------------------------|
| Curva de respuesta sidechain | —                    | —                                        |
| Barra de reducción de ganancia | —                  | 0 a 24 dB GR                             |
| Freq                         | 6000 Hz              | 1000 a 12000 Hz                          |
| Q                            | 2.00                 | 0.5 a 5.0                                |
| Thresh                       | −30.0 dB             | −60.0 a 0.0 dB                           |
| Amount                       | −6.0 dB              | −24.0 a 0.0 dB                           |
| Ataque (solo en channel strip) | 1.0 ms             | 0.1 a 30.0 ms                            |
| Liberación (solo en channel strip) | 100 ms          | 10.0 a 500.0 ms                          |
| Slope                        | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas)  |

## Curva de respuesta sidechain

El indicador de curva de respuesta sidechain muestra la respuesta del filtro paso banda con un punto móvil en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas del eje usan `QStaticText` para renderizado eficiente y muestran frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

El widget de curva ahora usa colores conscientes del tema mediante el contexto de contenedor `applet/deess`. El color de la curva se dibuja en el color de acento de peligro del tema, y el indicador de umbral usa el color de acento atenuado del tema.

## Control de pendiente (Slope)

Un botón Slope aparece en la parte inferior de la columna izquierda de perillas en el Aetherial Audio Channel Strip (paneles TX y RX). Cada clic alterna entre 12 → 24 → 36 → 48 dB/oct (1 a 4 bicuadros paso banda en cascada).

- Pendiente más alta = muesca más estrecha alrededor de la frecuencia sibilante = menos daño colateral en frecuencias medias en frases con muchas "S".
- El botón muestra el valor actual como "N dB/oct" (ej. "24 dB/oct").
- El ajuste se guarda por separado para TX y RX como `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

Para ajustar la pendiente:

1. Haga clic repetidamente en el botón Slope para recorrer los valores disponibles.
2. Observe la curva de respuesta sidechain actualizarse en tiempo real para ver la muesca estrechada.
3. Deténgase cuando el de-esser se dirija solo a las sibilancias sin afectar la energía del habla cercana.

**Nota:** El applet Aetherial De-Esser acoplado omite los controles Attack, Release y Slope. Estos solo están disponibles en el panel Aetherial Audio Channel Strip.

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Panel de Applets acoplado. Se abre desde la cadena TX en el Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Se accede a través del lado RX del Aetherial Audio Channel Strip. Usa su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc. El botón Slope en el panel RX usa `ClientDeEssRxSlopeStages`.

## Atenuación por bypass

Cuando la etapa DESS está en bypass mediante un solo clic en el widget CHAIN, todo el applet se renderiza con opacidad reducida (55%). Esto coincide con el efecto de atenuación usado en la curva del ecualizador y da una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para reactivar la etapa y restaurar la opacidad total.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra de Reducción de Ganancia indica este nivel, facilitando su uso como referencia durante el ajuste.
- Apunte a que la barra de Reducción de Ganancia se mueva notablemente en los sonidos "S" y "T", pero nunca llegue al tope del extremo de 24 dB. Una reducción de ganancia pesada en ese extremo se percibe como un ceceo o una caída de audio.
- Estrechar la banda sidechain con Q antes de finalizar el Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Estreche o ensanche la banda sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero — representan reducción, no aumento.
- Use la edición inline de valores para entrada numérica precisa en lugar de ajustar con la perilla.
- Ajuste Slope para ajustar la muesca sidechain — esto preserva el habla en frecuencias medias mientras corta agresivamente las sibilancias.

## Solución de problemas

- **El audio suena hueco o ceceante en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra de Reducción de Ganancia nunca se mueve** — El de-esser no está disparando. Verifique que Thresh esté por debajo de su nivel real de sibilancias y que la etapa DESS esté habilitada. Consulte [Ajuste el umbral justo debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de Reducción de Ganancia llega constantemente al tope de 24 dB** — Thresh está demasiado bajo, haciendo que el de-esser se dispare con todo el habla, no solo con las sibilancias. Suba Thresh primero, luego revalúe Amount.
- **El applet se ve descolorido o atenuado** — La etapa DESS está en bypass. Haga clic en la etapa en el widget CHAIN una vez para reactivarla.
- **El editor inline no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del control. Los valores fuera de rango se ajustan automáticamente. Si el valor se revierte, verifique que no haya espacios o caracteres adicionales que no se hayan eliminado.
- **El habla en frecuencias medias suena opaca o atenuada** — Slope puede estar demasiado bajo. Aumente Slope a 36 o 48 dB/oct para estrechar la muesca sidechain y preservar la energía en frecuencias medias.

## Conciencia del tema

En v26.6.1, todo el applet Aetherial De-Esser y sus sub-widgets se volvieron conscientes del tema:

- El contenedor del applet se registra como `applet/deess` para anulaciones de tema por contenedor.
- Los componentes de perilla (anillo de fondo, arco, manija, texto de etiqueta y valor) leen de los espacios de nombre del tema `color.knob.*` y `color.text.*`.
- La curva de respuesta sidechain lee de `color.background.*`, `color.text.label`, `color.accent.danger`, y `color.accent.dim`.

Esto significa que si está usando un tema personalizado, los colores del de-esser pueden diferir de las capturas de pantalla en este manual. Consulte la documentación de su tema para personalización específica de colores.

## Relacionados

- [Sweep Freq para localizar el pico de sibilancias](sweep-freq-to-locate-peak-sibilance.md)
- [Estreche o ensanche la banda sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la GR en vivo mientras lee una frase con sibilancias](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Ponga en bypass el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Descripción general del Aetherial De-Esser](overview.md)
