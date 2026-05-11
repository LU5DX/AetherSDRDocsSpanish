# Ajuste de la cantidad para un de-essing más transparente

El mando Amount establece la atenuación máxima que aplica el de-esser cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto le permite domar la aspereza sin que el audio suene procesado o bombeado.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. La aplicación secundaria (applet) permanece oculta hasta que la etapa esté activa.
- Abra la aplicación secundaria Aetherial De-Esser a través de la Aetherial Audio Channel Strip. El editor flotante (anteriormente accesible haciendo doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en la aplicación secundaria.
- Configure primero Freq y Thresh para que el de-esser ya esté disparando en la banda correcta. Consulte [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Haga que alguien transmita hacia el micrófono — o lea una frase sibilante en voz alta — para que el de-esser se active.
2. Observe la barra de reducción de ganancia (Gain-reduction). Se llena de derecha a izquierda en rojo suave para indicar cuánta atenuación se está aplicando. Una marca señala el punto de −6 dB.
3. Gire el mando Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que la aspereza desaparezca.
4. Retroceda en sentido horario hasta que la barra de reducción de ganancia solo alcance la marca de −6 dB en los picos de "S" más fuertes. Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de reducción de ganancia llega al tope cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pequeños pasos hasta que la naturalidad regrese.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Qué hace cada control

| Control            | Valor predeterminado | Rango válido     | Comportamiento                                                                                             |
|--------------------|----------------------|------------------|------------------------------------------------------------------------------------------------------------|
| Amount             | −6.0 dB              | −24.0 a 0.0 dB   | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción. |
| Barra de reducción de ganancia | —        | 0 a 24 dB GR     | Franja roja suave horizontal, relleno desde la derecha. La escala máxima es 24 dB; una marca indica el valor típico de −6 dB. Se actualiza a ~30 Hz. |
| Attack             | 1.0 ms               | 0.1 a 30.0 ms    | Mapeo exponencial (0.1 × 300^n). Define la rapidez con la que responde el de-esser una vez que la sibilancia supera el umbral. Presente en el StripDeEssPanel de la Channel Strip (RX y TX). La aplicación secundaria acoplada ClientDeEssApplet omite este mando. |
| Release            | 100 ms               | 10.0 a 500.0 ms  | Mapeo exponencial (10 × 50^n). Define la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en el StripDeEssPanel de la Channel Strip (RX y TX). La aplicación secundaria acoplada ClientDeEssApplet omite este mando. |

## Curva de respuesta de la cadena lateral

El indicador de curva de respuesta de la cadena lateral muestra la respuesta del filtro pasabanda con un punto móvil en la frecuencia central actual. En modo compacto, el widget de curva muestra la respuesta sin etiquetas de eje de frecuencia. Las etiquetas del eje utilizan `QStaticText` para un renderizado eficiente y muestran las frecuencias como "100", "500", "1k", "2k", "3k", "4k", "5k", "6k", "8k", "10k", "12k" cuando no está en modo compacto.

## Instancias de RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el panel de aplicaciones secundarias acoplado (docked Applet Panel). Se abre desde la cadena TX en la Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Se accede a través del lado RX de la Aetherial Audio Channel Strip. Utiliza su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, que se guardan por separado. Los ajustes de RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc.

## Atenuación por bypass

Cuando la etapa DESS está bypass mediante un solo clic en el widget CHAIN, toda la aplicación secundaria se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para reactivar la etapa y restaurar la opacidad completa.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra de reducción de ganancia indica este nivel, lo que facilita su uso como referencia durante el ajuste.
- Apunte a que la barra de reducción de ganancia se mueva notablemente en los sonidos "S" y "T", pero que nunca llegue al tope de 24 dB. Una reducción de ganancia intensa en ese extremo es audible como un ceceo o una caída del audio.
- Reducir la banda de la cadena lateral con Q antes de finalizar Amount reduce la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Reduzca o amplíe la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount son siempre negativos o cero — representan reducción, no aumento.

## Solución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está ajustado demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que la naturalidad regrese.
- **La barra de reducción de ganancia nunca se mueve** — El de-esser no se está disparando. Verifique que Thresh esté ajustado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de reducción de ganancia llega constantemente al tope de 24 dB** — Thresh está ajustado demasiado bajo, lo que hace que el de-esser se dispare con todo el habla, no solo con la sibilancia. Suba Thresh primero, luego reevalúe Amount.
- **La aplicación secundaria aparece atenuada u opaca** — La etapa DESS está bypass. Haga clic una vez en la etapa en el widget CHAIN para reactivarla.

## Relacionados

- [Sweep Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Reduzca o amplíe la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass del de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Visión general del Aetherial De-Esser](overview.md)
