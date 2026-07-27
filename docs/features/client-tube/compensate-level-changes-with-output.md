# Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

El saturador de válvula dinámica del lado cliente de AetherSDR agrega riqueza armónica moldeando la señal a través de un modelo de válvula con barrido de polarización. El sistema instancia dos copias independientes: una para la cadena de transmisión ("Aetherial Mic-PreAmp") y otra para la cadena de recepción ("Aetherial Dynamic Tube").

## Abrir los controles de la válvula

- **Mosaico de applet acoplado**: Haga clic en "Aetherial Mic-PreAmp" (TX) o "Aetherial Dynamic Tube" (RX) en el panel de applets. El mosaico compacto muestra una curva de transferencia con una bola de entrada en vivo y cinco perillas de ajuste.
- **Editor flotante**: Haga doble clic en la etapa TUBE en el widget CHAIN, o haga clic derecho y seleccione "Open editor". El editor sin marco se titula "Aetherial Tube — TX" o "Aetherial Tube — RX" y muestra el diseño completo de nueve perillas con un selector de carácter de válvula y un medidor de nivel de salida en vivo.

## Modelos de carácter de válvula

La etapa de válvula ofrece tres modelos de carácter de válvula exclusivos:

| Botón | Predeterminado | Comportamiento |
|---|---|---|
| A | Marcado | Selecciona el modelo de válvula A. Ámbar cuando está marcado. |
| B | Sin marcar | Selecciona el modelo de válvula B. Ámbar cuando está marcado. Exclusivo con A y C. |
| C | Sin marcar | Selecciona el modelo de válvula C. Ámbar cuando está marcado. Exclusivo con A y B. |

Los botones forman parte de un QButtonGroup exclusivo. El modelo seleccionado se persiste en `ClientTubeTxModel` / `ClientTubeRxModel` como un entero (0, 1 o 2).

## Edición de valor en línea

Ahora puede hacer clic en la visualización del valor de una perilla para ingresar al modo de texto:

1. **Haga clic en el texto del valor** debajo de cualquier perilla para abrir un editor en línea. El editor aparece como un rectángulo oscuro con un borde cian.
2. **Escriba un nuevo valor** y presione Enter para aplicarlo. El valor se limita al rango válido de la perilla.
3. **Haga clic en otro lugar** o presione Tab para confirmar el valor.
4. **Presione Escape** para cancelar la edición y revertir al valor anterior.

El editor en línea admite el análisis decimal con reconocimiento de configuración regional, por lo que valores como "12,5" funcionan en configuraciones regionales con coma decimal. También puede incluir texto de unidad; el analizador elimina los caracteres no numéricos automáticamente.

## Controles de perilla

El mosaico de applet acoplado muestra cinco perillas en una fila: Drive, Tone, Bias, Output, Dry/Wet. El editor flotante agrega cuatro perillas más en una columna derecha: Envelope, Attack, Release y los botones del selector de Modelo.

Los colores de las perillas (fondo del anillo, arco, puntero, etiqueta y texto del valor) siguen el tema actual. El primer plano de la perilla del saturador de válvula utiliza el color del tema `color.accent.dim`, mientras que el texto de la etiqueta y el valor utilizan `color.text.secondary` y `color.text.primary` respectivamente. El contenedor del applet de válvula está registrado bajo `applet/tube` para la personalización del tema.

### Drive

- **Formato de etiqueta**: `X.XX dB`
- **Predeterminado**: 0.00 dB
- **Rango válido**: 0.0 a 24.0 dB
- **Clave de ajuste (TX)**: `ClientTubeTxDriveDb`
- **Clave de ajuste (RX)**: `ClientTubeRxDriveDb`

Mapeo lineal. Introduce más señal en la etapa de válvula. Columna izquierda del editor.

### Tone

- **Formato de etiqueta**: `X.XX`
- **Predeterminado**: 0.00
- **Rango válido**: -1.0 a 1.0
- **Clave de ajuste (TX)**: `ClientTubeTxTone`
- **Clave de ajuste (RX)**: `ClientTubeRxTone`

Mapeo lineal. Los valores negativos oscurecen la señal saturada; los valores positivos la iluminan. Fila central del editor, a la izquierda del selector de Modelo.

### Bias

- **Formato de etiqueta**: Porcentaje (p. ej., `50 %`)
- **Predeterminado**: 0 %
- **Rango válido**: 0.0 a 1.0
- **Clave de ajuste (TX)**: `ClientTubeTxBias`
- **Clave de ajuste (RX)**: `ClientTubeRxBias`

Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla armónica. Fila central del editor, a la derecha del selector de Modelo.

### Output

- **Formato de etiqueta**: `X.XX dB`
- **Predeterminado**: 0.00 dB
- **Rango válido**: -24.0 a 12.0 dB
- **Clave de ajuste (TX)**: `ClientTubeTxOutputDb`
- **Clave de ajuste (RX)**: `ClientTubeRxOutputDb`

Ganancia de compensación/recorte posterior a la válvula. Columna izquierda del editor.

### Dry/Wet

- **Formato de etiqueta**: Porcentaje (p. ej., `100 %`)
- **Predeterminado**: 100 %
- **Rango válido**: 0.0 a 1.0
- **Clave de ajuste (TX)**: `ClientTubeTxDryWet`
- **Clave de ajuste (RX)**: `ClientTubeRxDryWet`

Mapeo lineal. Mezcla seco/húmedo (100 % = señal completamente saturada). Columna izquierda del editor (perilla superior).

### Envelope

- **Formato de etiqueta**: Porcentaje con signo (p. ej., `+25 %`, `-50 %`)
- **Predeterminado**: 0 %
- **Rango válido**: -1.0 a 1.0
- **Clave de ajuste (TX)**: `ClientTubeTxEnvelope`
- **Clave de ajuste (RX)**: `ClientTubeRxEnvelope`

Mapeo lineal (-1.0 a +1.0). Los valores positivos aumentan la excursión en los transitorios (la válvula se calienta más en los picos fuertes); los valores negativos la reducen, comprimiendo los armónicos dinámicamente. Columna derecha del editor.

### Attack

- **Formato de etiqueta**: `X.XX ms` (por debajo de 10 ms), `X.X ms` (por encima de 10 ms)
- **Predeterminado**: 5.00 ms
- **Rango válido**: 0.1 a 30.0 ms
- **Clave de ajuste (TX)**: `ClientTubeTxAttackMs`
- **Clave de ajuste (RX)**: `ClientTubeRxAttackMs`

Mapeo exponencial (0.1 * 300^n). Establece la rapidez con la que el seguidor de envolvente responde a los niveles crecientes cuando Envelope ≠ 0. Columna derecha del editor.

### Release

- **Formato de etiqueta**: `X.XX ms` (por debajo de 100 ms), `X.X ms` (por encima de 100 ms)
- **Predeterminado**: 35.00 ms
- **Rango válido**: 10.0 a 500.0 ms
- **Clave de ajuste (TX)**: `ClientTubeTxReleaseMs`
- **Clave de ajuste (RX)**: `ClientTubeRxReleaseMs`

Mapeo exponencial (10 * 50^n). Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles caen cuando Envelope ≠ 0. Columna derecha del editor.

## Visualización de la curva de transferencia

El ClientTubeCurveWidget en modo compacto dibuja la curva de transferencia de válvula configurada actualmente con una bola en vivo en el nivel de entrada. El widget de curva utiliza colores conscientes del tema:

| Elemento | Clave del tema |
|---|---|
| Fondo | `color.background.0` |
| Marco | `color.background.1` |
| Líneas de cuadrícula | `color.background.1` |
| Ejes | `color.background.1` |
| Curva | `color.accent.dim` (cian) |
| Resplandor de la bola | `color.accent.warning` |
| Núcleo de la bola | `color.text.primary` |

La bola se mueve a lo largo de la curva a medida que cambia el nivel de entrada, visualizando el régimen de saturación.

## Medidor de nivel de salida

El editor flotante incluye un medidor de nivel de pico **OUT** (el widget `ClientLevelMeter`) ubicado en el extremo derecho del panel del editor. Muestra el nivel de pico posterior a la saturación con balística de ataque rápido y liberación lenta y utiliza las siguientes bandas de color:

| Color | Rango de nivel |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor solo es visible en el editor flotante, no en el mosaico de applet acoplado. Se actualiza continuamente junto con los controles de perilla siempre que el editor flotante esté abierto.

## RN2 (Reducción de ruido solo para TX)

El editor flotante solo para TX incluye un botón de alternancia **RN2** ubicado debajo del medidor de nivel de salida. Este control habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP, suprimiendo el ruido de fondo antes de que llegue al gate, compresor o saturador.

- La alternancia RN2 está oculta en el modo RX.
- Disponible solo en modos de voz. Los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa.
- El ajuste se conserva a través del AudioEngine.

## Atenuación por bypass

Cuando la etapa de válvula está en bypass, todo el mosaico de applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % de lo normal). Esto coincide con el efecto de atenuación utilizado en el mosaico de la curva EQ y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa.

## Consejos

- Si aumentar Drive incrementa el volumen más de lo deseado, reduzca Output en una cantidad equivalente para mantener el nivel neto consistente.
- Use el medidor **OUT** en el editor flotante para verificar que la señal posterior a la válvula se mantenga por debajo de −3 dB (rojo) en condiciones operativas normales.
- Los cambios realizados en el editor flotante y en el applet acoplado se mantienen sincronizados. Un temporizador de sondeo de 30 Hz mantiene actualizadas ambas vistas, por lo que ajustar cualquier control en una ubicación se refleja inmediatamente en la otra.
- Haga clic en la visualización del valor de cualquier perilla en el editor flotante para escribir un valor exacto en lugar de arrastrar la perilla.
- Cuando el mosaico del applet aparece atenuado, la etapa de válvula está en bypass. Vuelva a habilitarla antes de realizar ajustes; de lo contrario, los controles no tendrán efecto en la señal en vivo.
- Active RN2 en la pestaña TX para reducir el ruido de fondo antes de que llegue a la etapa de saturación de válvula.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Parallel-blend saturation with Mix](parallel-blend-saturation-with-mix.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
