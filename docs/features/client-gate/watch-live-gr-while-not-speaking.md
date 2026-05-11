# Observe la reducción de ganancia en vivo sin hablar

El medidor de reducción de ganancia y la curva de transferencia se actualizan en tiempo real incluso cuando no está transmitiendo. Observarlos mientras la sala está en silencio le indica qué tan profundo está cortando la compuerta en cualquier momento, permitiéndole juzgar si los valores de umbral y piso son apropiados antes de activar la transmisión.

## Antes de comenzar

- La etapa de compuerta debe estar habilitada en el lado que desea observar. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si el applet no está visible.
- El subcontenedor "Aetherial TX Gate" o "Aetherial AGC-G (RX)" debe estar abierto dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Abra el panel de applets si aún no está visible: `View > Applet Panel`.
2. Localice el subcontenedor "Aetherial TX Gate" (lado TX) o "Aetherial AGC-G (RX)" (lado RX).
3. Permanezca en silencio — no hable ni active la transmisión del radio.
4. Observe la barra ámbar de reducción de ganancia. Mientras la entrada se mantenga por debajo del nivel Thresh, la barra se llena desde la derecha, mostrando la profundidad de atenuación aplicada.
5. Observe la bola de entrada en la curva de transferencia. La bola se sitúa en la región inferior izquierda de la curva cuando la compuerta está cerrada (entrada por debajo del umbral) y se mueve hacia arriba y a la derecha cuando la compuerta se abre.
6. Note hasta dónde se llena la barra. Si alcanza o supera la marca de -15 dB, la compuerta está aplicando al menos 15 dB de atenuación — el valor predeterminado de Floor.

## Atenuación por bypass

Cuando la etapa de compuerta está en bypass, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente al 55% del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva de EQ y proporciona una indicación visual rápida de que la etapa no está procesando audio. El applet vuelve al brillo completo tan pronto como se vuelve a habilitar la etapa.

## Qué hace cada control

| Control                | Tipo                                                                                                                                                                                                        | Valor predeterminado                                                                                                                                                                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Transfer curve         | Indicador                                                                                                                                                                                                   | —                                                                                                                                                                                                                                                                    |
| Input ball             | Indicador                                                                                                                                                                                                   | —                                                                                                                                                                                                                                                                    |
| Hysteresis band        | Indicador                                                                                                                                                                                                   | —                                                                                                                                                                                                                                                                    |
| Gain-reduction bar     | Medidor                                                                                                                                                                                                     | —                                                                                                                                                                                                                                                                    |
| Thresh                 | Perilla                                                                                                                                                                                                     | -40.0 dB                                                                                                                                                                                                                                                             |
| Ratio                  | Perilla                                                                                                                                                                                                     | 2.0                                                                                                                                                                                                                                                                  |
| Return                 | Perilla                                                                                                                                                                                                     | 2.0 dB                                                                                                                                                                                                                                                               |
| Release                | Perilla                                                                                                                                                                                                     | 100 ms                                                                                                                                                                                                                                                               |
| Floor                  | Perilla                                                                                                                                                                                                     | -15.0 dB                                                                                                                                                                                                                                                             |

**Barra de reducción de ganancia:** Franja ámbar horizontal, rellena desde la derecha. La escala máxima es de 40 dB. Una marca en -15 dB señala el valor predeterminado de Floor. Vacía significa que no hay atenuación; llena completamente desde la derecha indica que la compuerta está cortando a la profundidad máxima establecida por Floor.

**Curva de transferencia / Bola de entrada:** La curva estática muestra la relación entrada-salida del expansor. La bola en vivo sigue el nivel de entrada actual, moviéndose por debajo o por encima del umbral en tiempo real.

**Banda de histéresis:** Una banda vertical cian suave dibujada en la curva de transferencia entre (Thresh − Return) y Thresh. Hace visible la zona de retención de la compuerta: la compuerta se abre cuando la entrada supera Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return. La banda desaparece cuando Return está configurado en 0.

**Perilla Return:** Establece el ancho de la banda muerta de histéresis en dB. Aumentar Return evita que la compuerta oscile cuando la entrada se mantiene cerca del umbral. La etiqueta se muestra en el formato X.XX dB.

## Consejos

- El medidor se actualiza aproximadamente cada 33 ms, por lo que la barra sigue la reducción de ganancia con suficiente precisión para capturar eventos de ruido breves.
- Los cambios en las perillas realizados en el editor flotante de compuerta se reflejan en el applet dentro del mismo ciclo de 33 ms, por lo que puede dejar el applet visible como un medidor en vivo mientras ajusta en el editor.
- Una barra que nunca se vacía completamente mientras está en silencio significa que la compuerta siempre está atenuando — la entrada nunca supera Thresh incluso cuando deja de hablar. Esto es un comportamiento normal y esperado para una compuerta de ruido en reposo.
- Si la compuerta oscila — se abre y cierra rápidamente mientras habla cerca del umbral — aumente Return para ampliar la banda muerta de histéresis. La banda cian en la curva de transferencia se vuelve más ancha a medida que lo hace, proporcionándole una indicación visual de cuánta banda muerta está activa.
- Si el mosaico del applet aparece atenuado, la etapa de compuerta está en bypass y no hay procesamiento activo. Vuelva a habilitar la etapa para restaurar el brillo completo y reanudar la atenuación.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Tune return / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
