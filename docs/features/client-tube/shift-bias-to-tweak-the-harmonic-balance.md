# Ajuste de Bias para modificar el balance armónico

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando el equilibrio entre armónicos pares e impares que produce el saturador. Úselo para afinar el carácter de la saturación después de haber ajustado Drive.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- Drive ya debería estar lo suficientemente alto como para que la curva de transferencia se vea visiblemente curvada. Consulte [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).
- Abra el editor flotante haciendo doble clic en la etapa TUBE del widget CHAIN en el lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Localice el control Bias en la fila central del editor, a la derecha del selector de modelo A / B / C.
2. Gire Bias desde su valor predeterminado de 0 % hacia valores más altos (hasta 100 %) para desplazar el punto de operación y aumentar la saturación asimétrica.
3. Observe la curva de transferencia: la curva desplaza su punto de curvatura a medida que gira el control. La bola de entrada en vivo rastrea la nueva región de operación en tiempo real.
4. Deténgase cuando el balance armónico suene correcto para su caso de uso.
5. Si el nivel general cambia notablemente, ajuste el control Output para compensar. Consulte [Compensate level changes with Output](compensate-level-changes-with-output.md).

## Función de cada control

| Control   | Valor predeterminado | Rango válido |
|-----------|-----------------------|--------------|
| Bias (TX) | 0 %                   | 0 % a 100 % (interno 0.0 a 1.0) |
| Bias (RX) | 0 %                   | 0 % a 100 % (interno 0.0 a 1.0) |

El control Bias utiliza un mapeo lineal. El valor mostrado es un porcentaje. Internamente, el ajuste se almacena como un valor de 0.0 a 1.0 en `ClientTubeTxBias` (lado TX) o `ClientTubeRxBias` (lado RX).

## Control de envolvente

El control Envelope modula dinámicamente la unidad del tubo según el nivel de la señal. Cuando se ajusta a valores positivos, el tubo se calienta (más saturación) en los transitorios fuertes. Cuando se ajusta a valores negativos, el tubo reduce la saturación en los picos, comprimiendo los armónicos.

| Control           | Valor predeterminado | Rango válido                         | Comportamiento                                                                                                                             |
|-------------------|-----------------------|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Envelope (TX)     | 0 %                   | -100 % a +100 % (interno -1.0 a +1.0) | Mapeo lineal. Los valores positivos aumentan la unidad en los transitorios; los valores negativos la reducen, comprimiendo dinámicamente los armónicos. |
| Envelope (RX)     | 0 %                   | -100 % a +100 % (interno -1.0 a +1.0) | Mismo comportamiento que en TX.                                                                                                            |

Cuando Envelope se ajusta a cualquier valor distinto de cero, los controles Attack y Release determinan la rapidez con la que el seguidor de envolvente responde a los cambios en el nivel de la señal:

| Control | Valor predeterminado | Rango válido          | Comportamiento                                                                                          |
|---------|-----------------------|-----------------------|---------------------------------------------------------------------------------------------------------|
| Attack  | 5.00 ms               | 0.1 a 30.0 ms         | Mapeo exponencial (0.1 * 300^n). Define la rapidez con la que el seguidor de envolvente responde a niveles crecientes. |
| Release | 35.00 ms              | 10.0 a 500.0 ms       | Mapeo exponencial (10 * 50^n). Define la rapidez con la que el seguidor de envolvente se recupera después de que los niveles bajan. |

## RN2 (solo TX)

La activación de RN2 habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena de DSP en el lado TX. Esta activación está oculta en el modo RX.

| Control | Valor predeterminado | Comportamiento                                                                                                                                                                                                                         |
|---------|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RN2     | desmarcado            | Activación solo en TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena de DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. Se encuentra en el panel flotante StripTubePanel debajo del medidor de nivel de salida, solo en el lado TX. Modos de voz únicamente: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. El ajuste se persiste a través de AudioEngine. |

## Edición inline de valores

Las vistas compactas de uno y tres controles, así como todos los editores basados en controles, ahora admiten la edición inline de valores.

1. Haga clic en el valor numérico que se muestra debajo de cualquier control. Aparece un campo de entrada de texto que reemplaza la etiqueta del valor.
2. Escriba directamente el valor deseado. Puede incluir unidades (p. ej., "5.00 ms", "-6 dB", "12.5") o solo el número.
3. Presione Enter para confirmar el valor. El control se mueve inmediatamente a la nueva configuración.
4. El campo acepta automáticamente formatos numéricos adaptados a la configuración regional (separador decimal de coma en las configuraciones regionales donde es estándar).
5. Si escribe un valor no válido, el control vuelve a su configuración anterior.

**Nota:** El editor inline está disponible en todas las instancias de `ClientCompKnob` de la aplicación: Drive, Tone, Bias, Output, Dry/Wet, Envelope, Attack, Release y cualquier otro control basado en un control que muestre su valor numérico.

## Consejos

- Bias interactúa con el carácter del tubo seleccionado. Pruebe cada uno de los modelos A, B y C para escuchar cómo el mismo valor de Bias produce diferentes resultados armónicos con diferentes modelos.
- El control Bias también está presente en el mosaico del applet acoplado (la fila compacta de cinco controles debajo de la curva de transferencia), por lo que puede realizar ajustes rápidos sin abrir el editor completo.
- Los cambios realizados en el mosaico acoplado y en el editor flotante se mantienen sincronizados; un temporizador de 30 Hz mantiene ambas vistas actualizadas.
- Para introducir valores de Bias con el editor inline, haga clic en la pantalla de porcentaje (p. ej., "0 %") debajo del control y escriba un número entre 0 y 100.
- Envelope sigue la señal y requiere ajustes de Attack/Release distintos de cero para funcionar. Si Envelope está ajustado pero Attack y Release están en sus valores predeterminados, intente ajustarlos para obtener la respuesta dinámica deseada.

## Atenuación por bypass

Cuando la etapa Tube está desactivada, todo el mosaico del applet acoplado se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve a la opacidad total tan pronto como se vuelve a habilitar la etapa.

## Solución de problemas

- **El control Bias no tiene efecto audible** — Es posible que Drive esté en o cerca de 0.00 dB. Bias solo desplaza el punto de operación de manera significativa cuando la curva ya está curvada. Aumente Drive primero.
- **El nivel cambia cuando se ajusta Bias** — Esto es esperado. La asimetría introducida por Bias puede aumentar o disminuir la salida aparente. Ajuste el control Output para compensar.
- **El mosaico acoplado aparece atenuado** — La etapa Tube está desactivada. Vuelva a habilitarla en el lado TX o RX. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).
- **El editor inline no acepta el valor escrito** — Asegúrese de estar escribiendo un número simple o un número con punto decimal opcional y signo. Las comas solo se permiten en configuraciones regionales donde sirven como separadores decimales.
- **Envelope no tiene efecto** — Verifique que Envelope esté ajustado a un valor distinto de cero. También verifique que Attack y Release no estén en valores extremos que impidan que el seguidor de envolvente responda a la señal.
- **La activación de RN2 no es visible** — La activación de RN2 solo aparece en modo TX y en modos de voz (no en modos digitales). Cambie a un modo de voz o verifique que esté en el lado TX.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Select a tube character (Model A, B, or C) to change harmonic flavour](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
- [Use the Dry/Wet blend to control saturation mix](use-the-dry-wet-blend-to-control-saturation-mix.md)
