# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación de válvulas del lado del cliente que se ejecuta en su computadora, independientemente del radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma al audio transmitido antes de que llegue al radio, y **Aetherial Dynamic Tube** da forma al audio recibido en su camino hacia los altavoces o auriculares. Ambas usan el mismo modelo de válvula con barrido de polarización y los mismos controles; sus ajustes se almacenan de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores de la válvula permanecen ocultos hasta que la etapa de válvula se habilita mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión al radio para configurar los controles de la válvula.

## Cómo funciona

Cada instancia hace pasar la señal por un modelo de curva de transferencia de válvula. La curva se dobla según los valores de Drive, Bias y el modelo de carácter de válvula seleccionado (A, B o C). Una bola de entrada en tiempo real recorre la curva, mostrando en qué parte del régimen de saturación se encuentra el nivel de señal actual.

Para abrir el editor completo de cualquiera de los dos lados, haga doble clic en la etapa TUBE dentro del widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico de subcontenedor acoplado muestra un conjunto compacto de mandos y la curva de transferencia sin necesidad de abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su columna derecha, que muestra el nivel de pico posterior a la saturación. El medidor no es visible en el mosaico acoplado.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede hacer flotar, extraer u ocultar el mosaico.

## Qué hace cada control

La tabla siguiente aplica tanto a la instancia TX como a la RX. Cuando las claves de ajuste difieren según el lado, se muestran ambas. Los controles marcados como **Solo en el editor** están disponibles en el editor flotante, pero no en el mosaico acoplado.

| Control | Valor predeterminado | Rango válido | Clave de ajuste TX | Clave de ajuste RX | Descripción |
|---|---|---|---|---|---|
| Curva de transferencia | — | — | — | — | Muestra la curva de transferencia de válvula actual. La bola de entrada en tiempo real se desplaza a lo largo de la curva según el nivel de entrada actual, indicando el régimen de saturación activo. Indicador de solo lectura. Disponible tanto en el mosaico acoplado como en el editor. |
| Drive | 0.00 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Envía más señal hacia la etapa de válvula. Los valores más altos producen mayor saturación y curvatura. Se muestra como `X.XX dB`. |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Ajusta el carácter tonal de la señal saturada. Los valores negativos oscurecen el tono; los positivos lo aclaran. Se muestra como `X.XX`. |
| A | marcado (predeterminado) | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula A. Exclusivo con B y C. Se ilumina en ámbar cuando está activo. **Solo en el editor.** |
| B | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula B. Exclusivo con A y C. Se ilumina en ámbar cuando está activo. **Solo en el editor.** |
| C | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula C. Exclusivo con A y B. Se ilumina en ámbar cuando está activo. **Solo en el editor.** |
| Bias | 0 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxBias` | `ClientTubeRxBias` | Desplaza el punto de operación en la curva de transferencia, modificando la mezcla de armónicos pares e impares. Se muestra como porcentaje. |
| Output | 0.00 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` | `ClientTubeRxOutputDb` | Ganancia de compensación o recorte posterior a la válvula. Úsela para compensar los cambios de nivel introducidos por la saturación. Se muestra como `X.XX dB`. |
| Dry/Wet | 100 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Mezcla dry/wet entre la señal sin procesar y la saturada. 100 % pasa únicamente la señal saturada; 0 % pasa únicamente la señal seca. |
| Envelope | 0 % | −1.0 – 1.0 (mostrado como porcentaje con signo) | `ClientTubeTxEnvelope` | `ClientTubeRxEnvelope` | Profundidad del seguidor de envolvente. Los valores positivos aumentan el Drive en los transitorios, de modo que la válvula trabaja con más intensidad en los picos fuertes; los valores negativos reducen el Drive de forma dinámica, comprimiendo la salida de armónicos. No tiene efecto cuando se ajusta a 0 %. **Solo en el editor.** |
| Attack | 5.00 ms | 0.1 – 30.0 ms | `ClientTubeTxAttackMs` | `ClientTubeRxAttackMs` | Establece la rapidez con que el seguidor de envolvente responde al aumento del nivel de señal. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 10 ms, y como `X.X ms` por encima. **Solo en el editor.** |
| Release | 35.00 ms | 10.0 – 500.0 ms | `ClientTubeTxReleaseMs` | `ClientTubeRxReleaseMs` | Establece la rapidez con que el seguidor de envolvente se recupera tras la caída del nivel de señal. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 100 ms, y como `X.X ms` por encima. **Solo en el editor.** |

## Medidor de nivel de salida (solo en el editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna derecha. Muestra el nivel de pico posterior a la saturación con balística de ataque rápido y recuperación lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Verde lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico de applet acoplado.

El bypass de cada instancia se controla desde el widget CHAIN, no desde el mosaico de la válvula. Consulte [Omitir la válvula desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).

## Consejos

- Comience con Drive en 0.00 dB y auméntelo lentamente hasta que la curva de transferencia comience a doblarse de forma visible. La bola de entrada en tiempo real indica si los picos están alcanzando la región saturada.
- Use Output para que el nivel procesado vuelva a coincidir con el nivel seco tras añadir Drive, de modo que las comparaciones estén niveladas. Observe el medidor OUT en el editor para verificar los niveles de pico posteriores a la saturación.
- Ajuste Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca; esto puede añadir cuerpo sin aplicar el carácter completo de la saturación total.
- Bias en 0 % produce una curva simétrica. Aumentarlo introduce asimetría, desplazando el contenido armónico hacia los armónicos de orden par.
- Use el modelo A, B o C para cambiar el carácter fundamental de la curva de válvula antes de ajustar Drive y Bias.
- Ajuste Envelope a un valor positivo para que la saturación siga los transitorios: los picos fuertes llevan la válvula a mayor intensidad de forma automática. Use Attack y Release para controlar la rapidez de reacción y recuperación del seguidor.

## Relacionados

- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o moldeado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla en paralelo de la saturación con Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Omitir la válvula desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
