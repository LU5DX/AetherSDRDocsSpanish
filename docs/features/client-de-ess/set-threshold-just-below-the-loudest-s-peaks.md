# Ajuste el umbral justo por debajo de los picos de 'S' más fuertes

El mando **Thresh** controla el nivel a partir del cual el des-esibador comienza a atenuar la banda de sibilancia. Ajustarlo justo por debajo de sus picos de 'S' más fuertes garantiza que el des-esibador se active ante sibilancias pronunciadas sin afectar el habla normal.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN y el applet DESS debe ser visible. Consulte [Descripción general del des-esibador](overview.md).
- Identifique primero la frecuencia central de sibilancia. Consulte [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md).

## Pasos

1. Abra el subcontenedor DESS dentro del contenedor padre PooDoo Audio (TXDSP). Si está oculto, haga doble clic en la etapa DeEss del widget CHAIN para abrir el editor flotante De-Ess.
2. Active su audio de transmisión y pronuncie un sonido 'S' sostenido o una frase sibilante.
3. Observe la barra de reducción de ganancia. Si no muestra relleno rojo suave, el umbral está demasiado alto y el des-esibador no se está activando.
4. Gire el mando **Thresh** en sentido antihorario para bajar el umbral hasta que la barra de reducción de ganancia comience a mostrar un pequeño relleno en sus picos de 'S' más fuertes.
5. Continúe pronunciando frases sibilantes. Ajuste **Thresh** hacia arriba de nuevo hasta que la barra de reducción de ganancia apenas se active durante el habla normal, pero se ilumine claramente ante sonidos de 'S' pronunciados.
6. Confirme que el valor mostrado debajo del mando **Thresh** está ajustado justo por debajo del nivel de su sibilancia pico. Un punto de partida típico es aproximadamente `-30.0 dB`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Thresh** | -30.0 dB | -60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel a partir del cual el des-esibador comienza a atenuar la banda de sibilancia. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Franja roja suave horizontal, rellena desde la derecha. Muestra la atenuación aplicada en tiempo real. Una marca señala el punto de -6 dB. Se actualiza aproximadamente a 30 Hz. |

## Consejos

- La barra de reducción de ganancia es su principal herramienta de retroalimentación. Un umbral correctamente ajustado mostrará actividad breve y moderada en los sonidos 'S' y 'T', y permanecerá vacío durante las vocales y las consonantes normales.
- La escala de la barra de reducción de ganancia llega hasta 24 dB. Si la barra está constantemente cerca del límite, **Thresh** está demasiado bajo o **Amount** es demasiado agresivo. Suba **Thresh** primero y luego revise **Amount**.
- Si la barra nunca se ilumina durante sibilancias fuertes, suba **Freq** o amplíe la banda con **Q** antes de concluir que el umbral necesita ajuste. Consulte [Reducir o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md).

## Solución de problemas

- **La barra de reducción de ganancia no muestra actividad a pesar de los sonidos 'S' fuertes** — **Thresh** está ajustado por encima del nivel de sibilancia. Bájelo gradualmente hasta que la barra se active en los picos de 'S'.
- **La barra de reducción de ganancia está activa continuamente durante el habla normal** — **Thresh** está demasiado bajo. Súbalo hasta que la barra permanezca mayormente inactiva y solo se dispare ante picos de sibilancia verdaderos.
- **El des-esibador se activa pero el habla suena sobreprocesada** — El umbral puede ser correcto, pero **Amount** es demasiado elevado. Consulte [Ajustar Amount para un des-esibado más transparente](dial-amount-for-the-most-transparent-de-essing.md).

## Relacionados

- [Descripción general del des-esibador](overview.md)
- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Reducir o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar Amount para un des-esibado más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el des-esibador desde la cadena](bypass-the-de-esser-from-the-chain.md)
