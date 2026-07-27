# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación recupera el nivel general que se pierde cuando el compresor reduce los picos. Ajuste el mando **Makeup** en el lado TX o RX para que el audio comprimido salga a un nivel consistente y útil.

## Antes de comenzar

- El applet Compresor Aetherial (TX) o AGC-C Aetherial (RX) debe estar visible. Cada recuadro permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (no omitido) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está omitido. Cuando una etapa está omitida, todo el recuadro del applet se atenúa a aproximadamente un 55 % de opacidad como indicador visual de que el compresor está fuera de la ruta de la señal.

## Pasos

1. Localice el recuadro "Compresor Aetherial" (lado TX) o "AGC-C Aetherial" (lado RX) dentro del contenedor principal Audio Aetherial (TXDSP).
2. Encuentre el mando **Makeup** — el mando más a la derecha en la fila de cinco mandos en la parte inferior del applet.
3. Gire el mando **Makeup** al valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin él (por ejemplo, `-3.0 dB`). Para escribir un valor directamente, haga clic en la etiqueta de valor del mando; aparecerá un pequeño editor en línea con un borde cian. Escriba el número deseado (por ejemplo, `6.0`) y presione **Enter** o haga clic en otro lugar para confirmar. El mando saltará al valor ingresado, limitado al rango válido.
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación equivalente a aproximadamente la mitad de la reducción de ganancia mostrada en la barra.

## Qué hace cada control

| Control       | Valor predeterminado | Rango válido       |
|---------------|----------------------|--------------------|
| Thresh        | -18.0 dB             | -60.0 a 0.0 dB     |
| Ratio         | 3.0                  | 1.0 a 20.0         |
| Attack        | 20.0 ms              | 0.1 a 300.0 ms     |
| Release       | 200 ms               | 5 a 2000 ms        |
| Makeup (TX)   | 0.0 dB               | -12.0 a +24.0 dB   |
| Makeup (RX)   | 0.0 dB               | -12.0 a +24.0 dB   |
| Drive         | 0.0 dB               | 0.0 a 18.0 dB      |
| Phase         | 0 etapas             | 0 a 6 etapas       |

El mando **Makeup** utiliza un mapeo lineal. Agrega una cantidad fija de ganancia después de la etapa del compresor. No afecta el umbral, la relación ni ningún otro parámetro del compresor.

Los mandos **Drive** y **Phase** están disponibles solo en el panel flotante StripCompPanel (haga doble clic en el recuadro COMP del widget CHAIN). **Drive** agrega un impulso de ganancia previo a la compresión con compensación automática vinculada, enviando más señal a través del umbral mientras agrega simultáneamente la misma ganancia en la salida. Esto eleva el RMS promedio junto con los picos en lugar de reducirlo. **Phase** controla la cantidad de secciones de paso total en cascada (0 a 6 etapas) para la reducción de la relación entre potencia pico y promedio (PAPR). Cada etapa agrega 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz) para simetrizar los picos asimétricos de la voz antes de la compresión. El valor predeterminado de 4 etapas es el estándar de transmisión Optimod.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa regularmente en o más allá de la marca de `-6 dB`, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar el volumen.
- La ganancia de compensación se aplica antes de la etapa del limitador (si está habilitado). Si agrega un valor de compensación grande y la salida se recorta, habilite el limitador y establezca un techo adecuado. Consulte [Abra el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.
- La curva de transferencia en el applet utiliza un sistema de etiquetas de texto en caché que se adapta al modo compacto. Cuando el applet está en modo compacto, las etiquetas de los ejes usan una fuente más pequeña de 7 píxeles en lugar de 9 píxeles. Las etiquetas en sí siguen siendo las mismas: muestran los valores principales de las marcas (por ejemplo, -60, -40, -20, 0) a lo largo de los ejes.
- La edición en línea también funciona en los mandos Thresh, Ratio, Attack y Release. Haga clic en la etiqueta de valor de cualquier mando para escribir un valor numérico preciso. Presione **Enter** o la tecla de tabulación para confirmar, o presione **Escape** para cancelar y revertir.
- La curva de transferencia, las líneas de cuadrícula y los colores de la bola de la envolvente ahora siguen el tema activo de la aplicación. La curva utiliza el color de énfasis del tema, las líneas de cuadrícula usan colores de fondo, el resplandor de la bola usa el énfasis de advertencia y el núcleo de la bola usa el color de texto principal. Esto asegura que la visualización del compresor se adapte al esquema de colores que haya elegido.
- El medidor de reducción de ganancia (relleno del control deslizante) también utiliza el color de primer plano del control deslizante del tema, lo que le da una apariencia ámbar consistente que coincide con el tema visual general.
- La animación de la bola de la envolvente utiliza un temporizador preciso con renderizado continuo. Cuando la envolvente de compresión se estabiliza, el temporizador de animación se detiene, pero el widget continúa repintándose en cada tic, lo que garantiza que la visualización permanezca precisa y la posición de la bola se actualice sin problemas en todo momento.

## Solución de problemas

- **El mando Makeup no tiene efecto audible** — Es probable que la etapa del compresor esté omitida. El recuadro del applet aparecerá atenuado (aproximadamente un 55 % de opacidad) cuando esté omitido. Vuelva a habilitarlo a través del widget CHAIN para que el compresor esté en la ruta de la señal. Consulte [Omita el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos se recortan** — El valor de compensación combinado con su nivel de señal está superando el margen dinámico. Reduzca **Makeup**, o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abra el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El editor en línea acepta un valor pero el mando no cambia** — El valor ingresado puede estar fuera del rango válido. Los valores se limitan silenciosamente; verifique la etiqueta del mando para confirmar el valor resultante. Si el mando se comporta de manera inesperada, intente ingresar un número más simple (por ejemplo, `6` en lugar de `6.0`).

## Relacionados

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abra el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omita el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
