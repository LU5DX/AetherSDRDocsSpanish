# Configurar la relación de compresión para la voz (TX) o el audio recibido (RX AGC-C)

El mando Ratio controla la intensidad con la que el compresor recorta los picos una vez que la señal cruza el umbral. Una relación más alta produce un recorte más agresivo en los picos fuertes de voz (lado TX) o en el audio recibido con volumen alto (lado RX AGC-C).

## Antes de empezar

- La etapa del compresor debe estar habilitada (sin derivación) en el lado que desea ajustar. Cuando la etapa está derivada, todo el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad para indicar que está inactivo. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal "Aetherial Audio (TXDSP)" y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Gire el mando **Ratio** para configurar la relación de compresión.
   - Para la compresión de voz en TX, este mando se guarda en `ClientCompTxRatio`.
   - Para RX AGC-C, este mando se guarda en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta debajo del mando. Tiene el formato `X.XX:1` (por ejemplo, `3.00:1`).
4. Opcionalmente, haga clic en la etiqueta de valor debajo de un mando para ingresar un valor numérico preciso. La etiqueta se convierte en un campo de texto editable con un fondo oscuro y un borde cian. Escriba un valor y presione Enter, o haga clic en otro lugar, para confirmar el nuevo valor. Presione Escape para cancelar la edición y restaurar el valor anterior. Este editor en línea está disponible en los cinco mandos (Thresh, Ratio, Attack, Release, Makeup).
5. Observe la barra de reducción de ganancia y la bola de la envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación está produciendo la cantidad deseada de reducción de ganancia.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste guardado (TX / RX) |
|---|---|---|---|
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` |

El mando Ratio utiliza una asignación logarítmica (`1 × 20^n`) de modo que las relaciones bajas (compresión suave, 1.0–4.0:1) ocupen la mayor parte del recorrido del mando y las relaciones altas (limitación dura, hasta 20.0:1) se concentren en el extremo superior.

## Visualización de la curva de transferencia

El ClientCompCurveWidget en modo compacto dibuja la curva de transferencia estática de entrada/salida con una "bola" en vivo que muestra el nivel actual de la envolvente. Las etiquetas de los ejes se representan mediante objetos QStaticText en caché que se reconstruyen automáticamente cuando el applet cambia entre las vistas compacta y expandida. En el applet, la curva es solo de visualización; para editar los parámetros de Knee y techo del limitador, abra el ClientCompEditor flotante haciendo doble clic en la etapa COMP en el widget CHAIN.

## Medidor de reducción de ganancia

La franja horizontal de color ámbar se llena de derecha a izquierda, mostrando hasta 20 dB de reducción de ganancia. Una marca en -6 dB indica una cantidad de reducción de trabajo típica. El medidor se actualiza a aproximadamente 30 Hz utilizando la balística de MeterSmoother aplicada al valor `ClientComp::gainReductionDb()`.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz en TX. Los valores superiores a 10.0:1 se aproximan a un comportamiento de limitación.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia de trabajo típica. Si la barra rara vez alcanza esa marca, es posible que el umbral esté configurado demasiado alto para que la relación actual tenga un efecto significativo.
- Aumentar la relación mientras se reduce Makeup mantiene estable el nivel de salida promedio mientras se ajusta el rango dinámico.
- Para acceder a los controles de Knee y techo del limitador, que dan forma adicional a cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.
- Hacer clic en la etiqueta de valor de un mando abre un editor en línea para la entrada numérica precisa. Esto funciona en los cinco mandos y admite separadores decimales según la configuración regional (por ejemplo, "12,5" en configuraciones regionales que usan coma decimal). El editor también acepta valores con unidades o símbolos al final (por ejemplo, "12.5 ms" o "−6 dB").

## Solución de problemas

- **El mando Ratio no tiene efecto audible** — Es posible que la etapa aún esté en derivación. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) a través del widget CHAIN. Cuando la etapa está derivada, el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad; restaure la opacidad completa habilitando la etapa.
- **La barra de reducción de ganancia está fijada al máximo** — Es probable que el umbral sea demasiado bajo en relación con el nivel de la señal entrante. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.
- **El editor en línea no acepta el valor ingresado** — Asegúrese de que el valor esté dentro del rango válido para ese mando (consulte la tabla anterior). El editor limita los valores fuera de rango al límite válido más cercano cuando presiona Enter o hace clic en otro lugar.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
