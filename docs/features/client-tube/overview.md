# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación de válvula del lado del cliente que se ejecuta en su computadora, independientemente de la radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma al audio transmitido antes de que llegue a la radio, y **Aetherial Dynamic Tube** da forma al audio recibido en el camino hacia sus altavoces o auriculares. Ambas utilizan el mismo modelo de válvula con barrido de polarización y los mismos controles; sus ajustes se almacenan de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores de Tube están ocultos hasta que la etapa Tube se habilite mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión a la radio para configurar los controles de la válvula.

## Cómo funciona

Cada instancia procesa su señal a través de un modelo de curva de transferencia de válvula. La curva se deforma según el Drive, el Bias y el modelo de carácter de válvula seleccionado (A, B o C). Una bola de entrada en vivo se desplaza sobre la curva en tiempo real, mostrando qué parte del régimen de saturación está activa en el nivel de señal actual.

Puede abrir el editor completo para cualquier lado haciendo doble clic en la etapa TUBE en el widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico del subcontenedor acoplado muestra un conjunto compacto de perillas y la curva de transferencia sin abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su extremo derecho, que muestra el nivel pico posterior a la saturación. El medidor no es visible en el mosaico acoplado.

Cuando una etapa de válvula está desactivada mediante el widget CHAIN, todo el mosaico acoplado se renderiza con opacidad reducida (aproximadamente el 55% de lo normal). Esto coincide con el efecto de atenuación utilizado por la curva EQ cuando está desactivada y proporciona una indicación clara de un vistazo de que la etapa está inactiva.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede flotar, desacoplar u ocultar el mosaico.

## Edición de valores en línea

En la versión v26.5.2.1, todas las perillas del applet de válvula (y de todos los demás applets de AetherSDR que usan perillas) admiten la **edición de valores en línea**. Esto facilita escribir un número exacto en lugar de girar una perilla a ojo.

Para usar la edición en línea:

1. **Haga clic** en la visualización del valor de cualquier perilla (la posición donde aparece la etiqueta numérica normalmente). La etiqueta cambia a una pequeña entrada de texto con un borde cian.
2. **Escriba** el valor deseado, utilizando cualquier formato de número que entienda su configuración regional — por ejemplo, `12.5` o `12,5` (coma como separador decimal). También puede escribir solo el número sin la unidad (p. ej., `15` en lugar de `15.00 ms`). Una cadena de unidad final como `dB` o `ms` se ignora.
3. **Presione Enter** para confirmar el valor. La perilla se actualiza al ajuste válido más cercano dentro de su rango.
4. **Haga clic en cualquier otro lugar** o **presione Tab** para confirmar el valor y cerrar el editor. Si hace clic fuera del editor, el valor también se aplica (confirmar al perder el foco).

Para cancelar sin cambiar el valor, presione **Escape**. El editor revierte al valor almacenado anteriormente.

Mientras el editor en línea está activo, los eventos de la rueda del ratón aún funcionan, por lo que puede ajustar finamente desplazándose después de escribir un valor aproximado.

## Qué hace cada control

La siguiente tabla se aplica tanto a las instancias TX como RX. Cuando las claves de ajuste difieren según el lado, se muestran ambas. Los controles marcados como **Solo editor** están disponibles en el editor flotante pero no en el mosaico acoplado.

| Control | Valor predeterminado | Rango válido | Clave de ajuste TX | Clave de ajuste RX | Descripción |
|---|---|---|---|---|---|
| Curva de transferencia | — | — | — | — | Muestra la curva de transferencia actual de la válvula. La bola de entrada en vivo se mueve a lo largo de la curva en el nivel de entrada actual, mostrando el régimen de saturación activo. Indicador de solo lectura. Disponible tanto en el mosaico acoplado como en el editor. |
| Drive | 0.00 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | `ClientTubeRxDriveDb` | Introduce más señal en la etapa de válvula. Los valores más altos producen más saturación y deformación de la curva. Se muestra como `X.XX dB`. |
| Tone | 0.00 | −1.0 – 1.0 | `ClientTubeTxTone` | `ClientTubeRxTone` | Ajusta el carácter tonal de la señal saturada. Los valores negativos oscurecen; los valores positivos iluminan. Se muestra como `X.XX`. |
| A | marcado (predeterminado) | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el Modelo A de carácter de válvula. Exclusivo con B y C. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| B | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el Modelo B de carácter de válvula. Exclusivo con A y C. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| C | sin marcar | — | `ClientTubeTxModel` | `ClientTubeRxModel` | Selecciona el Modelo C de carácter de válvula. Exclusivo con A y B. Se ilumina en ámbar cuando está activo. **Solo editor.** |
| Bias | 0 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxBias` | `ClientTubeRxBias` | Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla de armónicos pares e impares. Se muestra como un porcentaje. |
| Output | 0.00 dB | −24.0 – 12.0 dB | `ClientTubeTxOutputDb` | `ClientTubeRxOutputDb` | Ganancia de compensación o recorte posterior a la válvula. Úselo para compensar los cambios de nivel introducidos por la saturación. Se muestra como `X.XX dB`. |
| Dry/Wet | 100 % | 0.0 – 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxDryWet` | `ClientTubeRxDryWet` | Mezcla seco/húmedo entre la señal no procesada y la saturada. 100 % pasa solo la señal saturada; 0 % pasa solo la señal seca. |
| Envelope | 0 % | −1.0 – 1.0 (mostrado como porcentaje con signo) | `ClientTubeTxEnvelope` | `ClientTubeRxEnvelope` | Profundidad del seguidor de envolvente. Los valores positivos aumentan el drive en los transitorios para que la válvula se caliente más en los picos fuertes; los valores negativos reducen el drive dinámicamente, comprimiendo la salida armónica. No tiene efecto cuando se establece en 0 %. **Solo editor.** |
| Attack | 5.00 ms | 0.1 – 30.0 ms | `ClientTubeTxAttackMs` | `ClientTubeRxAttackMs` | Establece la rapidez con la que el seguidor de envolvente responde a los niveles de señal crecientes. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 10 ms, `X.X ms` por encima. **Solo editor.** |
| Release | 35.00 ms | 10.0 – 500.0 ms | `ClientTubeTxReleaseMs` | `ClientTubeRxReleaseMs` | Establece la rapidez con la que el seguidor de envolvente se recupera después de que los niveles de señal bajan. Solo activo cuando Envelope ≠ 0 %. Se muestra como `X.XX ms` por debajo de 100 ms, `X.X ms` por encima. **Solo editor.** |

## Medidor de nivel de salida (solo editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna del extremo derecho. Muestra el nivel pico posterior a la saturación utilizando balística de ataque rápido / liberación lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico del applet acoplado.

La desactivación de cada instancia se controla desde el widget CHAIN, no desde el propio mosaico de Tube. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).

## Consejos

- Comience con Drive en 0.00 dB y súbalo lentamente hasta que la curva de transferencia comience a deformarse visiblemente. La bola de entrada en vivo muestra si los picos están alcanzando la región saturada.
- Use Output para alinear el nivel procesado con el nivel seco después de agregar Drive, de modo que las comparaciones tengan el nivel igualado. Observe el medidor OUT en el editor para verificar los niveles pico posteriores a la saturación.
- Configure Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca, lo que puede agregar cuerpo sin el carácter completo de la saturación total.
- Bias al 0 % produce una curva simétrica. Elevarlo introduce asimetría, desplazando el contenido armónico hacia los armónicos de orden par.
- Use el Modelo A, B o C para cambiar el carácter fundamental de la curva de la válvula antes de ajustar Drive y Bias.
- Configure Envelope en un valor positivo para que la saturación siga los transitorios; los picos fuertes activan la válvula de forma más intensa automáticamente. Use Attack y Release para controlar la rapidez con la que el seguidor reacciona y se recupera.
- Cuando una etapa de válvula está desactivada, el mosaico acoplado se atenúa visiblemente. Si nota que el mosaico aparece desteñido, verifique que la etapa esté habilitada en el widget CHAIN antes de ajustar los controles.
- Use la edición de valores en línea (haga clic en la etiqueta de la perilla) para ingresar números exactos rápidamente en lugar de girar una perilla. Presione Escape para cancelar la edición.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
