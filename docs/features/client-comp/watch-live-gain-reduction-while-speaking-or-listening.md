# Observe la reducción de ganancia en vivo mientras habla o escucha

El ClientCompApplet muestra un medidor de reducción de ganancia en vivo y una curva de transferencia animada mientras el audio pasa por el compresor. Use estos indicadores para ver en tiempo real la intensidad con la que trabaja el compresor, ya sea durante la transmisión (lado TX) o al recibir audio (lado RX), sin necesidad de abrir el editor flotante.

Cada perilla del compresor admite la edición en línea de su valor: haga clic en el texto del valor para ingresar directamente un valor numérico preciso, luego presione Enter o haga clic en otro lugar para confirmarlo.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa del compresor que desea monitorear (TX o RX) debe estar habilitada; el mosaico se muestra con opacidad reducida cuando la etapa está desactivada. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado.

## Pasos

1. Ubique el subcontenedor "Aetherial Compressor" (lado TX) o "Aetherial AGC-C" (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Hable por su micrófono (TX) o deje que se reproduzca el audio recibido (RX).
3. Observe la **Barra de reducción de ganancia** — la franja horizontal ambarina debajo de la curva de transferencia. La franja se llena desde la derecha a medida que aumenta la reducción de ganancia, hasta un máximo de 20 dB.
4. Observe la **Curva de transferencia** — la bola de envolvente en vivo se mueve a lo largo de la curva estática para mostrar el nivel de entrada actual en relación con el umbral y la relación de compresión.
5. Use la marca de -6 dB en la **Barra de reducción de ganancia** como referencia. Un llenado que alcanza o supera ligeramente esa marca es una cantidad de compresión de trabajo típica.

## Ingreso de valores precisos directamente

Haga clic en el texto del valor mostrado de cualquier perilla para abrir un editor en línea. Escriba un número y presione Enter, o haga clic en otro lugar para aplicar el valor. El editor se cierra automáticamente y la perilla se actualiza.

- El editor acepta formatos decimales adaptados a la configuración regional (por ejemplo, "12,5" en locales con coma decimal).
- Ingrese números simples sin unidades (por ejemplo, escriba "5" o "5.0" para un Ataque de 5.0 ms).
- Presione Escape para cancelar la edición y restaurar el valor anterior.
- El editor aparece como una superposición transparente que coincide con la apariencia normal de la etiqueta. Al enfocarse, un fondo ligeramente oscuro y un borde cian indican el modo de edición.

## Función de cada control

| Control            | Tipo                                                                                                                                                                                                                                                                    | Lo que ve                                                                                                                                                                                                                                                 |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | Indicador                                                                                                                                                                                                                                                               | Curva estática de entrada/salida con una bola en vivo en el nivel de envolvente actual. Los colores de la curva, la cuadrícula, la bola y las etiquetas de los ejes siguen el tema activo a través de `ThemeManager`.                                       |
| Barra de reducción de ganancia | Franja horizontal ambarina, se llena desde la derecha. La escala máxima es 20 dB de reducción; una marca en -6 dB señala una cantidad de trabajo típica.                                                                                                                 | Se muestrea a ~30 Hz desde `ClientComp::gainReductionDb()`; la balística de `MeterSmoother` (animación de 125 Hz, ataque de 30 ms / liberación de 180 ms) hace que el llenado se lea de manera idéntica en todas las superficies de medición.            |
| Umbral            | Perilla                                                                                                                                                                                                                                                                 | Umbral actual. Valor predeterminado -18.0 dB; rango -60.0 a 0.0 dB. Haga clic en el valor para escribir un umbral preciso. La configuración se almacena como `ClientCompTxThresholdDb` o `ClientCompRxThresholdDb`.                                       |
| Relación          | Perilla                                                                                                                                                                                                                                                                 | Relación actual. Valor predeterminado 3.0; rango 1.0 a 20.0. Se muestra como X.XX:1. Haga clic en el valor para escribir una relación precisa. La configuración se almacena como `ClientCompTxRatio` o `ClientCompRxRatio`.                              |
| Ataque            | Perilla                                                                                                                                                                                                                                                                 | Tiempo de ataque actual. Valor predeterminado 20.0 ms; rango 0.1 a 300.0 ms. Haga clic en el valor para escribir un tiempo de ataque preciso. La configuración se almacena como `ClientCompTxAttackMs` o `ClientCompRxAttackMs`.                          |
| Liberación        | Perilla                                                                                                                                                                                                                                                                 | Tiempo de liberación actual. Valor predeterminado 200 ms; rango 5 a 2000 ms. Haga clic en el valor para escribir un tiempo de liberación preciso. La configuración se almacena como `ClientCompTxReleaseMs` o `ClientCompRxReleaseMs`.                    |
| Maquillaje        | Perilla                                                                                                                                                                                                                                                                 | Ganancia de maquillaje actual. Valor predeterminado 0.0 dB; rango -12.0 a 24.0 dB. Haga clic en el valor para escribir una ganancia de maquillaje precisa. Muestra un signo '+' explícito para valores positivos. La configuración se almacena como `ClientCompTxMakeupDb` o `ClientCompRxMakeupDb`.                     |
| Drive             | Aumento de ganancia previo a la compresión con maquillaje automático vinculado. Empuja más señal a través del umbral para que el compresor trabaje más intensamente y agrega simultáneamente la misma ganancia en la salida, de modo que el RMS promedio suba junto con los picos en lugar de caer. Combínelo con Phase para mantener los picos limpios. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta se muestra como '+X.X dB'. Rango 0.0 a 18.0 dB. El tooltip explica el emparejamiento de reducción PAPR #2887. La configuración se almacena como `ClientCompTxDriveDb`. |
| Phase             | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa agrega 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Rango de 0 a 6 etapas. La configuración se almacena como `ClientCompTxPhaseRotatorStages`. Tooltip: 'Rotador de fase previo a la compresión (#2887). 0=desactivado, 4=valor predeterminado de radiodifusión.' |

## Consejos

- Si la **Barra de reducción de ganancia** nunca se mueve, el nivel de entrada no está superando el umbral. Reduzca la perilla de Umbral o aumente la ganancia de su micrófono.
- Si la **Barra de reducción de ganancia** está fija en o cerca de 20 dB de forma continua, la relación o el umbral están configurados de forma muy agresiva. Aumente el valor de Umbral o reduzca la perilla de Relación para suavizar la compresión.
- La bola de envolvente en la **Curva de transferencia** se encuentra en la línea de umbral cuando no hay audio presente. Durante el audio, viaja a lo largo de la curva; una bola que se sitúa en la parte curva de la misma confirma una compresión activa.
- Los mosaicos TX y RX se actualizan de forma independiente. Puede monitorear ambos simultáneamente si ambos subcontenedores están expandidos.
- Las etiquetas de los ejes de la curva de transferencia usan texto estático en caché para mejorar el rendimiento del renderizado. La caché se reconstruye automáticamente al alternar entre los modos de visualización compacto y completo.
- Para ingresar un valor preciso, haga clic en el texto del valor mostrado. El editor en línea acepta entrada numérica con separadores decimales adaptados a la configuración regional. Use signos negativos cuando corresponda (por ejemplo, "-24.0" para el umbral).
- Los colores de la curva de transferencia y la barra de reducción de ganancia se adaptan al tema activo. La curva usa el color del tema `color.accent.dim`, el brillo de la bola usa `color.accent.warning` y la cuadrícula usa `color.background.1`.
- El maquillaje automático de la perilla Drive sigue el modelo broadcast-Optimod: empuja más material a la curva Y agrega la misma ganancia de vuelta, de modo que la perilla fija de Maquillaje del usuario permanece como una perilla de recorte posterior limpia y global.
- El valor predeterminado del rotador de fase de 4 etapas (estándar de radiodifusión) usa frecuencias centrales escalonadas de 300/700/1500/2500 Hz con 1000/2000 Hz opcionales para cubrir el rango de formantes del habla sin agruparlas.
- Las animaciones del medidor de reducción de ganancia y la bola de envolvente se ejecutan a una frecuencia de actualización suave y eficiente. El temporizador de animación se detiene automáticamente cuando la señal se estabiliza, pero la pantalla continúa actualizándose. La pantalla se repinta continuamente durante la actividad de audio para garantizar una retroalimentación visual fluida.

## Solución de problemas

- **El mosaico aparece atenuado** — La etapa del compresor está desactivada. El mosaico ahora se renderiza con aproximadamente un 55 % de opacidad cuando la etapa está deshabilitada, coincidiendo con el efecto de atenuación utilizado en la curva EQ. Habilite la etapa desde el widget CHAIN (haga clic único en la etapa COMP) o consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md).
- **La Barra de reducción de ganancia no muestra movimiento durante el audio** — El nivel de entrada no está alcanzando el umbral. Reduzca el valor de la perilla de Umbral o verifique que el dispositivo de audio correcto esté activo y produciendo señal.
- **La bola de envolvente no se mueve** — El applet no está conectado a un motor de audio activo. Verifique que la radio esté conectada y que el audio fluya a través de la cadena de procesamiento TX o RX correspondiente.
- **El editor en línea no aparece** — Haga clic directamente en el texto del valor numérico debajo de cada perilla. El editor solo aparece al hacer clic en el valor, no en el cuerpo de la perilla.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
