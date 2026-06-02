# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo establecer el nivel de umbral en el cual el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) comienza a actuar. Reducir el umbral hace que el compresor se active antes y afecte a más parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero atenuado a aproximadamente 55% de opacidad. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado o si necesita reactivar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe ser visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Busque el control **Thresh** en la fila de cinco controles en la parte inferior del mosaico.
3. Haga clic y arrastre el control **Thresh** hacia arriba para aumentar el umbral o hacia abajo para reducirlo. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Para introducir un valor directamente, haga clic en la etiqueta de valor debajo de cualquier control. Aparece una superposición QLineEdit con un sutil fondo oscuro y un borde cian. Escriba el valor deseado y presione Enter. El editor también confirma el valor cuando pierde el foco (por ejemplo, al hacer clic en otro lugar del applet). El valor se limita automáticamente al rango válido.
5. Observe la curva de transferencia y la bola de envolvente sobre la fila de controles. A medida que ajusta el umbral, el punto de inflexión en la curva se desplaza y la posición de la bola en relación con la curva cambia para reflejar dónde cae el nivel de señal actual.
6. Observe la barra de reducción de ganancia. El relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en −6 dB indica una cantidad de trabajo típica de reducción de ganancia.
7. Suelte el control cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Qué hace cada control

| Control            | Valor predeterminado | Rango válido | Comportamiento |
|--------------------|---------|-------------|----------|
| Thresh             | −18.0 dB | −60.0 a 0.0 dB | Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. Etiqueta con formato '-18.0 dB'. |
| Ratio              | 3.0 | 1.0 a 20.0 | Mapeo logarítmico (1 * 20^n). Establece cuán fuertemente se sostienen los picos una vez superado el umbral. Etiqueta con formato 'X.XX:1'. |
| Attack             | 20.0 ms | 0.1 a 300.0 ms | Mapeo exponencial (0.1 * 3000^n). Establece la rapidez con que el compresor actúa después de superar el umbral. Etiqueta con formato 'X.X ms' por debajo de 10, 'X ms' por encima. |
| Release            | 200 ms | 5 a 2000 ms | Mapeo exponencial (5 * 400^n). Establece la rapidez con que la ganancia retorna después de que la entrada cae por debajo del umbral. Etiqueta con formato 'X ms'. |
| Makeup             | 0.0 dB | −12.0 a 24.0 dB | Mapeo lineal. Añade ganancia para compensar la pérdida por compresión. La etiqueta muestra un signo '+' explícito para valores positivos. |
| Curva de transferencia | — | — | ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia entrada/salida más una bola en vivo que muestra el nivel de envolvente actual. Solo vista en el applet; editable en el ClientCompEditor flotante. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | Barra horizontal ámbar, relleno desde la derecha. La escala máxima es 20 dB de reducción; una marca en -6 dB señala una cantidad de trabajo típica. Actualizada a ~30 Hz desde ClientComp::gainReductionDb() con balística MeterSmoother. |
| Drive              | 0.0 dB | 0.0 a 18.0 dB | Aumento de ganancia previo a la compresión con auto-makeup vinculado. Empuja más señal a través del umbral para que el compresor actúe con más fuerza, y simultáneamente añade la misma cantidad de ganancia en la salida, de modo que el RMS promedio se eleva junto con los picos en lugar de caer. Combínelo con Phase para mantener los picos limpios. Se muestra solo en el StripCompPanel flotante (columna derecha). La etiqueta muestra '+X.X dB'. El tooltip explica el emparejamiento de reducción PAPR #2887. El auto-makeup coincide con el modelo broadcast-Optimod: Drive empuja más material a la curva Y añade la misma ganancia de vuelta, para que el Makeup fijo del usuario se mantenga como un control de ajuste fino posterior a todo. |
| Phase              | 0 etapas | 0 a 6 etapas | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza picos de voz asimétricos antes de la compresión para reducir PAPR. Se muestra solo en el StripCompPanel flotante (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Tooltip: 'Rotador de fase previo a la compresión (#2887). Cascada de paso total que simetriza picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor predeterminado de broadcast.' Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcionales) cubren el rango de formantes del habla sin agruparse. |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y reduzca el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de knee y limiter, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de knee y techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual inmediata: si la bola nunca sale del segmento recto inferior izquierdo, el umbral está por encima de su nivel de señal típico y el compresor no está actuando.
- Para ingresar valores precisos, haga clic en la etiqueta de valor debajo de cualquier control para abrir el editor en línea. Escriba el número (con reconocimiento de configuración regional; se admite coma como separador decimal) y presione Enter.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad de brillo. Esto es solo un indicador visual y no afecta a ningún valor guardado de los controles.
- La curva de transferencia y la bola de envolvente ahora respetan los colores del tema actual. El fondo, las líneas de cuadrícula, la curva y el resplandor de la bola reflejan la paleta del tema activo para una apariencia visual coherente en toda la aplicación.

## Solución de problemas

- **El control Thresh está presente pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — Es posible que la etapa del compresor aún esté en bypass, o que el motor de audio no esté ejecutándose. Confirme que la etapa esté habilitada a través del widget CHAIN y que el audio esté fluyendo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Actívela desde el widget CHAIN para restaurar el brillo completo y el procesamiento activo. El mosaico permanece visible mientras está en bypass, a diferencia de versiones anteriores donde estaba oculto.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
