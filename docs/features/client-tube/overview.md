# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación de válvulas en el lado del cliente que se ejecuta en su computadora, de forma independiente al radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma al audio transmitido antes de que llegue al radio, y **Aetherial Dynamic Tube** da forma al audio recibido en el camino hacia sus altavoces o auriculares. Ambas utilizan el mismo modelo de válvula con barrido de polarización y los mismos controles; sus configuraciones se almacenan de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores Tube permanecen ocultos hasta que la etapa Tube se habilita mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión al radio para configurar los controles del Tube.

## Cómo funciona

Cada instancia hace pasar la señal a través de un modelo de curva de transferencia de válvula. La curva se dobla según Drive, Bias y el modelo de carácter de válvula seleccionado (A, B o C). Una esfera de entrada en tiempo real recorre la curva, mostrando qué parte del régimen de saturación está activa en el nivel de señal actual.

Puede abrir el editor completo de cualquiera de los lados haciendo doble clic en la etapa TUBE en el widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico de subcontenedor acoplado muestra un conjunto compacto de perillas y la curva de transferencia sin necesidad de abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su columna extrema derecha, que muestra el nivel de pico posterior a la saturación. El medidor no es visible en el mosaico acoplado.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede hacer flotar, extraer u ocultar el mosaico.

## Qué hace cada control

La tabla siguiente aplica tanto a las instancias TX como RX. Donde las claves de configuración difieren según el lado, se muestran ambas. Los controles marcados como **Editor only** están disponibles en el editor flotante, pero no en el mosaico acoplado.

| Control | Valor predeterminado | Rango válido | Clave de configuración TX | Clave de configuración RX | Descripción |
|---|---|---|---|---|---|
| Transfer curve | — | — | — | — | Muestra la curva de transferencia actual de la válvula. La esfera de entrada en tiempo real se desplaza a lo largo de la curva según el nivel de entrada actual, indicando el régimen de saturación activo. Indicador de solo lectura. Disponible tanto en el mosaico acoplado como en el editor. |
| Drive | 0.00 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Introduce más señal en la etapa de válvula. Valores más altos producen mayor saturación y curvatura. Se muestra como `X.XX dB`. |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Ajusta el carácter tonal de la señal saturada. Valores negativos oscurecen el tono; valores positivos lo aclaran. Se muestra como `X.XX`. |
| A | activado (predeterminado) | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula A. Exclusivo con B y C. Se ilumina en ámbar cuando está activo. **Editor only.** |
| B | desactivado | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula B. Exclusivo con A y C. Se ilumina en ámbar cuando está activo. **Editor only.** |
| C | desactivado | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula C. Exclusivo con A y B. Se ilumina en ámbar cuando está activo. **Editor only.** |
| Bias | 0 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxBias` | `ClientTubeRxBias` | Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla de armónicos pares e impares. Se muestra como porcentaje. |
| Output | 0.00 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` | `ClientTubeRxOutputDb` | Ganancia de compensación o ajuste posterior a la válvula. Úsela para compensar los cambios de nivel introducidos por la saturación. Se muestra como `X.XX dB`. |
| Dry/Wet | 100 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Mezcla dry/wet entre la señal sin procesar y la señal saturada. El 100 % pasa únicamente la señal saturada; el 0 % pasa únicamente la señal seca. |
| Envelope | 0 % | −1.0 – 1.0 (mostrado como porcentaje con signo) | `ClientTubeTxEnvelope` | `ClientTubeRxEnvelope` | Profundidad del seguidor de envolvente. Valores positivos aumentan el Drive en las transitorias, de modo que la válvula trabaja más fuerte en los picos intensos; valores negativos reducen el Drive de forma dinámica, comprimiendo la salida armónica. No tiene efecto cuando está ajustado a 0 %. **Editor only.** |
| Attack | 5.00 ms | 0.1 – 30.0 ms | `ClientTubeTxAttackMs` | `ClientTubeRxAttackMs` | Establece con qué rapidez responde el seguidor de envolvente al aumento del nivel de señal. Solo está activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 10 ms y como `X.X ms` por encima. **Editor only.** |
| Release | 35.00 ms | 10.0 – 500.0 ms | `ClientTubeTxReleaseMs` | `ClientTubeRxReleaseMs` | Establece con qué rapidez se recupera el seguidor de envolvente tras la caída del nivel de señal. Solo está activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 100 ms y como `X.X ms` por encima. **Editor only.** |

## Medidor de nivel de salida (solo en el editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna extrema derecha. Muestra el nivel de pico posterior a la saturación con una dinámica de ataque rápido y caída lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico de applet acoplado.

El bypass de cada instancia se controla desde el widget CHAIN, no desde el mosaico del Tube en sí. Consulte [Desactivar el Tube desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md).

## Consejos

- Comience con Drive en 0.00 dB y auméntelo lentamente hasta que la curva de transferencia comience a doblarse de forma visible. La esfera de entrada en tiempo real indica si los picos están alcanzando la región de saturación.
- Use Output para devolver el nivel procesado al nivel de la señal seca después de aumentar Drive, de modo que las comparaciones estén igualadas en nivel. Observe el medidor OUT en el editor para verificar los niveles de pico posteriores a la saturación.
- Ajuste Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca; esto puede añadir cuerpo sin el carácter completo de la saturación total.
- Bias en 0 % produce una curva simétrica. Al aumentarlo se introduce asimetría, desplazando el contenido armónico hacia armónicos de orden par.
- Use el modelo A, B o C para cambiar el carácter fundamental de la curva de válvula antes de ajustar Drive y Bias.
- Ajuste Envelope a un valor positivo para que la saturación siga las transitorias: los picos intensos impulsan la válvula con más fuerza de forma automática. Use Attack y Release para controlar con qué rapidez reacciona y se recupera el seguidor.

## Relacionados

- [Ajustar Drive hasta que la curva comience a doblarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Desplazar Bias para ajustar el balance entre armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla de saturación en paralelo con Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Desactivar el Tube desde cualquiera de las cadenas](bypass-the-tube-from-either-chain.md)
