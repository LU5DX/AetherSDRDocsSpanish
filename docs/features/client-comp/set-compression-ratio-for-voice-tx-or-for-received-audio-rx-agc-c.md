# Configurar la Relación de Compresión para Voz (TX) o Audio Recibido (RX AGC-C)

El mando Ratio controla la intensidad con la que el compresor recorta los picos una vez que la señal supera el umbral. Una relación más alta proporciona una compresión más agresiva en los picos de voz fuertes (lado TX) o en el audio recibido fuerte (lado RX AGC-C).

## Antes de empezar

- La etapa del compresor debe estar habilitada (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico completo del applet se atenúa aproximadamente al 55 % de opacidad para indicar que está inactiva. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- Abra el contenedor principal "Aetherial Audio (TXDSP)" y expanda el subcontenedor correspondiente: "Aetherial Compressor" para TX, o "Aetherial AGC-C" para RX.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del applet. Los mandos están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Gire el mando **Ratio** para ajustar la relación de compresión.
   - Para la compresión de voz TX, este mando persiste en `ClientCompTxRatio`.
   - Para RX AGC-C, este mando persiste en `ClientCompRxRatio`.
3. Lea el valor actual en la etiqueta debajo del mando. Tiene el formato `X.XX:1` (por ejemplo, `3.00:1`).
4. Opcionalmente, haga clic en la etiqueta de valor debajo de un mando para introducir un valor numérico preciso. La etiqueta se convierte en un campo de texto editable con fondo oscuro y borde cian. Escriba un valor y presione Enter, o haga clic en otro lugar, para confirmar el nuevo valor. Presione Escape para cancelar la edición y restaurar el valor anterior. Este editor en línea está disponible en los cinco mandos (Thresh, Ratio, Attack, Release, Makeup).
5. Observe la barra de reducción de ganancia y el punto envolvente en la curva de transferencia mientras habla (TX) o mientras se reproduce audio (RX) para confirmar que la relación está produciendo la cantidad de reducción de ganancia deseada.

## Función de cada control

| Control  | Valor por defecto                                                                                                                                                                                                                           | Rango válido                                   |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| Ratio    | 3.0                                                                                                                                                                                                                                         | 1.0 a 20.0                                     |
| Thresh   | -18.0 dB                                                                                                                                                                                                                                    | -60.0 a 0.0 dB                                 |
| Attack   | 20.0 ms                                                                                                                                                                                                                                     | 0.1 a 300.0 ms                                 |
| Release  | 200 ms                                                                                                                                                                                                                                      | 5 a 2000 ms                                    |
| Makeup   | 0.0 dB                                                                                                                                                                                                                                      | -12.0 a 24.0 dB                                |
| Drive    | Aumento de ganancia previo a la compresión. Envía más señal por encima del umbral para que el compresor actúe con más fuerza, elevando la potencia media. Combínelo con Phase para mantener los picos limpios.                               | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra '+X.X dB'. La información sobre herramientas explica la combinación para reducir PAPR #2887. |
| Phase    | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase pre-comp (#2887). 0=off, 4=default de radiodifusión.' |

El mando Ratio utiliza un mapeo logarítmico (`1 × 20^n`) para que las relaciones bajas (compresión suave, 1.0–4.0:1) ocupen la mayor parte del recorrido del mando y las relaciones altas (limitación fuerte, hasta 20.0:1) se concentren en el extremo superior.

## Visualización de la curva de transferencia

El ClientCompCurveWidget en modo compacto dibuja la curva de transferencia estática de entrada/salida con un "punto" animado que muestra el nivel de envolvente actual. Las etiquetas de los ejes se representan mediante objetos QStaticText almacenados en caché que se reconstruyen automáticamente cuando el applet cambia entre las vistas compacta y expandida. En el applet, la curva es solo de visualización; para editar los parámetros de Knee y techo del limitador, abra el ClientCompEditor flotante haciendo doble clic en la etapa COMP en el widget CHAIN.

## Medidor de reducción de ganancia

La barra horizontal de color ámbar se llena de derecha a izquierda, mostrando hasta 20 dB de reducción de ganancia. Una marca en -6 dB indica una cantidad de reducción de trabajo típica. El medidor se actualiza a aproximadamente 30 Hz utilizando la balística de MeterSmoother aplicada al valor `ClientComp::gainReductionDb()`.

## Consejos

- Una relación entre 2.0:1 y 4.0:1 es típica para la compresión de voz TX. Los valores superiores a 10.0:1 se acercan a un comportamiento de limitación.
- La barra de reducción de ganancia muestra hasta 20 dB de reducción. Una marca en -6 dB indica una cantidad de reducción de ganancia de trabajo típica. Si la barra rara vez alcanza esa marca, es posible que el umbral esté demasiado alto para que la relación actual tenga mucho efecto.
- Aumentar la relación mientras se reduce Makeup mantiene estable el nivel de salida medio al mismo tiempo que ajusta el rango dinámico.
- Para acceder a los controles de Knee y techo del limitador, que moldean aún más cómo se aplica la relación, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN.
- Al hacer clic en la etiqueta de valor de un mando, se abre un editor en línea para la introducción numérica precisa. Esto funciona en los cinco mandos y admite separadores decimales adaptados a la configuración regional (por ejemplo, "12,5" en configuraciones regionales que usan coma decimal). El editor también acepta valores con unidades o símbolos finales (por ejemplo, "12.5 ms" o "−6 dB").

## Solución de problemas

- **El mando Ratio no tiene efecto audible** — Es posible que la etapa aún esté en bypass. Confirme que el compresor esté habilitado en el lado correcto (TX o RX) a través del widget CHAIN. Cuando la etapa está en bypass, el mosaico del applet se atenúa aproximadamente al 55 % de opacidad; restaure la opacidad completa habilitando la etapa.
- **La barra de reducción de ganancia está fija en el máximo** — Es probable que el umbral esté demasiado bajo en relación con el nivel de señal de entrada. Reduzca la relación o suba el mando Thresh hasta que la barra muestre una reducción moderada e intermitente.
- **El editor en línea no acepta el valor introducido** — Asegúrese de que el valor esté dentro del rango válido para ese mando (consulte la tabla anterior). El editor ajusta los valores fuera de rango al límite válido más cercano cuando presiona Enter o hace clic en otro lugar.

## Relacionados

- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
