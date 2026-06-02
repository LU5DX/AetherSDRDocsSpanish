# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación de válvula del lado del cliente que se ejecuta en su computadora, independiente de la radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma al audio transmitido antes de que llegue a la radio, y **Aetherial Dynamic Tube** da forma al audio recibido en el camino hacia sus altavoces o auriculares. Ambas usan el mismo modelo de válvula con barrido de polarización y los mismos controles; sus configuraciones se almacenan de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores de Tube están ocultos hasta que la etapa Tube se habilita mediante el widget CHAIN en el lado correspondiente.
- No se requiere conexión a la radio para configurar los controles de la válvula.

## Cómo funciona

Cada instancia procesa su señal a través de un modelo de curva de transferencia de válvula. La curva se dobla según Drive, Bias y el modelo de carácter de válvula seleccionado (A, B o C). Un indicador de entrada en vivo recorre la curva en tiempo real, mostrando qué parte del régimen de saturación está activa en el nivel de señal actual.

Puede abrir el editor completo para cualquier lado haciendo doble clic en la etapa TUBE en el widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico del subcontenedor acoplado muestra un conjunto compacto de perillas y la curva de transferencia sin abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su extremo derecho, que muestra el nivel pico posterior a la saturación. El medidor no es visible en el mosaico acoplado.

Cuando una etapa de válvula está desactivada (bypass) mediante el widget CHAIN, todo el mosaico acoplado se renderiza con opacidad reducida (aproximadamente el 55 % de lo normal). Esto coincide con el efecto de atenuación que usa la curva EQ cuando está desactivada y proporciona una indicación clara de un vistazo de que la etapa está inactiva.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede flotar, desacoplar u ocultar el mosaico.

## Edición de valor en línea

En v26.5.2.1, todas las perillas del applet de válvula (y todos los demás applets de AetherSDR que usan perillas) admiten la **edición de valor en línea**. Esto facilita escribir un número exacto en lugar de girar una perilla a ojo.

Para usar la edición en línea:

1. **Haga clic** en la pantalla de valor de cualquier perilla (la posición donde normalmente aparece la etiqueta numérica). La etiqueta cambia a una pequeña entrada de texto con un borde cian.
2. **Escriba** el valor deseado, usando cualquier formato numérico que entienda su configuración regional — por ejemplo, `12.5` o `12,5` (coma como separador decimal). También puede escribir solo el número sin la unidad (p. ej., `15` en lugar de `15.00 ms`). Una cadena de unidad final como `dB` o `ms` se ignora.
3. **Presione Enter** para confirmar el valor. La perilla se actualiza al valor válido más cercano dentro de su rango.
4. **Haga clic en cualquier otro lugar** o **presione Tab** para confirmar el valor y cerrar el editor. Si hace clic fuera del editor, el valor también se aplica (confirmar al perder el foco).

Para cancelar sin cambiar el valor, presione **Escape**. El editor vuelve al valor almacenado previamente.

Mientras el editor en línea está activo, los eventos de la rueda del ratón siguen funcionando, por lo que puede ajustar finamente desplazándose después de escribir un valor aproximado.

## Qué hace cada control

La siguiente tabla se aplica tanto a las instancias TX como RX. Cuando las claves de configuración difieren según el lado, se muestran ambas. Los controles marcados como **Solo editor** están disponibles en el editor flotante pero no en el mosaico acoplado.

| Control | Descripción del comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Curva de transferencia | ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia de válvula configurada actualmente con un indicador en vivo en la entrada. | — | — | — |
| Drive | Mapeo lineal. Empuja más señal hacia la etapa de válvula. | 0.00 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb` |
| Tone | Mapeo lineal. Los valores negativos oscurecen, los positivos aclaran la señal saturada. | 0.00 | -1.0 a 1.0 | `ClientTubeTxTone` / `ClientTubeRxTone` |
| A | Selecciona el Modelo A de carácter de válvula. Exclusivo con B y C. Ámbar cuando está marcado. | marcado | — | `ClientTubeTxModel` / `ClientTubeRxModel` |
| B | Selecciona el Modelo B de carácter de válvula. Exclusivo con A y C. Ámbar cuando está marcado. | desmarcado | — | `ClientTubeTxModel` / `ClientTubeRxModel` |
| C | Selecciona el Modelo C de carácter de válvula. Exclusivo con A y B. Ámbar cuando está marcado. | desmarcado | — | `ClientTubeTxModel` / `ClientTubeRxModel` |
| Bias | Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla armónica. La etiqueta se muestra como porcentaje. | 0 % | 0.0 a 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxBias` / `ClientTubeRxBias` |
| Output | Mapeo lineal. Ganancia de maquillaje/recorte posterior a la válvula. Etiqueta 'X.XX dB'. | 0.00 dB | -24.0 a 12.0 dB | `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb` |
| Dry/Wet | Mapeo lineal. Mezcla seca/húmeda (100 % = señal completamente saturada). La etiqueta se muestra como porcentaje. | 100 % | 0.0 a 1.0 (mostrado como 0 – 100 %) | `ClientTubeTxDryWet` / `ClientTubeRxDryWet` |
| Envelope | Mapeo lineal (-1.0 a +1.0). Los valores positivos aumentan el drive en los transitorios; los valores negativos lo reducen, comprimiendo los armónicos dinámicamente. La etiqueta se muestra como porcentaje con signo. | 0 % | -1.0 a 1.0 (mostrado como porcentaje con signo) | `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope` |
| Attack | Mapeo exponencial (0.1 * 300^n). Define la rapidez con que el seguidor de envolvente responde a niveles crecientes cuando Envelope ≠ 0. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` |
| Release | Mapeo exponencial (10 * 50^n). Define la rapidez con que el seguidor de envolvente se recupera después de que los niveles bajan cuando Envelope ≠ 0. Etiqueta 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` |
| RN2 | Alternancia solo TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al gate/compresor/saturador. Ubicado en el panel StripTubePanel flotante debajo del medidor de nivel de salida, solo lado TX. Solo modos de voz — los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se persiste a través de AudioEngine. | desmarcado | — | — |

## Medidor de nivel de salida (solo editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna del extremo derecho. Muestra el nivel pico posterior a la saturación usando balística de ataque rápido / liberación lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico del applet acoplado.

La desactivación (bypass) de cada instancia se controla desde el widget CHAIN, no desde el interior del mosaico de válvula. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).

## Apariencia de las perillas y soporte de temas

En v26.6.1, todas las perillas en el applet de válvula (y en todo AetherSDR) siguen el tema de color. Su apariencia se obtiene de cinco claves de color de tema dedicadas:

| Componente de la perilla | Clave del tema | Ejemplo de efecto |
|---|---|---|
| Anillo de fondo | `color.knob.background` | El arco no iluminado detrás del arco de la perilla |
| Arco de primer plano | `color.knob.foreground` | El arco que muestra el valor actual |
| Mango/indicador | `color.knob.handle` | La línea que apunta al valor actual |
| Texto del valor | `color.text.primary` | El valor numérico dibujado debajo de la perilla |
| Texto de la etiqueta | `color.text.secondary` | El nombre del control dibujado encima de la perilla |

El widget de la curva de transferencia también sigue el tema:

| Elemento de la curva | Clave del tema | Ejemplo de efecto |
|---|---|---|
| Fondo | `color.background.0` | El área de relleno del gráfico |
| Marco/cuadrícula | `color.background.1` | El borde y las líneas de la cuadrícula |
| Líneas de los ejes | `color.background.1` | Líneas de los ejes horizontal y vertical |
| Línea de la curva | `color.accent.dim` | La curva de transferencia de la válvula |
| Resplandor del indicador | `color.accent.warning` | El resplandor alrededor del indicador de entrada en vivo |
| Núcleo del indicador | `color.text.primary` | El punto central del indicador de entrada en vivo |

El contenedor del widget en sí está etiquetado con el contenedor de tema `applet/tube`, lo que permite anulaciones de color por applet para las perillas y la curva de la válvula.

## Consejos

- Comience con Drive en 0.00 dB y auméntelo lentamente hasta que la curva de transferencia comience a doblarse visiblemente. El indicador de entrada en vivo muestra si los picos están alcanzando la región saturada.
- Use Output para alinear el nivel procesado con el nivel seco después de agregar Drive, de modo que las comparaciones tengan niveles igualados. Observe el medidor OUT en el editor para verificar los niveles pico posteriores a la saturación.
- Configure Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca, lo que puede agregar cuerpo sin el carácter completo de la saturación total.
- Bias al 0 % produce una curva simétrica. Aumentarlo introduce asimetría, desplazando el contenido armónico hacia armónicos de orden par.
- Use los Modelos A, B o C para cambiar el carácter fundamental de la curva de la válvula antes de ajustar Drive y Bias.
- Establezca Envelope en un valor positivo para que la saturación siga a los transitorios: los picos fuertes accionan la válvula más automáticamente. Use Attack y Release para controlar la rapidez con que el seguidor reacciona y se recupera.
- Cuando una etapa de válvula está desactivada (bypass), el mosaico acoplado se atenúa visiblemente. Si nota que el mosaico parece desvaído, verifique que la etapa esté habilitada en el widget CHAIN antes de ajustar los controles.
- Use la edición de valor en línea (haga clic en la etiqueta de la perilla) para ingresar números exactos rápidamente en lugar de girar una perilla. Presione Escape para cancelar la edición.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
