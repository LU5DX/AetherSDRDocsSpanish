# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación (make-up gain) corrige el nivel general que se pierde cuando el compresor reduce los picos. Ajuste el mando **Makeup** en el lado TX o RX para que el audio comprimido salga a un nivel consistente y útil.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. Cada mosaico permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (no en bypass) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está en bypass.

## Pasos

1. Ubique el mosaico "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP).
2. Localice el mando **Makeup** — el mando más a la derecha en la fila de cinco mandos en la parte inferior del applet.
3. Gire el mando **Makeup** hasta el valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin él (por ejemplo, `-3.0 dB`).
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación equivalente a aproximadamente la mitad de la reducción de ganancia que muestra la barra.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|---------|-------------|-----------------------|
| Makeup (TX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompTxMakeupDb` |
| Makeup (RX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompRxMakeupDb` |

El mando **Makeup** utiliza una asignación lineal. Agrega una cantidad fija de ganancia después de la etapa del compresor. No afecta el umbral, la relación ni ningún otro parámetro del compresor.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa regularmente en la marca `-6 dB` o la supera, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar el volumen.
- La ganancia de compensación se aplica antes de la etapa limitadora (si está habilitada). Si agrega un valor de compensación elevado y la salida recorta, habilite el limitador y establezca un techo apropiado. Consulte [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.

## Resolución de problemas

- **El mando Makeup no tiene efecto audible** — Es probable que la etapa del compresor esté en bypass. Vuelva a habilitarla mediante el widget CHAIN para que el compresor quede en la cadena de señal. Consulte [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos están recortando** — El valor de compensación combinado con el nivel de su señal está superando el margen dinámico disponible. Reduzca **Makeup**, o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Relacionado

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Observar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md)
