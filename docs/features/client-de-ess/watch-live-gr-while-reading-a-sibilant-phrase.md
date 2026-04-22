# Ver la reducción de ganancia en tiempo real mientras lee una frase sibilante

Use la barra de reducción de ganancia del applet De-Esser para ver cuánta atenuación está aplicando el de-esser en tiempo real. Leer una frase con abundantes sonidos de "S" y "T" mientras observa la barra le permite confirmar que los ajustes de Thresh y Amount funcionan correctamente antes de salir al aire.

## Antes de comenzar

- La etapa De-Ess debe estar habilitada mediante el widget CHAIN. El applet DESS permanece oculto hasta que la etapa esté activa.
- El sub-contenedor DESS debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga clic derecho en la barra de título del sub-contenedor DESS y seleccione la opción para mostrarlo, o haga doble clic en la etapa DeEss en el widget CHAIN para abrir el editor flotante De-Ess.
- Su micrófono y la ruta de audio TX deben estar activos para que el audio en vivo pase a través del de-esser.

## Pasos

1. Abra el sub-contenedor DESS en el contenedor principal PooDoo Audio (TXDSP).
2. Localice la barra de reducción de ganancia — la franja horizontal directamente debajo de la curva de respuesta de la cadena lateral (sidechain).
3. Active el transmisor y lea en voz alta una frase sibilante (por ejemplo, "sixty-six sizzling sausages").
4. Observe cómo la barra de reducción de ganancia se llena desde la derecha con un color rojo suave en cada sonido de "S" o "T". La escala de la barra va de 0 a 24 dB; una marca en la posición de un cuarto desde la derecha indica el punto −6 dB.
5. Si la barra nunca se llena, el de-esser no está activándose — reduzca Thresh hacia un valor más negativo.
6. Si la barra llega al máximo en cada sílaba, no solo en las sibilantes, aumente Thresh hacia 0 dB o reduzca Amount.
7. Procure que la barra alcance aproximadamente la marca de −6 dB en las sibilantes más pronunciadas y que vuelva a vacío entre palabras.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Curva de respuesta de la cadena lateral | — | — | — | Dibuja la forma del filtro de paso de banda; una bola en movimiento marca la frecuencia central actual. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Franja horizontal de rojo suave, rellena desde la derecha. Muestra la atenuación que se aplica en ese momento a la banda de sibilancia. Una marca indica el punto −6 dB. Se actualiza a aproximadamente 30 Hz. |
| Freq | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` | Establece la frecuencia central de la banda de sibilancia. Utiliza mapeo logarítmico. |
| Q | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Establece el ancho de banda de la banda de sibilancia. Un Q mayor produce una banda más estrecha. |
| Thresh | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel por encima del cual el de-esser comienza a atenuar. |
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada en el pico de sibilancia. |

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz, por lo que los transitorios rápidos de "S" pueden aparecer como destellos breves. Esto es normal.
- La bola de frecuencia central en la curva de respuesta de la cadena lateral se mueve junto con Freq. Observar tanto la bola como la barra al mismo tiempo ayuda a confirmar que el de-esser está centrado en la parte correcta de su voz.
- Evite que la barra llegue a 24 dB: eso indica una reducción mayor de la que permite Amount, lo que significa que Thresh está configurado demasiado bajo.

## Solución de problemas

- **La barra de reducción de ganancia permanece vacía durante el habla** — El de-esser no se está activando. Reduzca Thresh (más negativo) hasta que la barra reaccione ante las sibilantes pronunciadas. Confirme también que la etapa De-Ess está habilitada en el widget CHAIN y que el audio está pasando realmente por la cadena TX.
- **La barra de reducción de ganancia se llena continuamente, no solo en las sibilantes** — Thresh es demasiado bajo o Freq está centrado en una frecuencia que domina su voz. Aumente Thresh o desplace Freq hacia una frecuencia más alta donde la sibilancia esté más aislada.
- **El applet DESS no está visible** — La etapa De-Ess no está habilitada. Habilítela mediante el widget CHAIN o haciendo doble clic en la etapa DeEss en el widget CHAIN para abrir el editor flotante y luego activarla desde allí.

## Relacionados

- [Descripción general del De-Esser](overview.md)
- [Ajustar el umbral justo por debajo de los picos más altos de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para lograr el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Desplazar Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Desactivar el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
