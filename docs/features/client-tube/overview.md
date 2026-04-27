# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación de válvula en el lado del cliente que se ejecuta en su computadora, independientemente del radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** modela el audio que usted transmite antes de que llegue al radio, y **Aetherial Dynamic Tube** modela el audio recibido en su camino hacia los altavoces o auriculares. Ambas utilizan el mismo modelo de válvula con barrido de bias y los mismos cinco controles; sus ajustes se almacenan de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores Tube permanecen ocultos hasta que la etapa Tube se habilita mediante el widget CHAIN del lado correspondiente.
- No se requiere conexión con el radio para configurar los controles de la válvula.

## Cómo funciona

Cada instancia procesa la señal a través de un modelo de curva de transferencia de válvula. La curva se curva según los valores de Drive, Bias y el modelo seleccionado. Una bola de entrada en tiempo real recorre la curva, mostrando en qué parte del régimen de saturación se encuentra el nivel de señal actual.

Puede abrir el editor completo para cualquiera de los lados haciendo doble clic en la etapa TUBE dentro del widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. Los cinco mandos también están disponibles directamente en el panel subcontenedor acoplado sin necesidad de abrir el editor. Los cambios realizados en el editor flotante y en el panel acoplado se sincronizan automáticamente.

Para abrir el menú contextual del panel acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede hacer flotar, extraer u ocultar el panel.

## Qué hace cada control

La tabla a continuación aplica tanto para las instancias TX como RX. Cuando las claves de ajuste difieren según el lado, se muestran ambas.

| Control | Valor predeterminado | Rango válido | Clave de ajuste TX | Clave de ajuste RX | Descripción |
|---|---|---|---|---|---|
| Transfer curve | — | — | — | — | Muestra la curva de transferencia de válvula actual. La bola de entrada en tiempo real se desplaza por la curva según el nivel de entrada actual, mostrando el régimen de saturación activo. Indicador de solo lectura. |
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Introduce más señal en la etapa de válvula. Valores más altos producen mayor saturación y curvatura de la curva. Se muestra como `X.X dB`. |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Ajusta el carácter tonal de la señal saturada. Valores negativos oscurecen el sonido; valores positivos lo aclaran. Se muestra como `X.XX`. |
| Bias | 0 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxBiasAmount` | `ClientTubeRxBiasAmount` | Desplaza el punto de operación en la curva de transferencia, modificando la mezcla de armónicos pares e impares. Se muestra como porcentaje. |
| Output | 0.0 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputGainDb` | `ClientTubeRxOutputGainDb` | Ganancia de compensación o recorte posterior a la válvula. Úsela para compensar los cambios de nivel introducidos por la saturación. Se muestra como `X.X dB`. |
| Mix | 100 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Mezcla dry/wet entre la señal sin procesar y la señal saturada. El 100 % pasa únicamente la señal saturada; el 0 % pasa únicamente la señal seca. |

El bypass de cada instancia se controla desde el widget CHAIN, no desde el propio panel de la válvula. Consulte [Bypass de la válvula desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente hasta que la curva de transferencia empiece a curvarse visiblemente. La bola de entrada en tiempo real indica si los picos están alcanzando la región de saturación.
- Use Output para devolver el nivel procesado al nivel de la señal seca después de aumentar el Drive, de modo que las comparaciones estén ajustadas en nivel.
- Ajuste Mix por debajo del 100 % para mezclar en paralelo con la señal seca, lo que puede añadir cuerpo sin el carácter completo de la saturación total.
- Bias en 0 % produce una curva simétrica. Al aumentarlo se introduce asimetría, desplazando el contenido armónico hacia los armónicos de orden par.

## Relacionados

- [Ajuste Drive hasta que la curva empiece a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplace Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Bypass de la válvula desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
