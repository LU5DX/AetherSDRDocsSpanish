# Ajuste de Bias para modificar el balance armónico

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando el equilibrio entre armónicos pares e impares que produce el saturación. Úselo para ajustar el carácter de la saturación después de haber configurado Drive.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Drive ya debe estar configurado lo suficientemente alto como para que la curva de transferencia esté visiblemente curvada. Consulte [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).
- Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor tiene el título "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Localice el control Bias en la fila central del editor, a la derecha del selector de modelos A / B / C.
2. Gire Bias desde su valor predeterminado de 0 % hacia valores más altos (hasta 100 %) para desplazar el punto de operación y aumentar la saturación asimétrica.
3. Observe la curva de transferencia: la curva desplaza su punto de curvatura a medida que gira el control. La bola de entrada en vivo rastrea la nueva región de operación en tiempo real.
4. Deténgase cuando el balance armónico suene correcto para su caso de uso.
5. Si el nivel general cambia notablemente, ajuste el control Output para compensarlo. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Descripción de cada control

| Control   | Valor predeterminado                                 | Rango válido                                        |
|-----------|------------------------------------------------------|-----------------------------------------------------|
| Bias (TX) | 0 %                                                  | 0 % a 100 % (interno 0.0 a 1.0)                    |
| Bias (RX) | 0 %                                                  | 0 % a 100 % (interno 0.0 a 1.0)                    |
| RN2       | Alternancia solo para TX (oculto en modo RX). Habilita el denoising neuronal RNNoise en la entrada del micrófono antes de la cadena de DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturación. | Ubicado en el panel flotante StripTubePanel debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) pasan por alto esta etapa. La configuración se persiste a través de AudioEngine. |

El control Bias utiliza un mapeo lineal. El valor mostrado es un porcentaje. Internamente, la configuración se almacena como un valor de 0.0 a 1.0 en `ClientTubeTxBias` (lado TX) o `ClientTubeRxBias` (lado RX).

## Edición de valor en línea

Las vistas compactas de uno y tres controles, y todos los editores basados en controles giratorios, ahora admiten la edición de valor en línea.

1. Haga clic en el valor numérico que se muestra debajo de cualquier control. Un campo de entrada de texto reemplaza la etiqueta del valor.
2. Escriba directamente el valor deseado. Puede incluir unidades (por ejemplo, "5.00 ms", "-6 dB", "12.5") o solo el número.
3. Presione Enter para confirmar el valor. El control se mueve inmediatamente a la nueva configuración.
4. El campo acepta automáticamente formatos numéricos adaptados a la configuración regional (coma como separador decimal en las regiones donde sea estándar).
5. Si escribe un valor no válido, el control vuelve a su configuración anterior.

**Nota:** El editor en línea está disponible en todas las instancias de ClientCompKnob en la aplicación: Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release y cualquier otro control basado en perilla que muestre su valor numérico.

## Consejos

- Bias interactúa con el carácter del tubo seleccionado. Pruebe cada uno de A, B y C para escuchar cómo el mismo valor de Bias produce diferentes resultados armónicos con diferentes modelos.
- El control Bias también está presente en el mosaico del applet acoplado (la fila compacta de cinco controles debajo de la curva de transferencia), por lo que puede realizar ajustes rápidos sin abrir el editor completo.
- Los cambios realizados en el mosaico acoplado y en el editor flotante se mantienen sincronizados; un temporizador de 30 Hz mantiene ambas vistas actualizadas.
- Para introducir valores de Bias con el editor en línea, haga clic en la pantalla de porcentaje (por ejemplo, "0 %") debajo del control y escriba un número entre 0 y 100.

## Atenuación de bypass

Cuando la etapa Tube está desviada, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve a la opacidad completa tan pronto como la etapa se vuelve a habilitar.

## Solución de problemas

- **El control Bias no tiene efecto audible** — Drive puede estar en o cerca de 0.00 dB. Bias solo desplaza el punto de operación de manera significativa cuando la curva ya está curvada. Aumente Drive primero.
- **El nivel cambia cuando se ajusta Bias** — Esto es esperado. La asimetría introducida por Bias puede aumentar o disminuir la salida aparente. Ajuste el control Output para compensar.
- **El mosaico acoplado aparece atenuado** — La etapa Tube está desviada. Vuelva a habilitarla en el lado TX o RX. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- **El editor en línea no acepta el valor escrito** — Asegúrese de escribir un número simple o un número con punto decimal opcional y signo. Las comas solo se permiten en regiones donde sirven como separadores decimales.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
