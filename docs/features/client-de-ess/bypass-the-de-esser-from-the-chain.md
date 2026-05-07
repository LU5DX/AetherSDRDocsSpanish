# Omitir el de-esser de la cadena

Elimine el Aetherial De-Esser de su ruta de audio de TX o RX sin cambiar ninguno de sus ajustes. Omitir el de-esser es útil cuando desea comparar el audio tratado y el no tratado, o deshabilitar temporalmente la reducción de sibilancias para una sesión en particular.

## Antes de comenzar

- AetherSDR debe estar abierto y la cadena de procesamiento de Aetherial Audio (TXDSP o RXDSP) debe estar visible.
- La etapa DESS ya debe existir en el widget CHAIN. Si el de-esser nunca se ha habilitado, es posible que la etapa DESS no esté presente; consulte [Descripción general de Aetherial De-Esser](overview.md).
- El de-esser está disponible tanto en la ruta de audio de TX como en la de RX. Cada ruta tiene su propia instancia independiente del Aetherial De-Esser.

## Pasos para omitir el de-esser de TX

1. Localice el widget CHAIN en el contenedor de Aetherial Audio (TXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para activar o desactivar la omisión.

## Pasos para omitir el de-esser de RX

1. Localice el widget CHAIN en el contenedor de Aetherial Audio (RXDSP).
2. Encuentre la etapa **DESS** en la cadena.
3. Haga clic una vez en la etapa **DESS** para activar o desactivar la omisión.

Cuando se omite, todo el bloque del de-esser se muestra con opacidad reducida (55 % de lo normal). Al hacer clic una vez más, se vuelve a habilitar y se restaura la opacidad completa del bloque. Los ajustes `ClientDeEssTxEnabled` y `ClientDeEssRxEnabled` se actualizan inmediatamente.

## Abrir el panel de ajustes del de-esser

El panel de ajustes del de-esser tiene dos instancias:
- **Instancia de TX**: "Aetherial De-Esser — TX" (accesible desde la ruta de TX de la tira de canal de Aetherial Audio)
- **Instancia de RX**: "Aetherial De-Esser — RX" (accesible desde la ruta de RX de la tira de canal de Aetherial Audio)

Para abrir la instancia adecuada:
1. Abra la tira de canal de Aetherial Audio.
2. Haga clic en la etapa **DESS** para abrir el panel de ajustes del de-esser para esa ruta (TX o RX).
3. La barra de título del panel muestra "Aetherial De-Esser — TX" o "Aetherial De-Esser — RX" según la ruta a la que accedió.

## Controles del de-esser

El panel de Aetherial De-Esser contiene los siguientes controles:

| Etiqueta | Tipo | Valor predeterminado | Rango válido | Clave de ajuste | Notas |
|---|---|---|---|---|---|
| Curva de respuesta de la cadena lateral | indicador | — | — | — | Dibuja la respuesta del filtro paso banda con un punto móvil en la frecuencia central actual. |
| Barra de reducción de ganancia | medidor | — | 0 a 24 dB de GR | — | Franja horizontal de color rojo suave, llenada por la derecha. La escala máxima es 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a ~30 Hz. |
| Freq | perilla | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` o `ClientDeEssRxFrequencyHz` | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancias. |
| Q | perilla | 2,00 | 0,5 a 5,0 | `ClientDeEssTxQ` o `ClientDeEssRxQ` | Mapeo lineal. Establece el ancho de banda de la banda de sibilancias: Q más alto = más estrecho. |
| Thresh | perilla | -30,0 dB | -60,0 a 0,0 dB | `ClientDeEssTxThresholdDb` o `ClientDeEssRxThresholdDb` | Nivel por encima del cual el de-esser comienza a atenuar la banda. |
| Amount | perilla | -6,0 dB | -24,0 a 0,0 dB | `ClientDeEssTxAmountDb` o `ClientDeEssRxAmountDb` | Atenuación máxima aplicada en el pico de sibilancias. Los valores son negativos (o cero) porque representan reducción. |
| Attack | perilla | 1,0 ms | 0,1 a 30,0 ms | `ClientDeEssTxAttackMs` o `ClientDeEssRxAttackMs` | Establece la rapidez con la que responde el de-esser una vez que las sibilancias superan el umbral. Presente en el panel StripDeEssPanel de la tira de canal (RX y TX). |
| Release | perilla | 100 ms | 10,0 a 500,0 ms | `ClientDeEssTxReleaseMs` o `ClientDeEssRxReleaseMs` | Establece la rapidez con la que la ganancia regresa después de que las sibilancias caen por debajo del umbral. Presente en el panel StripDeEssPanel de la tira de canal (RX y TX). |

## Consejos

- Omitir no restablece ningún valor de las perillas. Freq, Q, Thresh y Amount conservan sus ajustes actuales cuando vuelve a habilitar la etapa.
- Las instancias del de-esser de TX y RX son independientes. Cambiar los ajustes en una no afecta a la otra.
- La curva de respuesta de la cadena lateral y el medidor de reducción de ganancia reflejan la instancia actualmente activa (TX o RX) en la barra de título del panel.

## Relacionados

- [Descripción general de Aetherial De-Esser](overview.md)
- [Barrer Freq para localizar el pico de sibilancias](sweep-freq-to-locate-peak-sibilance.md)
- [Establecer el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para la reducción de sibilancias más transparente](dial-amount-for-the-most-transparent-de-essing.md)
