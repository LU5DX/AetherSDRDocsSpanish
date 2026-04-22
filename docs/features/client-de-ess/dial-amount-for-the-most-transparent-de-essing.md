# Ajuste de Amount para el de-essing más transparente

El control Amount establece la atenuación máxima que aplica el de-esser cuando los picos de sibilancia son más intensos. Ajustarlo al valor mínimo que suavice la aspereza mantiene el tratamiento imperceptible en el habla normal.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada. Consulte [Descripción general del De-Esser](overview.md) para saber cómo habilitarla desde el widget CHAIN.
- El applet DESS debe estar visible dentro del contenedor PooDoo Audio (TXDSP). Si está oculto, haga doble clic en la etapa DeEss del widget CHAIN para abrir el editor flotante, o haga clic derecho en la barra de título del subcontenedor DESS y muéstrelo.
- Configure Freq y Thresh antes de ajustar Amount, de modo que el de-esser ya esté activándose con su sibilancia. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md) y [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Abra el applet DESS dentro del contenedor PooDoo Audio (TXDSP).
2. Hable continuamente al micrófono, repitiendo palabras sibilantes ("sister", "sixty-six", "success") para mantener el de-esser en funcionamiento.
3. Observe la barra de reducción de ganancia (Gain-reduction). El relleno rojo suave muestra la atenuación que se está aplicando en ese momento; la marca indica el punto de −6 dB.
4. Gire el control Amount completamente hacia la izquierda hasta su mínimo (−24.0 dB) para escuchar el efecto con claridad.
5. Gire Amount lentamente hacia la derecha (hacia 0.0 dB) hasta que la aspereza regrese, luego retroceda ligeramente: este es el ajuste más transparente.
6. Confirme que la barra de reducción de ganancia alcanza su pico brevemente en los sonidos 'S' fuertes, pero permanece cerca de cero en las vocales normales. Si está al máximo durante el habla ordinaria, el umbral está demasiado bajo; consulte [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).
7. Suelte el control. El valor se guarda automáticamente en `ClientDeEssTxAmountDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada a la banda de sibilancia cuando la señal del sidechain está en su pico. Los valores son negativos porque representan reducción. 0.0 dB significa sin atenuación. |
| Barra de reducción de ganancia | — | 0 a 24 dB mostrados | — | Franja horizontal rojo suave, rellena desde la derecha. Muestra la atenuación actual en tiempo real. Una marca indica el punto de −6 dB. Se actualiza aproximadamente 30 veces por segundo. |

## Consejos

- El valor predeterminado de −6.0 dB es un punto de partida seguro. La mayoría de las voces necesitan entre −3.0 dB y −9.0 dB para un tratamiento transparente.
- Los valores negativos más altos (hacia −24.0 dB) producen un ducking más agresivo que es más fácil de percibir como artefacto. Úselos solo para sibilancia severa.
- Si no puede encontrar un ajuste donde las sibilantes se suavicen sin afectar el habla normal, la banda del sidechain puede ser demasiado ancha. Estreche primero con el control Q; consulte [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).
- Use [Ver la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md) para evaluar el ajuste final en condiciones realistas antes de transmitir.

## Solución de problemas

- **La barra de reducción de ganancia siempre está al límite de Amount** — Thresh está demasiado bajo y el de-esser se activa con todo el habla, no solo con las sibilantes. Suba Thresh hasta que la barra solo deflecte en los sonidos fuertes de 'S' y 'T'.
- **No aparece reducción de ganancia incluso con Amount en −24.0 dB** — El de-esser no se está activando. O bien la etapa está en bypass o Thresh está por encima del nivel de su sibilancia. Compruebe que la etapa esté habilitada en el widget CHAIN y luego baje Thresh.
- **El cambio de Amount no tiene efecto tras reconectarse** — Los ajustes se restauran desde `ClientDeEssTxAmountDb` al cargar. Si el control muestra el valor correcto pero el audio no se ve afectado, confirme que la etapa De-Ess esté habilitada y no en bypass; consulte [Poner el de-esser en bypass desde la cadena](bypass-the-de-esser-from-the-chain.md).

## Relacionados

- [Descripción general del De-Esser](overview.md)
- [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ver la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Poner el de-esser en bypass desde la cadena](bypass-the-de-esser-from-the-chain.md)
