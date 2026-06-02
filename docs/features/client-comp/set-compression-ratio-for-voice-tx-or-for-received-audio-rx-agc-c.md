# Cómo establecer la relación de compresión para voz (TX) o audio recibido (RX AGC-C)

El mando de Relación (Ratio) controla la intensidad con la que el compresor recorta los picos una vez que la señal supera el umbral. Una relación más alta proporciona una compresión más agresiva de los picos de voz fuertes (en el lado TX) o del audio recibido con alto volumen (en el lado RX AGC-C).

## Antes de comenzar

- La etapa de compresión debe estar activada (sin bypass) en el lado que desea ajustar. Cuando la etapa está en bypass, todo el mosaico del applet se atenúa a aproximadamente el 55 % de opacidad para indicar que está inactiva. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal "Aetherial Audio (TXDSP)" y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Gire el mando **Ratio** para establecer la relación de compresión.
   - Para la compresión de voz en TX, este mando persiste en `ClientCompTxRatio`.
   - Para RX AGC-C, este mando persiste en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta debajo del mando. Tiene el formato `X.XX:1` (por ejemplo, `3.00:1`).
4. Opcionalmente, haga clic en la etiqueta de valor debajo de un mando para introducir un valor numérico preciso. La etiqueta se convierte en un campo de texto editable con fondo oscuro y borde cian. Escriba un valor y presione Enter, o haga clic en otro lugar, para confirmar el nuevo valor. Presione Escape para cancelar la edición y restaurar el valor anterior. Este editor en línea está disponible en los cinco mandos (Thresh, Ratio, Attack, Release, Makeup).
5. Observe la barra de reducción de ganancia y la bola de la envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación produce la cantidad de reducción de ganancia deseada.

## Función de cada control

| Control | Valor predeterminado | Rango válido |
|---------|---------------------|--------------|
| Ratio | 3.0 | 1.0 a 20.0 |
| Thresh | -18.0 dB | -60.0 a 0.0 dB |
| Attack | 20.0 ms | 0.1 a 300.0 ms |
| Release | 200 ms | 5 a 2000 ms |
| Makeup | 0.0 dB | -12.0 a 24.0 dB |
| Drive | 0.0 dB | 0.0 a 18.0 dB |
| Phase | 0 etapas (desactivado) | 0 a 6 etapas |

El mando Ratio utiliza una asignación logarítmica (`1 × 20^n`) para que las relaciones bajas (compresión suave, 1.0–4.0:1) ocupen la mayor parte del recorrido del mando y las relaciones altas (limitación fuerte, hasta 20.0:1) se concentren en el extremo superior.

El mando Drive proporciona un aumento de ganancia previo a la compresión con maquillaje automático vinculado. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza y, simultáneamente, añade la misma cantidad de ganancia en la salida para que el RMS promedio se eleve junto con los picos, en lugar de disminuir. Combínelo con Phase para mantener los picos limpios. Drive se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra '+X.X dB'. El maquillaje automático sigue el modelo broadcast-Optimod: Drive introduce más material en la curva Y añade la misma ganancia de retorno, de modo que el ajuste fijo de Makeup del usuario permanece como un mando de ajuste fino posterior y limpio.

El mando Phase controla el número de secciones de paso total en cascada (0 = desactivado, 1–6 etapas). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). El rotador de fase simetriza los picos de voz asimétricos antes de la compresión para reducir la relación pico a potencia promedio (PAPR). Phase se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra 'Off' cuando es 0, 'N stg' cuando está activo. La información sobre herramientas explica: 'Pre-comp phase rotator (#2887). Cascada de paso total que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor predeterminado de emisión.' Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcionales) cubren el rango de formantes del habla sin agruparse.

## Visualización de la curva de transferencia

El ClientCompCurveWidget en modo compacto dibuja la curva de transferencia estática de entrada/salida con una "bola" en vivo que muestra el nivel actual de la envolvente. Las etiquetas de los ejes se renderizan utilizando objetos QStaticText en caché que se reconstruyen automáticamente cuando el applet cambia entre vistas compacta y expandida. En el applet, la curva es solo de visualización; para editar los parámetros de Knee y el techo del limitador, abra el editor flotante ClientCompEditor haciendo doble clic en la etapa COMP en el widget CHAIN.

El widget de la curva de transferencia utiliza tokens de color del tema activo a través de `ThemeManager::color()`:
- Fondo: `color.background.0`
- Líneas de cuadrícula: `color.background.1`
- Etiquetas de eje: `color.text.label`
- Diagonal de unidad: `color.background.1`
- Curva del compresor: `color.accent.dim`
- Brillo de la bola envolvente: `color.accent.warning`
- Núcleo de la bola envolvente: `color.text.primary`

## Medidor de reducción de ganancia

La barra horizontal de color ámbar se llena de derecha a izquierda, mostrando hasta 20 dB de reducción de ganancia. Una marca en -6 dB indica una cantidad de reducción de trabajo típica. El medidor se actualiza aproximadamente a 30 Hz utilizando la balística de MeterSmoother aplicada al valor `ClientComp::gainReductionDb()`.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz en TX. Los valores superiores a 10.0:1 se acercan a un comportamiento de limitación.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia de trabajo típica. Si la barra rara vez alcanza esa marca, es posible que el umbral esté demasiado alto para que la relación actual tenga mucho efecto.
- Aumentar la relación mientras se reduce Makeup mantiene el nivel de salida promedio estable mientras se ajusta el rango dinámico.
- Para acceder a los controles de Knee y al techo del limitador, que moldean aún más cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.
- Hacer clic en la etiqueta de valor de un mando abre un editor en línea para la introducción numérica precisa. Esto funciona en los cinco mandos y admite separadores decimales según la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal). El editor también acepta valores con unidades o símbolos al final (por ejemplo, "12.5 ms" o "−6 dB").
- Para la operación en TX, combine Drive con el Rotador de Fase (en el panel flotante StripCompPanel) para aumentar la potencia promedio mientras mantiene los picos limpios mediante la reducción de PAPR.

## Solución de problemas

- **El mando Ratio no tiene efecto audible** — Es posible que la etapa aún esté en bypass. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) a través del widget CHAIN. Cuando la etapa está en bypass, el mosaico del applet se atenúa a aproximadamente el 55 % de opacidad; restaure la opacidad total habilitando la etapa.
- **La barra de reducción de ganancia está fijada al máximo** — Es probable que el umbral sea demasiado bajo en relación con el nivel de señal entrante. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.
- **El editor en línea no acepta el valor introducido** — Asegúrese de que el valor esté dentro del rango válido para ese mando (consulte la tabla anterior). El editor limita los valores fuera de rango al límite válido más cercano cuando presiona Enter o hace clic en otro lugar.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
