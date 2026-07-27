# Ajuste de Bias para modificar el balance armónico

El mando Bias desplaza el punto de operación en la curva de transferencia del tubo, modificando el equilibrio entre armónicos pares e impares que produce el saturación. Úselo para ajustar finamente el carácter de la saturación después de haber configurado Drive.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Drive ya debe estar configurado lo suficientemente alto como para que la curva de transferencia esté visiblemente curvada. Consulte [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).
- Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Localice el mando Bias en la fila central del editor, a la derecha del selector de modelo A / B / C.
2. Gire Bias desde su valor predeterminado de 0 % hacia valores más altos (hasta 100 %) para desplazar el punto de operación y aumentar la saturación asimétrica.
3. Observe la curva de transferencia: la curva desplaza su punto de curvatura a medida que gira el mando. La bola de entrada en vivo rastrea la nueva región de operación en tiempo real.
4. Deténgase cuando el balance armónico suene correcto para su caso de uso.
5. Si el nivel general cambia notablemente, ajuste el mando Output para compensarlo. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control   | Valor predeterminado                                                                                                                                                             | Rango válido                                                                                                                                                                                               |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Bias (TX) | 0 %                                                                                                                                                                              | 0 % a 100 % (interno 0.0 a 1.0)                                                                                                                                                                        |
| Bias (RX) | 0 %                                                                                                                                                                              | 0 % a 100 % (interno 0.0 a 1.0)                                                                                                                                                                        |
| RN2       | Alternancia solo en TX (oculto en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena de DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. | Ubicado en el panel StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se persiste a través de AudioEngine. |

El mando Bias utiliza un mapeo lineal. El valor mostrado es un porcentaje. Internamente, la configuración se almacena como un valor de 0.0 a 1.0 en `ClientTubeTxBias` (lado TX) o `ClientTubeRxBias` (lado RX).

## Control de envolvente

El mando Envelope modula dinámicamente la excitación del tubo según el nivel de la señal. Cuando se configura en valores positivos, el tubo se calienta (más saturación) en los transitorios fuertes. Cuando se configura en valores negativos, el tubo reduce la saturación en los picos, comprimiendo los armónicos.

| Control        | Valor predeterminado | Rango válido               | Comportamiento                                                                                                                                                                        |
|----------------|----------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Envelope (TX)  | 0 %                  | -100 % a +100 % (interno -1.0 a +1.0) | Mapeo lineal. Los valores positivos aumentan la excitación en los transitorios; los valores negativos la reducen, comprimiendo dinámicamente los armónicos. |
| Envelope (RX)  | 0 %                  | -100 % a +100 % (interno -1.0 a +1.0) | Mismo comportamiento que en TX. |

Cuando Envelope se configura en cualquier valor distinto de cero, los mandos Attack y Release controlan la rapidez con la que el seguidor de envolvente responde a los cambios en el nivel de la señal:

| Control   | Valor predeterminado | Rango válido         | Comportamiento                                                                           |
|-----------|----------------------|-----------------------|-------------------------------------------------------------------------------------------|
| Attack    | 5.00 ms              | 0.1 a 30.0 ms       | Mapeo exponencial (0.1 * 300^n). Define la rapidez con la que el seguidor de envolvente responde a los niveles crecientes. |
| Release   | 35.00 ms             | 10.0 a 500.0 ms     | Mapeo exponencial (10 * 50^n). Define la rapidez con la que el seguidor de envolvente se recupera después de que los niveles bajan. |

## RN2 (solo TX)

La alternancia RN2 habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena de DSP en el lado TX. Esta alternancia está oculta en el modo RX.

| Control | Valor predeterminado | Comportamiento                                                                                                                                                                       |
|---------|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RN2     | desmarcado            | Alternancia solo en TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada de micrófono antes de la cadena de DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. Ubicado en el panel StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se persiste a través de AudioEngine. |

## Edición de valor en línea

Las vistas compactas de uno y tres mandos, y todos los editores basados en mandos, ahora admiten la edición de valor en línea.

1. Haga clic en el valor numérico que se muestra debajo de cualquier mando. Un campo de entrada de texto reemplaza la etiqueta del valor.
2. Escriba el valor deseado directamente. Puede incluir unidades (por ejemplo, "5.00 ms", "-6 dB", "12.5") o solo el número.
3. Presione Enter para confirmar el valor. El mando se mueve inmediatamente a la nueva configuración.
4. El campo acepta automáticamente formatos numéricos que reconocen la configuración regional (separador decimal de coma para regiones donde es estándar).
5. Si escribe un valor no válido, el mando vuelve a su configuración anterior.

**Nota:** El editor en línea está disponible en todas las instancias de ClientCompKnob en toda la aplicación: Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release y cualquier otro control basado en mando que muestre su valor numérico.

## Consejos

- Bias interactúa con el carácter de tubo seleccionado. Pruebe cada uno de A, B y C para escuchar cómo el mismo valor de Bias produce diferentes resultados armónicos con diferentes modelos.
- El mando Bias también está presente en el mosaico de applet acoplado (la fila compacta de cinco mandos debajo de la curva de transferencia), para que pueda hacer ajustes rápidos sin abrir el editor completo.
- Los cambios realizados en el mosaico acoplado y el editor flotante se mantienen sincronizados; un temporizador de 30 Hz mantiene ambas vistas actualizadas.
- Para introducir valores de Bias con el editor en línea, haga clic en la visualización del porcentaje (por ejemplo, "0 %") debajo del mando y escriba un número entre 0 y 100.
- Envelope sigue la señal y requiere configuraciones de Attack/Release distintas de cero para funcionar. Si Envelope está configurado pero Attack y Release están en sus valores predeterminados, intente ajustarlos para obtener la respuesta dinámica deseada.

## Atenuación al omitir

Cuando la etapa Tube está desviada (bypassed), todo el mosaico de applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa.

## Solución de problemas

- **El mando Bias no tiene efecto audible**: es posible que Drive esté en o cerca de 0.00 dB. Bias solo desplaza el punto de operación de manera significativa cuando la curva ya está curvada. Aumente Drive primero.
- **Cambios de nivel al ajustar Bias**: esto es esperado. La asimetría introducida por Bias puede aumentar o disminuir la salida aparente. Ajuste el mando Output para compensarlo.
- **El mosaico acoplado aparece atenuado**: la etapa Tube está desviada. Vuelva a habilitarla en el lado TX o RX. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- **El editor en línea no acepta el valor escrito**: asegúrese de escribir un número simple o un número con punto decimal opcional y signo. Las comas solo están permitidas en configuraciones regionales donde sirven como separadores decimales.
- **Envelope no tiene efecto**: verifique que Envelope esté configurado en un valor distinto de cero. También compruebe que Attack y Release no estén configurados en valores extremos que impidan que el seguidor de envolvente responda a la señal.
- **La alternancia RN2 no es visible**: la alternancia RN2 solo aparece en el modo TX y en modos de voz (no en modos digitales). Cambie a un modo de voz o verifique que se encuentra en el lado TX.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- Use la mezcla Dry/Wet para controlar la mezcla de saturación
