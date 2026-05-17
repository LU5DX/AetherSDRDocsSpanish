# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación recupera el nivel general perdido cuando el compresor reduce los picos. Ajuste el mando **Makeup** en el lado TX o RX para que el audio comprimido tenga un nivel consistente y útil.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. Cada mosaico permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (no en bypass) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está en bypass. Cuando una etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual de que el compresor está fuera de la ruta de la señal.

## Pasos

1. Localice el mosaico "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) en el contenedor principal Aetherial Audio (TXDSP).
2. Busque el mando **Makeup** — es el mando más a la derecha en la fila de cinco mandos en la parte inferior del applet.
3. Gire el mando **Makeup** al valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin signo (por ejemplo, `-3.0 dB`). Para escribir un valor directamente, haga clic en la etiqueta del valor del mando; aparecerá un pequeño editor en línea con un borde cian. Escriba el número deseado (por ejemplo, `6.0`) y presione **Enter** o haga clic en otro lugar para confirmar. El mando se ajusta al valor ingresado, limitado al rango válido.
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación igual a aproximadamente la mitad de la reducción de ganancia mostrada en la barra.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste persistida |
|---------|---------------------|--------------|----------------------------|
| Makeup (TX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompTxMakeupDb` |
| Makeup (RX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompRxMakeupDb` |

El mando **Makeup** usa un mapeo lineal. Agrega una cantidad fija de ganancia después de la etapa del compresor. No afecta el umbral, la relación ni ningún otro parámetro del compresor.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa regularmente en o más allá de la marca de `-6 dB`, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar el volumen.
- La ganancia de compensación se aplica antes de la etapa del limitador (si está habilitado). Si agrega un valor grande de compensación y la salida recorta, habilite el limitador y establezca un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.
- La curva de transferencia en el applet ahora utiliza un sistema de etiquetas de texto en caché que se adapta al modo compacto. Cuando el applet está en modo compacto, las etiquetas de los ejes usan una fuente más pequeña de 7 píxeles en lugar de 9. Las etiquetas en sí siguen siendo las mismas: muestran los valores principales de las marcas (por ejemplo, -60, -40, -20, 0) a lo largo de los ejes.
- La edición en línea también funciona en los mandos Thresh, Ratio, Attack y Release. Haga clic en la etiqueta del valor de cualquier mando para escribir un valor numérico preciso. Presione **Enter** o tabule para confirmar, o presione **Escape** para cancelar y revertir.

## Solución de problemas

- **El mando Makeup no tiene efecto audible** — Probablemente la etapa del compresor esté en bypass. El mosaico del applet aparecerá atenuado (aproximadamente 55 % de opacidad) cuando esté en bypass. Vuelva a habilitarlo mediante el widget CHAIN para que el compresor esté en la ruta de la señal. Consulte [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos recortan** — El valor de compensación combinado con su nivel de señal está superando el margen dinámico. Reduzca **Makeup** o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El editor en línea acepta un valor pero el mando no cambia** — El valor ingresado puede estar fuera del rango válido. Los valores se limitan silenciosamente; verifique la etiqueta del mando para confirmar el valor resultante. Si el mando se comporta de manera inesperada, intente ingresar un número más simple (por ejemplo, `6` en lugar de `6.0`).

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ver la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md)
