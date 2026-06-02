# Aclarar u oscurecer la señal saturada con Tone

Utilice el mando Tone para inclinar el carácter espectral de la señal saturada: los valores negativos la oscurecen y la hacen más cálida, los valores positivos la aclaran y la hacen más presente. Tone funciona de forma independiente tanto en el lado de TX (Aetherial Mic-PreAmp) como en el de RX (Aetherial Dynamic Tube).

## Antes de comenzar

- La etapa de válvula debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- El subcontenedor Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX) debe estar visible en el Applet Panel. Haga doble clic en la etapa TUBE en el widget CHAIN para abrir el editor flotante, o localice el subcontenedor directamente en el panel.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del applet Aetherial Mic-PreAmp (TX) o Aetherial Dynamic Tube (RX).
2. Encuentre el mando etiquetado **Tone** — es el segundo mando desde la izquierda, entre Drive y Bias.
3. Gire el mando **Tone** hacia la izquierda (hacia −1.00) para oscurecer la señal saturada, o hacia la derecha (hacia +1.00) para aclararla.
4. Lea el valor actual de la etiqueta debajo del mando. La etiqueta muestra dos decimales (p. ej., `−0.50` o `0.75`).
5. Para restablecer Tone a su valor predeterminado, haga doble clic en el mando **Tone**.
6. Para escribir un valor preciso directamente, haga clic en la visualización del valor debajo del mando Tone. Aparecerá un pequeño campo de entrada de texto. Escriba el valor deseado y presione **Enter** o haga clic en otro lugar para confirmarlo. El valor se ajusta automáticamente al rango válido. Presione **Escape** para cancelar la edición y volver al valor anterior.

## Función de cada control

| Control   | Valor predeterminado                                                                                                                                                               | Rango válido                                                                                                                                                                                              |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tone (TX) | 0.00                                                                                                                                                                                | −1.0 a 1.0                                                                                                                                                                                               |
| Tone (RX) | 0.00                                                                                                                                                                                | −1.0 a 1.0                                                                                                                                                                                               |
| Drive     | 0.00 dB                                                                                                                                                                             | 0.0 a 24.0 dB                                                                                                                                                                                            |
| Bias      | 0 %                                                                                                                                                                                 | 0.0 a 1.0                                                                                                                                                                                                |
| Output    | 0.00 dB                                                                                                                                                                             | −24.0 a 12.0 dB                                                                                                                                                                                          |
| Dry/Wet   | 100 %                                                                                                                                                                               | 0.0 a 1.0                                                                                                                                                                                                |
| Envelope  | 0 %                                                                                                                                                                                 | −1.0 a 1.0                                                                                                                                                                                               |
| Attack    | 5.00 ms                                                                                                                                                                             | 0.1 a 30.0 ms                                                                                                                                                                                            |
| Release   | 35.00 ms                                                                                                                                                                            | 10.0 a 500.0 ms                                                                                                                                                                                          |
| RN2       | Activación solo para TX (oculta en modo RX). Activa el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. | Ubicado en el panel flotante StripTubePanel debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva a través de AudioEngine. |

## Medidor de nivel de salida

El editor flotante (titulado **Aetherial Tube — TX** o **Aetherial Tube — RX**) incluye un medidor de nivel **OUT** en la columna del extremo derecho. Este medidor muestra el nivel pico posterior a la saturación y utiliza balística de ataque rápido / liberación lenta.

| Rango de nivel | Color del medidor |
|---|---|
| −60 a −12 dB | Verde |
| −12 a −6 dB | Lima |
| −6 a −3 dB | Ámbar |
| Por encima de −3 dB | Rojo |

El medidor solo es visible en el editor flotante. No aparece en el mosaico del applet acoplado en el Applet Panel.

## Atenuación por derivación

Cuando la etapa de válvula está derivada, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en el widget de la curva EQ cuando esa etapa está derivada. La opacidad vuelve al completo tan pronto como se reactiva la etapa. El editor flotante no se ve afectado por esta atenuación.

## Consejos

- Tone interactúa con Drive: un valor alto de Drive produce más armónicos de saturación, por lo que los ajustes de Tone se vuelven más audibles a medida que aumenta Drive. Ajuste primero Drive y luego use Tone para dar forma al resultado.
- Si tiene el editor flotante abierto junto con el applet, ambos reflejan el mismo valor. Los cambios realizados en uno se sincronizan con el otro en aproximadamente 33 ms.
- Un valor de Tone de 0.00 deja el equilibrio espectral de la señal saturada sin cambios.
- Vigile el medidor **OUT** en el editor flotante para detectar recortes posteriores a la saturación. Si el medidor alcanza el rojo, reduzca el mando **Output** o baje **Drive**.
- El editor de valores en línea admite el análisis de números según la configuración regional. Ingrese `12,5` en una configuración regional con coma decimal, o elimine unidades como `12.5 ms` y el editor analizará la parte numérica.

## Solución de problemas

- **El mando Tone no tiene efecto audible** — la etapa de válvula puede estar derivada. Confirme que la etapa esté activa en el widget CHAIN en el lado correspondiente. También verifique que Mix esté por encima del 0 %; una señal completamente seca (Mix al 0 %) pasa a través del modelo de válvula pero no mezcla nada de la salida procesada.
- **La posición del mando no coincide con lo esperado después de recargar** — el valor se guarda automáticamente cada vez que cambia el mando. Si `ClientTubeTxTone` o `ClientTubeRxTone` falta o está dañado en su archivo de configuración, el valor vuelve al predeterminado de 0.00.
- **El medidor OUT no es visible** — el medidor solo aparece en el editor flotante. Haga doble clic en la etapa TUBE en el widget CHAIN para abrirlo.
- **El mosaico del applet aparece atenuado** — la etapa de válvula está derivada. Active la etapa en el widget CHAIN para restaurar la opacidad completa.
- **El editor en línea muestra un borde rojo y no acepta entrada** — el editor solo aparece cuando hace clic en la visualización del valor. Si no ve el editor, asegúrese de hacer clic directamente en el texto del valor numérico debajo del mando, no en el mando mismo. El editor vuelve a una apariencia similar a una etiqueta cuando no está enfocado.

## Relacionados

- [Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX) overview](overview.md)
- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Modulate the tube curve with Envelope](modulate-the-tube-curve-with-envelope.md)
- Type exact values with the value popup editor
