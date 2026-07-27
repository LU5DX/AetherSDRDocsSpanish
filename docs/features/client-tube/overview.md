# Descripción general de Aetherial Mic-PreAmp (TX) / Aetherial Dynamic Tube (RX)

AetherSDR incluye una etapa de saturación tipo tubo del lado del cliente que se ejecuta en su computadora, independiente de la radio. Existen dos instancias completamente separadas: **Aetherial Mic-PreAmp** da forma a su audio transmitido antes de que llegue a la radio, y **Aetherial Dynamic Tube** da forma al audio recibido en el camino hacia sus altavoces o auriculares. Ambas utilizan el mismo modelo de tubo con barrido de polarización y los mismos controles; su configuración se almacena de forma independiente.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Los subcontenedores del tubo permanecen ocultos hasta que la etapa del tubo se habilite a través del widget CHAIN en el lado correspondiente.
- No se requiere conexión a la radio para configurar los controles del tubo.

## Cómo funciona

Cada instancia procesa su señal a través de un modelo de curva de transferencia de tubo. La curva se deforma según Drive, Bias y el modelo de carácter de tubo seleccionado (A, B o C). Una bola de entrada en vivo se desplaza sobre la curva en tiempo real, mostrando qué parte del régimen de saturación está activa en el nivel de señal actual.

Puede abrir el editor completo para cualquier lado haciendo doble clic en la etapa TUBE en el widget CHAIN. El editor flotante se titula **Aetherial Tube — TX** o **Aetherial Tube — RX**. El mosaico del subcontenedor acoplado muestra un conjunto compacto de perillas y la curva de transferencia sin abrir el editor. Los cambios realizados en el editor flotante y en el mosaico acoplado se sincronizan automáticamente.

El editor flotante también incluye un medidor de nivel **OUT** en su extremo derecho, que muestra el nivel pico posterior a la saturación. El medidor no está visible en el mosaico acoplado.

Cuando una etapa de tubo se omite mediante el widget CHAIN, todo el mosaico acoplado se renderiza con opacidad reducida (aproximadamente el 55 % de lo normal). Esto coincide con el efecto de atenuación utilizado por la curva EQ cuando está omitida y proporciona una indicación clara de un vistazo de que la etapa está inactiva.

Para abrir el menú contextual del mosaico acoplado, haga clic derecho en la barra de título del subcontenedor **Aetherial Mic-PreAmp** o **Aetherial Dynamic Tube**. Desde allí puede flotar, desacoplar u ocultar el mosaico.

## Edición de valor en línea

En v26.5.2.1, todas las perillas del applet de tubo (y todos los demás applets de AetherSDR que usan perillas) admiten la **edición de valor en línea**. Esto facilita escribir un número exacto en lugar de girar una perilla a ojo.

Para usar la edición en línea:

1. **Haga clic** en la visualización del valor de cualquier perilla (la posición donde normalmente aparece la etiqueta numérica). La etiqueta cambia a una pequeña entrada de texto con un borde cian.
2. **Escriba** el valor deseado, usando cualquier formato numérico que entienda su configuración regional — por ejemplo, `12.5` o `12,5` (coma como separador decimal). También puede escribir solo el número sin la unidad (p. ej., `15` en lugar de `15.00 ms`). Una cadena de unidad al final como `dB` o `ms` se ignora.
3. **Presione Enter** para confirmar el valor. La perilla se actualiza a la configuración válida más cercana dentro de su rango.
4. **Haga clic en cualquier otro lugar** o **presione Tab** para confirmar el valor y cerrar el editor. Si hace clic fuera del editor, el valor también se aplica (confirmación al perder el foco).

Para cancelar sin cambiar el valor, presione **Escape**. El editor vuelve al valor almacenado anteriormente.

Mientras el editor en línea está activo, los eventos de la rueda del ratón aún funcionan, por lo que puede ajustar finamente desplazándose después de escribir un valor aproximado.

## Qué hace cada control

La siguiente tabla se aplica tanto a las instancias TX como RX. Cuando las claves de configuración difieren según el lado, se muestran ambas. Los controles marcados como **Solo editor** están disponibles en el editor flotante pero no en el mosaico acoplado.

| Control        | Descripción del comportamiento                                                                                                                                                                                                                                                                                                                                                              | Predeterminado |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Curva de transferencia | ClientTubeCurveWidget en modo compacto. Dibuja la curva de transferencia del tubo configurada actualmente con una bola en vivo en la entrada.                                                                                                                                                                                                                                                     | —              |
| Drive          | Mapeo lineal. Empuja más señal hacia la etapa de tubo. Clave de configuración: `ClientTubeTxDriveDb` / `ClientTubeRxDriveDb`. Etiqueta 'X.XX dB'.                                                                                                                                                                                                                                              | 0.00 dB        |
| Tone           | Mapeo lineal. Los valores negativos oscurecen, los positivos iluminan la señal saturada. Clave de configuración: `ClientTubeTxTone` / `ClientTubeRxTone`. Etiqueta 'X.XX'.                                                                                                                                                                                                                        | 0.00           |
| A              | Selecciona el modelo de carácter de tubo A. Exclusivo con B y C. Ámbar cuando está marcado. Clave de configuración: `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero 0/1/2).                                                                                                                                                                                             | marcado        |
| B              | Selecciona el modelo de carácter de tubo B. Exclusivo con A y C. Ámbar cuando está marcado. Clave de configuración: `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero 0/1/2).                                                                                                                                                                                             | no marcado     |
| C              | Selecciona el modelo de carácter de tubo C. Exclusivo con A y B. Ámbar cuando está marcado. Clave de configuración: `ClientTubeTxModel` / `ClientTubeRxModel` (almacenado como entero 0/1/2).                                                                                                                                                                                             | no marcado     |
| Bias           | Mapeo lineal. Desplaza el punto de operación en la curva de transferencia, cambiando la mezcla armónica. La etiqueta se muestra como porcentaje. Clave de configuración: `ClientTubeTxBias` / `ClientTubeRxBias`.                                                                                                                                                                          | 0 %            |
| Output         | Mapeo lineal. Ganancia de compensación / recorte posterior al tubo. Etiqueta 'X.XX dB'. Clave de configuración: `ClientTubeTxOutputDb` / `ClientTubeRxOutputDb`.                                                                                                                                                                                                                             | 0.00 dB        |
| Dry/Wet        | Mapeo lineal. Mezcla de señal seca / procesada (100 % = señal completamente saturada). La etiqueta se muestra como porcentaje. Clave de configuración: `ClientTubeTxDryWet` / `ClientTubeRxDryWet`.                                                                                                                                                                                        | 100 %          |
| Envelope       | Mapeo lineal (-1.0 a +1.0). Los valores positivos aumentan la drive en los transitorios (el tubo se calienta más en los picos fuertes); los valores negativos la reducen, comprimiendo los armónicos dinámicamente. La etiqueta se muestra como porcentaje con signo. Clave de configuración: `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope`.                                             | 0 %            |
| Attack         | Mapeo exponencial (0.1 * 300^n). Establece qué tan rápido responde el seguidor de envolvente a los niveles crecientes cuando Envelope ≠ 0. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima. Clave de configuración: `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs`.                                                                                                             | 5.00 ms        |
| Release        | Mapeo exponencial (10 * 50^n). Establece qué tan rápido se recupera el seguidor de envolvente después de que los niveles bajan cuando Envelope ≠ 0. Etiqueta 'X.XX ms' por debajo de 100 ms, 'X.X ms' por encima. Clave de configuración: `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs`.                                                                                               | 35.00 ms       |
| RN2            | Alternancia solo para TX (oculta en modo RX). Habilita el eliminador de ruido neuronal RNNoise en la entrada del micrófono antes de la cadena DSP. Suprime el ruido de fondo antes de que llegue al compuerta/compresor/saturador. Ubicado en el StripTubePanel flotante debajo del medidor de nivel de salida, solo en el lado TX. Solo modos de voz: los modos digitales (RADE, DAX, RTTY, FT8, FDV, CW) omiten esta etapa. La configuración se conserva a través de AudioEngine. | no marcado     |

## Medidor de nivel de salida (solo editor)

El editor flotante contiene un medidor de nivel **OUT** en su columna del extremo derecho. Muestra el nivel pico posterior a la saturación utilizando balística de ataque rápido / liberación lenta. Las bandas de color son:

| Color | Rango |
|---|---|
| Verde | −60 a −12 dB |
| Lima | −12 a −6 dB |
| Ámbar | −6 a −3 dB |
| Rojo | Por encima de −3 dB |

El medidor no está presente en el mosaico del applet acoplado.

La omisión de cada instancia se controla desde el widget CHAIN, no desde dentro del mosaico del tubo. Consulte [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md).

## Apariencia de las perillas y soporte de temas

En v26.6.1, todas las perillas en el applet de tubo (y en todo AetherSDR) siguen el tema de color. Su apariencia se obtiene de cinco claves de color de tema dedicadas:

| Componente de la perilla | Clave del tema | Efecto de ejemplo |
|--------------------------|----------------|-------------------|
| Anillo de fondo          | `color.knob.background` | El arco no iluminado detrás del arco de la perilla |
| Arco de primer plano     | `color.knob.foreground` | El arco que muestra el valor actual |
| Mango / puntero          | `color.knob.handle` | La línea que apunta al valor actual |
| Texto del valor          | `color.text.primary` | El valor numérico dibujado debajo de la perilla |
| Texto de la etiqueta     | `color.text.secondary` | El nombre del control dibujado encima de la perilla |

El widget de la curva de transferencia también sigue el tema:

| Elemento de la curva | Clave del tema | Efecto de ejemplo |
|----------------------|----------------|-------------------|
| Fondo                | `color.background.0` | El relleno del área del gráfico |
| Marco / cuadrícula   | `color.background.1` | El borde y las líneas de la cuadrícula |
| Líneas de los ejes   | `color.background.1` | Líneas de los ejes horizontal y vertical |
| Línea de la curva    | `color.accent.dim` | La curva de transferencia del tubo |
| Resplandor de la bola| `color.accent.warning` | El resplandor alrededor de la bola de entrada en vivo |
| Núcleo de la bola    | `color.text.primary` | El punto central de la bola de entrada en vivo |

El contenedor del widget en sí está etiquetado con el contenedor de tema `applet/tube`, lo que permite anulaciones de color por applet para las perillas y la curva del tubo.

## Consejos

- Comience con Drive en 0.00 dB y súbalo lentamente hasta que la curva de transferencia comience a doblarse visiblemente. La bola de entrada en vivo muestra si los picos están alcanzando la región saturada.
- Use Output para devolver el nivel procesado a la par con el nivel seco después de agregar Drive, de modo que las comparaciones tengan el nivel igualado. Observe el medidor OUT en el editor para verificar los niveles pico posteriores a la saturación.
- Configure Dry/Wet por debajo del 100 % para mezclar en paralelo con la señal seca, lo que puede agregar cuerpo sin el carácter completo de la saturación total.
- Bias al 0 % produce una curva simétrica. Elevarlo introduce asimetría, desplazando el contenido armónico hacia armónicos de orden par.
- Use el Modelo A, B o C para cambiar el carácter fundamental de la curva del tubo antes de ajustar Drive y Bias.
- Configure Envelope en un valor positivo para que la saturación siga los transitorios: los picos fuertes impulsan el tubo más automáticamente. Use Attack y Release para controlar qué tan rápido reacciona y se recupera el seguidor.
- Cuando una etapa de tubo está omitida, el mosaico acoplado se atenúa visiblemente. Si nota que el mosaico parece desvanecido, verifique que la etapa esté habilitada en el widget CHAIN antes de ajustar los controles.
- Use la edición de valor en línea (haga clic en la etiqueta de la perilla) para ingresar números exactos rápidamente en lugar de girar una perilla. Presione Escape para cancelar la edición.

## Relacionado

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Shift Bias to tweak the even / odd harmonic balance](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Brighten or darken the saturated signal with Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-mix.md)
- [Bypass the tube from either chain](bypass-the-tube-from-either-chain.md)
