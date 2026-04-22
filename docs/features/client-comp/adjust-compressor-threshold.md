# Ajustar el umbral del compresor

Use el control **Thresh** para establecer el nivel de entrada a partir del cual el compresor comienza a reducir la ganancia. Bajar el umbral significa que una mayor parte de la señal de voz es comprimida; subirlo permite que los pasajes más suaves pasen sin ser afectados.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si el bloque COMPRESSOR está oculto, habilite la etapa a través del widget CHAIN o del editor flotante de Compressor. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel de applets.
2. Encuentre el control rotativo etiquetado como **Thresh** en la fila de cinco controles en la parte inferior del bloque.
3. Haga clic y arrastre el control **Thresh** hacia arriba para subir el umbral o hacia abajo para bajarlo. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Observe la curva de transferencia ubicada sobre la fila de controles. El punto de rodilla en la curva se desplaza a medida que ajusta el umbral, indicando dónde comenzará la compresión.
5. Hable por el micrófono y observe la bola de envolvente sobre la curva de transferencia. Cuando la bola se sitúa por encima de la rodilla, el compresor está activo. La barra de reducción de ganancia se ilumina en color ámbar para confirmar que se está reduciendo la ganancia.
6. Suelte el control cuando el umbral esté en el valor deseado. El valor se guarda automáticamente en `ClientCompTxThresholdDb`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| **Thresh** | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| **Ratio** | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| **Attack** | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| **Release** | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| **Makeup** | +0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

La **curva de transferencia** es un indicador de solo visualización en el applet. Dibuja la curva estática de entrada/salida y muestra una bola en tiempo real en el nivel actual de la envolvente. Para editar la rodilla y los ajustes del limitador que no están expuestos en el applet, abra el editor flotante.

La **barra de reducción de ganancia** es una franja horizontal de color ámbar que se llena desde la derecha. La escala va de 0 a 20 dB de reducción. Una marca en −6 dB indica una cantidad de reducción de ganancia típica en operación normal.

## Consejos

- Comience con el umbral predeterminado de -18.0 dB y bájelo en pasos pequeños mientras habla. Detenga el ajuste cuando la barra de reducción de ganancia muestre aproximadamente 6 dB de reducción durante los picos normales de voz.
- Si baja el umbral de forma significativa, agregue ganancia de compensación con el control **Makeup** para contrarrestar la reducción del nivel promedio.
- La rodilla y el techo del limitador no son ajustables desde el applet. Abra el editor completo para acceder a esos controles.

## Solución de problemas

- **El control Thresh es visible pero la barra de reducción de ganancia nunca se ilumina** — Es posible que la etapa Compressor esté en bypass. Verifique el widget CHAIN y confirme que la etapa Compressor esté habilitada. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- **El bloque COMPRESSOR no es visible en el panel de applets** — El bloque permanece oculto hasta que la etapa Compressor esté habilitada. Habilite la etapa desde el widget CHAIN o desde el editor flotante de Compressor.

## Relacionados

- [Descripción general del compresor](overview.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Ajustar ataque y liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Observar la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Abrir el editor completo de Compressor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
