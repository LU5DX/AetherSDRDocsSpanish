# Aclarar u oscurecer la señal saturada con Tone

Utilice el mando Tone para inclinar el carácter espectral de la señal saturada: los valores negativos la oscurecen y la vuelven más cálida, los valores positivos la aclaran y la hacen más presente. Tone funciona de forma independiente tanto en el lado de TX (Aetherial Mic-PreAmp) como en el de RX (Aetherial Dynamic Tube).

## Antes de comenzar

- La etapa de tubo debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Applet Panel. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante, o localice el subcontenedor directamente en el panel.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX).
2. Encuentre el mando etiquetado como **Tone** — es el segundo mando desde la izquierda, entre Drive y Bias.
3. Gire el mando **Tone** hacia la izquierda (hacia −1.00) para oscurecer la señal saturada, o hacia la derecha (hacia +1.00) para aclararla.
4. Lea el valor actual en la etiqueta debajo del mando. La etiqueta muestra dos decimales (p. ej., `−0.50` o `0.75`).
5. Para restablecer Tone a su valor predeterminado, haga doble clic en el mando **Tone**.
6. Para escribir un valor preciso directamente, haga clic en la visualización del valor debajo del mando Tone. Aparecerá un pequeño campo de entrada de texto. Escriba el valor deseado y presione **Enter** o haga clic en otro lugar para confirmar. El valor se ajusta automáticamente al rango válido. Presione **Escape** para cancelar la edición y volver al valor anterior.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste (TX) | Clave de ajuste (RX) | Notas |
|---|---|---|---|---|---|
| Tone (TX) | 0.00 | −1.0 a 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Fila central del editor, a la izquierda del selector de modelo |
| Drive | 0.00 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Columna izquierda del editor |
| Bias | 0 % | 0.0 a 1.0 | `ClientTubeTxBias` | `ClientTubeRxBias` | Fila central del editor, a la derecha del selector de modelo |
| Output | 0.00 dB | −24.0 a 12.0 dB | `ClientTubeTxOutputDb` | `ClientTubeRxOutputDb` | Columna izquierda del editor |
| Dry/Wet | 100 % | 0.0 a 1.0 | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Columna izquierda del editor (mando superior) |
| Envelope | 0 % | −1.0 a 1.0 | `ClientTubeTxEnvelope` | `ClientTubeRxEnvelope` | Columna derecha del editor |
| Attack | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` | `ClientTubeRxAttackMs` | Columna derecha del editor |
| Release | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` | `ClientTubeRxReleaseMs` | Columna derecha del editor |
| RN2 | desmarcado | — | — | — | Alternancia solo para TX (oculto en modo RX). Activa el denoizador neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz; los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. Ajuste persistente mediante AudioEngine |

### Modelos de carácter de tubo

| Etiqueta | Valor predeterminado | Clave de ajuste | Comportamiento |
|---|---|---|---|
| A | marcado | `ClientTubeTxModel` / `ClientTubeRxModel` | Selecciona el modelo de carácter de tubo A. Excluyente con B y C |
| B | desmarcado | `ClientTubeTxModel` / `ClientTubeRxModel` | Selecciona el modelo de carácter de tubo B. Excluyente con A y C |
| C | desmarcado | `ClientTubeTxModel` / `ClientTubeRxModel` | Selecciona el modelo de carácter de tubo C. Excluyente con A y B |

El selector de modelo aparece como tres botones de alternancia de color ámbar en la fila central del editor, entre Tone y Bias. El valor de respaldo se almacena como un entero (0 = A, 1 = B, 2 = C) en la clave de ajuste correspondiente.

## Medidor de nivel de salida

El editor flotante (con el título **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en la columna del extremo derecho. Este medidor muestra el nivel pico posterior a la saturación y utiliza balística de ataque rápido / liberación lenta.

| Rango de nivel | Color del medidor |
|---|---|
| −60 a −12 dB | Verde |
| −12 a −6 dB | Lima |
| −6 a −3 dB | Ámbar |
| Por encima de −3 dB | Rojo |

El medidor solo es visible en el editor flotante. No aparece en el mosaico del applet acoplado en el Applet Panel.

## Indicador de curva de transferencia

El mosaico del applet acoplado muestra un widget compacto de **curva de transferencia** que dibuja la curva de transferencia del tubo actualmente configurada con una bola de entrada en vivo. La bola recorre la curva al nivel de entrada actual, visualizando el régimen de saturación en tiempo real.

## Atenuación por bypass

Cuando la etapa de tubo está en bypass, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en el widget de la curva EQ cuando esa etapa está en bypass. La opacidad vuelve al valor completo tan pronto como la etapa se vuelve a habilitar. El editor flotante no se ve afectado por esta atenuación.

## Consejos

- Tone interactúa con Drive: un valor alto de Drive produce más armónicos de saturación, por lo que los ajustes de Tone se vuelven más audibles a medida que aumenta Drive. Ajuste primero Drive, luego use Tone para dar forma al resultado.
- Si tiene el editor flotante abierto junto al applet, ambos reflejan el mismo valor. Los cambios realizados en uno se sincronizan con el otro en aproximadamente 33 ms.
- Un valor de Tone de 0.00 deja el balance espectral de la señal saturada sin cambios.
- Observe el medidor **OUT** en el editor flotante para detectar recortes posteriores a la saturación. Si el medidor llega al rojo, reduzca el mando **Output** o baje **Drive**.
- El editor de valores en línea admite el análisis de números según la configuración regional. Ingrese `12,5` en una configuración regional de coma decimal, o elimine unidades como `12.5 ms` y el editor analizará la parte numérica.

## Solución de problemas

- **El mando Tone no tiene efecto audible** — la etapa de tubo puede estar en bypass. Confirme que la etapa esté activa en el widget CHAIN del lado correspondiente. También verifique que Mix esté por encima del 0 %; una señal completamente seca (Mix al 0 %) pasa a través del modelo de tubo pero no mezcla nada de la salida húmeda.
- **La posición del mando no coincide con lo que espera después de recargar** — el valor se guarda automáticamente cada vez que el mando cambia. Si `ClientTubeTxTone` o `ClientTubeRxTone` falta o está dañado en su archivo de ajustes, el valor vuelve al valor predeterminado de 0.00.
- **El medidor OUT no es visible** — el medidor solo aparece en el editor flotante. Haga doble clic en la etapa TUBE en el widget CHAIN para abrirlo.
- **El mosaico del applet aparece atenuado** — la etapa de tubo está en bypass. Habilite la etapa en el widget CHAIN para restaurar la opacidad completa.
- **El editor en línea muestra un borde rojo y no acepta entrada** — el editor solo aparece cuando hace clic en la visualización del valor. Si no ve el editor, asegúrese de estar haciendo clic directamente en el texto del valor numérico debajo del mando, no en el mando mismo. El editor vuelve a una apariencia similar a una etiqueta cuando no está enfocado.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Modulate the tube curve with Envelope](modulate-the-tube-curve-with-envelope.md)
- Type exact values with the value popup editor
