# Ajustar Bias para equilibrar los armónicos

El control Bias desplaza el punto de operación en la curva de transferencia del tubo, cambiando el balance de armónicos pares e impares que produce el saturador. Úselo para afinar el carácter de la saturación después de haber configurado Drive.

## Antes de comenzar

- La etapa Tube debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md).
- Drive ya debe estar configurado con un valor suficientemente alto para que la curva de transferencia muestre una curvatura visible. Consulte [Ajustar Drive hasta que la curva empiece a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md).
- Abra el editor flotante haciendo doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX. El editor se titula "Aetherial Tube — TX" o "Aetherial Tube — RX".

## Pasos

1. Localice el control Bias en la fila central del editor, a la derecha del selector de modelo A / B / C.
2. Gire Bias desde su valor predeterminado de 0 % hacia valores más altos (hasta 100 %) para desplazar el punto de operación y aumentar la saturación asimétrica.
3. Observe la curva de transferencia: el punto de curvatura se desplaza a medida que gira el control. La bola de entrada en tiempo real sigue la nueva región de operación.
4. Detenga el ajuste cuando el balance de armónicos suene correcto para su caso de uso.
5. Si el nivel general cambia de forma notable, ajuste el control Output para compensarlo. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|---------|-------------|-----------------------|
| Bias (TX) | 0 % | 0 % a 100 % (interno 0.0 a 1.0) | `ClientTubeTxBias` |
| Bias (RX) | 0 % | 0 % a 100 % (interno 0.0 a 1.0) | `ClientTubeRxBias` |

El control Bias utiliza una asignación lineal. El valor mostrado es un porcentaje. Internamente, la configuración se almacena como un valor de 0.0 a 1.0 en `ClientTubeTxBias` (lado TX) o `ClientTubeRxBias` (lado RX).

## Consejos

- Bias interactúa con el carácter de tubo seleccionado. Pruebe cada uno de los modelos A, B y C para escuchar cómo el mismo valor de Bias produce resultados armónicos distintos con diferentes modelos.
- El control Bias también está presente en el panel applet acoplado (la fila compacta de cinco controles debajo de la curva de transferencia), de modo que puede realizar ajustes rápidos sin abrir el editor completo.
- Los cambios realizados en el panel acoplado y en el editor flotante se mantienen sincronizados; un temporizador de 30 Hz mantiene ambas vistas actualizadas.

## Solución de problemas

- **El control Bias no produce efecto audible** — Drive puede estar en 0.00 dB o cerca de ese valor. Bias solo desplaza el punto de operación de forma significativa cuando la curva ya está curvada. Aumente Drive primero.
- **El nivel cambia al ajustar Bias** — Esto es esperado. La asimetría introducida por Bias puede aumentar o reducir el nivel de salida aparente. Ajuste el control Output para compensarlo.

## Relacionados

- [Ajustar Drive hasta que la curva empiece a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Seleccionar un carácter de tubo (Modelo A, B o C) para cambiar el perfil armónico](select-a-tube-character-model-a-b-or-c-to-change-harmonic-flavour.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Monitorear el recorte de salida con el medidor de nivel en el editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
- [Omitir el tubo desde cualquier cadena](bypass-the-tube-from-either-chain.md)
