# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación recupera el nivel general que se pierde cuando el compresor reduce los picos. Ajuste el control **Makeup** en el lado TX o RX para que el audio comprimido salga con un nivel consistente y útil.

## Antes de empezar

- El applet Compresor Aetherial (TX) o AGC-C Aetherial (RX) debe estar visible. Cada recuadro permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (no en bypass) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está en bypass. Cuando una etapa está en bypass, el recuadro completo del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual de que el compresor está fuera de la ruta de señal.

## Pasos

1. Localice el recuadro "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP).
2. Busque el control **Makeup** — es el control más a la derecha en la fila de cinco controles en la parte inferior del applet.
3. Gire el control **Makeup** al valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin signo (por ejemplo, `-3.0 dB`). Para escribir un valor directamente, haga clic en la etiqueta de valor del control; aparecerá un pequeño editor en línea con un borde cian. Escriba el número deseado (por ejemplo, `6.0`) y presione **Enter** o haga clic en otro lugar para confirmar. El control se ajusta al valor ingresado, limitado al rango válido.
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación igual a aproximadamente la mitad de la reducción de ganancia mostrada en la barra.

## Qué hace cada control

| Control   | Valor predeterminado | Rango válido |
|-----------|----------------------|--------------|
| Makeup (TX) | `0.0 dB` | `-12.0` a `+24.0 dB` |
| Makeup (RX) | `0.0 dB` | `-12.0` a `+24.0 dB` |
| Drive     | Aumento de ganancia previo a la compresión. Introduce más señal a través del umbral para que el compresor actúe con más fuerza, elevando la potencia promedio. Combínelo con Phase para mantener los picos limpios. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta aparece como '+X.X dB'. El tooltip explica la reducción de PAPR #2887. |
| Phase     | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir la PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Tooltip: 'Pre-comp phase rotator (#2887). 0=off, 4=broadcast default.' |

El control **Makeup** utiliza un mapeo lineal. Agrega una cantidad fija de ganancia después de la etapa del compresor. No afecta el umbral, la relación ni ningún otro parámetro del compresor.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa regularmente en o más allá de la marca de `-6 dB`, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar el volumen.
- La ganancia de compensación se aplica antes de la etapa del limitador (si está habilitado). Si agrega un valor grande de compensación y la salida recorta, habilite el limitador y establezca un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.
- La curva de transferencia en el applet ahora utiliza un sistema de etiquetas de texto en caché que se adapta al modo compacto. Cuando el applet está en modo compacto, las etiquetas de los ejes usan una fuente más pequeña de 7 píxeles en lugar de 9 píxeles. Las etiquetas en sí permanecen iguales: muestran los valores de las marcas principales (por ejemplo, -60, -40, -20, 0) a lo largo de los ejes.
- La edición en línea también funciona en los controles Thresh, Ratio, Attack y Release. Haga clic en la etiqueta de valor de cualquier control para escribir un valor numérico preciso. Presione **Enter** o tabule para confirmar, o presione **Escape** para cancelar y revertir.

## Solución de problemas

- **El control Makeup no tiene efecto audible** — Es probable que la etapa del compresor esté en bypass. El recuadro del applet aparecerá atenuado (aproximadamente 55 % de opacidad) cuando está en bypass. Vuelva a habilitarlo mediante el widget CHAIN para que el compresor esté en la ruta de señal. Consulte [Poner en bypass el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos recortan** — El valor de compensación combinado con su nivel de señal está excediendo el margen de reserva. Reduzca **Makeup**, o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El editor en línea acepta un valor pero el control no cambia** — El valor ingresado puede estar fuera del rango válido. Los valores se limitan silenciosamente; verifique la etiqueta del control para confirmar el valor resultante. Si el control se comporta de forma inesperada, intente ingresar un número más simple (por ejemplo, `6` en lugar de `6.0`).

## Relacionados

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Ver la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Poner en bypass el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
