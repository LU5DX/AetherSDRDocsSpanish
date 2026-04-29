# Ajuste de Amount para una des-esibilización lo más transparente posible

El control Amount establece la atenuación máxima que aplica el des-esibilizador cuando la sibilancia supera el umbral. Ajustar el valor correcto permite dominar la aspereza sin que el audio suene procesado o con efectos de bombeo.

## Antes de comenzar

- El módulo Aetherial De-Esser (DESS) debe estar habilitado en el widget CHAIN. El applet permanece oculto hasta que el módulo esté activo.
- Abra el applet Aetherial De-Esser o el editor flotante. Para abrir el editor, haga doble clic en el módulo DESS dentro del widget CHAIN (titulado "Aetherial De-Esser — TX").
- Configure primero Freq y Thresh para que el des-esibilizador ya esté actuando sobre la banda correcta. Consulte [Barra Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md) y [Ajuste el umbral justo por debajo de los picos más altos de "S"](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Haga que alguien hable ante el micrófono — o lea en voz alta una frase con sibilantes — de modo que el des-esibilizador esté actuando activamente.
2. Observe la barra de reducción de ganancia (Gain-reduction bar). Se rellena de derecha a izquierda en rojo suave para indicar cuánta atenuación se está aplicando. Una marca señala el punto de −6 dB.
3. Gire el control Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra de reducción de ganancia solo alcance la marca de −6 dB en los picos más altos de "S". Detenerse aquí mantiene el procesado transparente.
5. Si la barra de reducción de ganancia se clava cerca de 24 dB o el audio suena hueco, aumente Amount hacia 0 dB en pasos pequeños hasta que el sonido natural regrese.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada a la banda de sibilancia cuando la señal supera el umbral. Más negativo = mayor reducción. 0 dB desactiva la atenuación por completo. |
| Gain-reduction bar | — | 0 a 24 dB GR | — | Franja horizontal en rojo suave que muestra la reducción de ganancia actual en tiempo real. La escala llega hasta 24 dB; una marca señala −6 dB. Se actualiza aproximadamente 30 veces por segundo. |

## Consejos

- −6 dB (el valor predeterminado) es un buen punto de partida para la mayoría de las voces. La marca en la barra de reducción de ganancia indica este nivel, lo que facilita usarlo como referencia durante el ajuste.
- Procure que la barra de reducción de ganancia se mueva de forma visible con los sonidos "S" y "T", pero que nunca llegue al extremo de 24 dB. Una reducción de ganancia muy elevada en ese extremo se percibe como un ceceo o un corte de audio.
- Estrechar la banda del sidechain con Q antes de fijar definitivamente Amount reduce la atenuación colateral en la energía de voz adyacente, lo que mejora la transparencia. Consulte [Estreche o amplíe la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount siempre son negativos o cero — representan reducción, no realce.

## Resolución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está demasiado bajo (demasiada atenuación). Auméntelo hacia 0 dB en pasos de 2 dB mientras habla hasta que el sonido natural regrese.
- **La barra de reducción de ganancia nunca se mueve** — El des-esibilizador no está actuando. Compruebe que Thresh esté configurado por debajo de su nivel real de sibilancia y que el módulo DESS esté habilitado. Consulte [Ajuste el umbral justo por debajo de los picos más altos de "S"](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de reducción de ganancia se clava en 24 dB constantemente** — Thresh está demasiado bajo, lo que hace que el des-esibilizador actúe sobre toda la voz y no solo sobre las sibilantes. Aumente Thresh primero y luego reevalúe Amount.

## Relacionados

- [Barra Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Estreche o amplíe la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos más altos de "S"](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observe la reducción de ganancia en vivo mientras lee una frase con sibilantes](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Desactive el des-esibilizador desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Descripción general de Aetherial De-Esser](overview.md)
