# Ajuste de Cantidad para un des-esseado más transparente

El mando Amount (Cantidad) establece la atenuación máxima que aplica el des-essedor cuando los picos de sibilancia superan el umbral. Ajustar el valor correcto le permite domar la aspereza sin que su audio suene procesado o bombeado.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser a través de Aetherial Audio Channel Strip. El editor flotante (anteriormente accesible al hacer doble clic en la etapa DESS) ya no existe; todos los controles están disponibles directamente en el applet.
- Ajuste primero Freq y Thresh para que el des-essedor ya esté disparando en la banda correcta. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md) y [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Haga que alguien transmita por el micrófono — o lea una frase sibilante en voz alta — para que el des-essedor esté disparando activamente.
2. Observe la barra Gain-reduction (Reducción de ganancia). Se llena de derecha a izquierda en rojo suave para mostrar cuánta atenuación se está aplicando. Una marca indica el punto de −6 dB.
3. Gire el mando Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra Gain-reduction solo alcance la marca de −6 dB en los picos de "S" más fuertes. Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra Gain-reduction está fija cerca de 24 dB o el audio suena hueco, suba Amount hacia 0 dB en pasos pequeños hasta que recupere la naturalidad.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Función de cada control

| Control            | Valor predeterminado                                                                                            | Rango válido                                                                                            |
|--------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Amount             | −6.0 dB                                                                                                         | −24.0 a 0.0 dB                                                                                         |
| Barra Gain-reduction | —                                                                                                               | 0 a 24 dB GR                                                                                           |
| Attack             | Mapeo exponencial (0.1 * 300^n). Define qué tan rápido responde el des-essedor una vez que la sibilancia cruza el umbral. | Presente en el Channel Strip StripDeEssPanel (RX y TX). El applet acoplado ClientDeEssApplet omite este mando. |
| Release            | Mapeo exponencial (10 * 50^n). Define qué tan rápido regresa la ganancia después de que la sibilancia cae por debajo del umbral. | Presente en el Channel Strip StripDeEssPanel (RX y TX). El applet acoplado ClientDeEssApplet omite este mando. |

## Instancias RX y TX

El Aetherial De-Esser tiene instancias separadas para transmisión y recepción:

- **Instancia TX** — Etiquetada como "Aetherial De-Esser" en el Applet Panel acoplado. Se abre desde la cadena TX en Aetherial Audio Channel Strip.
- **Instancia RX** — Etiquetada como "Aetherial De-Esser — RX" en su barra de título. Se accede a través del lado RX de Aetherial Audio Channel Strip. Utiliza su propia ventana dedicada titulada "Aetherial De-Esser — RX".

Cada instancia tiene ajustes independientes, guardados por separado. Los ajustes RX se guardan bajo `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, etc.

## Atenuación por bypass

Cuando la etapa DESS se omite mediante un solo clic en el widget CHAIN, todo el applet se renderiza con opacidad reducida (55 %). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación visual clara de que la etapa está inactiva. Haga clic nuevamente en el widget CHAIN para re-habilitar la etapa y restaurar la opacidad completa.

## Consejos

- −6 dB (el valor predeterminado) es un punto de partida razonable para la mayoría de las voces. La marca en la barra Gain-reduction indica este nivel, lo que facilita su uso como referencia durante el ajuste.
- Apunte a que la barra Gain-reduction se mueva notablemente en los sonidos "S" y "T", pero nunca se fije contra el extremo de 24 dB. Una reducción de ganancia intensa en ese extremo es audible como un ceceo o una caída del volumen.
- Reducir el ancho de la banda del sidechain con Q antes de finalizar Amount disminuye la atenuación colateral en la energía del habla cercana, lo que ayuda a la transparencia. Consulte [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero — representan reducción, no aumento.

## Solución de problemas

- **El audio suena hueco o cecea en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Súbalo hacia 0 dB en pasos de 2 dB mientras habla hasta que recupere la naturalidad.
- **La barra Gain-reduction nunca se mueve** — El des-essedor no está disparando. Verifique que Thresh esté configurado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra Gain-reduction está fija constantemente en 24 dB** — Thresh está demasiado bajo, lo que hace que el des-essedor se dispare en todo el habla, no solo en la sibilancia. Suba Thresh primero, luego re-evalúe Amount.
- **El applet aparece atenuado u oscurecido** — La etapa DESS está en bypass. Haga clic una vez en la etapa en el widget CHAIN para re-habilitarla.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
- [Aetherial De-Esser overview](overview.md)
