# Resumen de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación tipo válvula que se ejecuta en su computadora, independientemente de la radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma a su audio transmitido antes de que llegue a la radio, y **Aetherial Dynamic Tube** da forma al audio recibido en su camino hacia los altavoces o auriculares. Ambas usan el mismo modelo de válvula con barrido de polarización y los mismos controles; su configuración se almacena de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores de Tube están ocultos hasta que la etapa Tube se habilite a través del widget CHAIN en el lado correspondiente.
- No se requiere conexión a la radio para configurar los controles de Tube.

## Cómo funciona

Cada instancia procesa su señal a través de un modelo de curva de transferencia de válvula. La curva se deforma según Drive, Bias y el modelo de carácter de válvula seleccionado (A, B o C). Una bola de entrada en vivo se desplaza sobre la curva en tiempo real, mostrando qué parte del régimen de saturación está activa en el nivel de señal actual.

Puede abrir el editor completo para cualquier lado haciendo doble clic en la etapa TUBE en el widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico del subcontenedor acoplado muestra un conjunto compacto de perillas y la curva de transferencia sin abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su extremo derecho, que muestra el nivel pico posterior a la saturación. El medidor no está visible en el mosaico acoplado.

Cuando una etapa Tube se omite a través del widget CHAIN, todo el mosaico acoplado se renderiza con opacidad reducida (aproximadamente el 55 % de lo normal). Esto coincide con el efecto de atenuación utilizado por la curva EQ cuando se omite y proporciona una indicación clara de un vistazo de que la etapa está inactiva.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede flotar, desacoplar u ocultar el mosaico.

## Qué hace cada control

La siguiente tabla aplica tanto para las instancias TX como RX. Cuando las claves de configuración difieren según el lado, se muestran ambas. Los controles marcados como **Solo editor** están disponibles en el editor flotante, pero no en el mosaico acoplado.

| Control | Valor predeterminado | Rango válido | Clave de configuración TX | Clave de configuración RX | Descripción |
|---|---|---|---|---|---|
| Curva de transferencia | — | — | — | — | Muestra la curva de transferencia de válvula actual. La bola de entrada en vivo se mueve a lo largo de la curva al nivel de entrada actual, mostrando el régimen de saturación activo. Indicador de solo lectura. Disponible tanto en el mosaico acoplado como en el editor. |
| Drive | 0.00 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Introduce más señal en la etapa de válvula. Los valores más altos producen más saturación y curvatura. Se muestra como `X.XX dB`. |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Ajusta el carácter tonal de la señal saturada. Los valores negativos oscurecen; los positivos brillan. Se muestra como `X.XX`. |
| A | marcado (predeterminado) | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula A. Exclusivo con B y C. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| B | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula B. Exclusivo con A y C. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| C | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el modelo de carácter de válvula C. Exclusivo con A y B. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| Bias | 0 % | 0.0 – 1.0 (se muestra como 0 – 100 %) | `ClientTubeTxBias` | `ClientTubeRxBias` | Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla de armónicos pares e impares. Se muestra como un porcentaje. |
| Output | 0.00 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` | `ClientTubeRxOutputDb` | Ganancia de compensación o maquillaje posterior a la válvula. Úselo para compensar los cambios de nivel introducidos por la saturación. Se muestra como `X.XX dB`. |
| Dry/Wet | 100 % | 0.0 – 1.0 (se muestra como 0 – 100 %) | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Mezcla seca/húmeda entre la señal sin procesar y la saturada. 100 % pasa solo la señal saturada; 0 % pasa solo la señal seca. |
| Envelope | 0 % | −1.0 – 1.0 (se muestra como porcentaje con signo) | `ClientTubeTxEnvelope` | `ClientTubeRxEnvelope` | Profundidad del seguidor de envolvente. Los valores positivos aumentan la excitación en los transitorios para que la válvula se caliente más en los picos fuertes; los valores negativos reducen la excitación dinámicamente, comprimiendo la salida armónica. No tiene efecto cuando se establece en 0 %. **Solo editor.** |
| Attack | 5.00 ms | 0.1 – 30.0 ms | `ClientTubeTxAttackMs` | `ClientTubeRxAttackMs` | Establece la rapidez con la que el seguidor de envolvente responde al aumento de los niveles de señal. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 10 ms, `X.X ms` por encima. **Solo editor.** |
| Release | 35.00 ms | 10.0 – 500.0 ms | `ClientTubeTxReleaseMs` | `ClientTubeRxReleaseMs` | Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles de señal caen. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 100 ms, `X.X ms` por encima. **Solo editor.** |

## Medidor de nivel de salida (solo editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna del extremo derecho. Muestra el nivel pico posterior a la saturación utilizando balística de ataque rápido / liberación lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico del applet acoplado.

La omisión de cada instancia se controla desde el widget CHAIN, no desde el propio mosaico de Tube. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).

## Consejos

- Comience con Drive en 0.00 dB y súbalo lentamente hasta que la curva de transferencia comience a doblarse visiblemente. La bola de entrada en vivo muestra si los picos están alcanzando la región saturada.
- Use Output para devolver el nivel procesado a la misma línea que el nivel seco después de agregar Drive, de modo que las comparaciones tengan el nivel equiparado. Observe el medidor OUT en el editor para verificar los niveles pico posteriores a la saturación.
- Establezca Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca, lo que puede agregar cuerpo sin el carácter completo de la saturación total.
- Bias al 0 % produce una curva simétrica. Subirlo introduce asimetría, desplazando el contenido armónico hacia los armónicos de orden par.
- Use los modelos A, B o C para cambiar el carácter fundamental de la curva de válvula antes de ajustar Drive y Bias.
- Establezca Envelope en un valor positivo para que la saturación siga los transitorios: los picos fuertes excitan la válvula automáticamente. Use Attack y Release para controlar la rapidez con la que el seguidor reacciona y se recupera.
- Cuando una etapa Tube está omitida, el mosaico acoplado se atenúa visiblemente. Si nota que el mosaico aparece desvanecido, verifique que la etapa esté habilitada en el widget CHAIN antes de ajustar los controles.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
