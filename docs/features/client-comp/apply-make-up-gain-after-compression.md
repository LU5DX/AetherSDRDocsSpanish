# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación recupera el nivel general que se pierde cuando el compresor reduce los picos. Ajuste el mando **Makeup** en el lado TX o RX para que el audio comprimido salga con un nivel consistente y útil.

## Antes de comenzar

- El applet **Aetherial Compressor** (TX) o **Aetherial AGC-C** (RX) debe estar visible. Cada bloque permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (sin bypass) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está en bypass. Cuando una etapa está en bypass, todo el bloque del applet se atenúa hasta aproximadamente un 55 % de opacidad como indicador visual de que el compresor está fuera de la ruta de señal.

## Pasos

1. Localice el bloque **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) dentro del contenedor principal **Aetherial Audio (TXDSP)**.
2. Busque el mando **Makeup** — es el mando más a la derecha en la fila de cinco mandos en la parte inferior del applet.
3. Gire el mando **Makeup** al valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin signo (por ejemplo, `-3.0 dB`).
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación aproximadamente igual a la mitad de la reducción de ganancia mostrada en la barra.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|---------------------|--------------|-----------------------------------|
| Makeup (TX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompTxMakeupDb` |
| Makeup (RX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompRxMakeupDb` |

El mando **Makeup** utiliza un mapeo lineal. Añade una cantidad fija de ganancia después de la etapa del compresor. No afecta al umbral, la relación ni ningún otro parámetro del compresor.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa regularmente en la marca `-6 dB` o más allá, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar el volumen.
- La ganancia de compensación se aplica antes de la etapa del limitador (si está habilitado). Si agrega un valor grande de compensación y la salida recorta, habilite el limitador y establezca un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.

## Solución de problemas

- **El mando Makeup no tiene efecto audible** — Es probable que la etapa del compresor esté en bypass. El bloque del applet aparecerá atenuado (aproximadamente un 55 % de opacidad) cuando esté en bypass. Vuelva a habilitarlo mediante el widget CHAIN para que el compresor esté en la ruta de señal. Consulte [Poner en bypass el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos recortan** — El valor de compensación combinado con su nivel de señal está superando el margen dinámico. Reduzca **Makeup** o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Relacionados

- [Visión general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ver la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Poner en bypass el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
