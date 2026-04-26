# Ajuste de Amount para la desibilación más transparente

El control Amount establece la atenuación máxima que aplica el desibilador cuando la sibilancia supera el umbral. Ajustar el valor correcto permite suavizar la aspereza sin que el audio suene procesado o con efecto de bombeo.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada en el widget CHAIN. El applet permanece oculto hasta que la etapa esté activa.
- Abra el applet Aetherial De-Esser o el editor flotante. Para abrir el editor, haga doble clic en la etapa DESS dentro del widget CHAIN (titulada "Aetherial De-Esser — TX").
- Configure primero Freq y Thresh para que el desibilador ya esté actuando sobre la banda correcta. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md) y [Establecer el umbral justo por debajo de los picos más fuertes de "S"](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Haga que alguien transmita hacia el micrófono —o lea en voz alta una frase con sibilantes— para que el desibilador esté disparándose activamente.
2. Observe la barra de reducción de ganancia (Gain-reduction). Se llena de derecha a izquierda en rojo suave para indicar cuánta atenuación se está aplicando. Una marca señala el punto −6 dB.
3. Gire el control Amount en sentido antihorario para aumentar la atenuación (valores más negativos) hasta que desaparezca la aspereza.
4. Retroceda en sentido horario hasta que la barra de reducción de ganancia solo alcance la marca de −6 dB en los picos más fuertes de "S". Detenerse aquí mantiene el procesamiento transparente.
5. Si la barra de reducción de ganancia se fija cerca de 24 dB o el audio suena hueco, aumente Amount hacia 0 dB en pasos pequeños hasta que el sonido natural regrese.
6. Los cambios se guardan automáticamente. El ajuste persiste como `ClientDeEssTxAmountDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada a la banda de sibilancia cuando la señal supera el umbral. Más negativo = mayor reducción. 0 dB desactiva la atenuación por completo. |
| Barra de reducción de ganancia (Gain-reduction) | — | 0 a 24 dB GR | — | Franja horizontal en rojo suave que muestra la reducción de ganancia actual en tiempo real. La escala llega hasta 24 dB; una marca señala −6 dB. Se actualiza aproximadamente 30 veces por segundo. |

## Consejos

- −6 dB (el valor predeterminado) es un buen punto de partida para la mayoría de las voces. La marca en la barra de reducción de ganancia señala este nivel, lo que facilita su uso como referencia durante el ajuste.
- Busque que la barra de reducción de ganancia se mueva de forma notable en los sonidos "S" y "T", pero que nunca llegue al extremo de 24 dB. Una reducción de ganancia excesiva en ese extremo se escucha como ceceo o corte de audio.
- Estrechar la banda del sidechain con Q antes de finalizar Amount reduce la atenuación colateral sobre la energía vocal adyacente, lo que mejora la transparencia. Consulte [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Los valores de Amount son siempre negativos o cero; representan reducción, no realce.

## Solución de problemas

- **El audio suena hueco o con ceceo en cada "S"** — Amount está configurado demasiado bajo (demasiada atenuación). Auméntelo hacia 0 dB en pasos de 2 dB mientras habla, hasta que el sonido natural regrese.
- **La barra de reducción de ganancia nunca se mueve** — El desibilador no se está disparando. Verifique que Thresh esté configurado por debajo de su nivel real de sibilancia y que la etapa DESS esté habilitada. Consulte [Establecer el umbral justo por debajo de los picos más fuertes de "S"](set-threshold-just-below-the-loudest-s-peaks.md).
- **La barra de reducción de ganancia se fija constantemente en 24 dB** — Thresh está configurado demasiado bajo, lo que hace que el desibilador se dispare con todo el habla y no solo con la sibilancia. Aumente primero Thresh y luego reevalúe Amount.

## Relacionados

- [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Establecer el umbral justo por debajo de los picos más fuertes de "S"](set-threshold-just-below-the-loudest-s-peaks.md)
- [Observar la reducción de ganancia en vivo mientras se lee una frase con sibilantes](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el desibilador desde la cadena](bypass-the-de-esser-from-the-chain.md)
- [Descripción general del Aetherial De-Esser](overview.md)
