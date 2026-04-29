# Aplicar ganancia de compensación después de la compresión

La ganancia de compensación corrige el nivel general que se pierde cuando el compresor reduce los picos. Ajuste el control **Makeup** en el lado TX o RX para que el audio comprimido salga a un nivel uniforme y utilizable.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. Cada bloque permanece oculto hasta que su etapa se habilita mediante el widget CHAIN.
- El compresor debe estar habilitado (sin bypass) en el lado que desea ajustar. La ganancia de compensación no tiene efecto audible cuando el compresor está en bypass.

## Pasos

1. Localice el bloque "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP).
2. Encuentre el control **Makeup** — el más a la derecha en la fila de cinco controles en la parte inferior del applet.
3. Gire el control **Makeup** hasta el valor deseado. Los valores positivos se muestran con un signo `+` explícito (por ejemplo, `+6.0 dB`); los valores negativos se muestran sin él (por ejemplo, `-3.0 dB`).
4. Observe la barra de reducción de ganancia mientras habla (TX) o escucha (RX). Un buen punto de partida es agregar una ganancia de compensación aproximadamente igual a la mitad de la reducción de ganancia que muestra la barra.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración persistida |
|---------|----------------------|--------------|-----------------------------------|
| Makeup (TX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompTxMakeupDb` |
| Makeup (RX) | `0.0 dB` | `-12.0` a `+24.0 dB` | `ClientCompRxMakeupDb` |

El control **Makeup** utiliza una escala lineal. Agrega una cantidad fija de ganancia después de la etapa del compresor. No afecta el umbral, la relación de compresión ni ningún otro parámetro del compresor.

## Consejos

- Observe la barra de reducción de ganancia mientras transmite o escucha. Si la barra se sitúa habitualmente en la marca `-6 dB` o la supera, está aplicando una compresión significativa; considere agregar ganancia de compensación en el rango de `+4.0` a `+10.0 dB` para recuperar volumen.
- La ganancia de compensación se aplica antes de la etapa limitadora (si está habilitada). Si agrega un valor de compensación elevado y la salida distorsiona, habilite el limitador y establezca un techo adecuado. Consulte [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Los lados TX y RX almacenan sus valores de compensación de forma independiente. Ajustar uno no afecta al otro.

## Solución de problemas

- **El control Makeup no tiene efecto audible** — Es probable que la etapa del compresor esté en bypass. Vuelva a habilitarla mediante el widget CHAIN para que el compresor quede en la cadena de señal. Consulte [Activar el bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **La salida es más fuerte pero los picos están distorsionando** — El valor de compensación combinado con el nivel de su señal está superando el margen dinámico disponible. Reduzca **Makeup**, o abra el editor completo y habilite el limitador con un techo adecuado. Consulte [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Temas relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Observar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del Compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Activar el bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
