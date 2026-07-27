# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo definir el nivel de umbral en el cual el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) comienza a actuar. Bajar el umbral hace que el compresor se active antes y afecte una mayor parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (sin bypass) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero atenuado a aproximadamente 55% de opacidad. Consulte [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado o si necesita volver a habilitar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Busque el control **Thresh** en la fila de cinco controles en la parte inferior del mosaico.
3. Haga clic y arrastre el control **Thresh** hacia arriba para subir el umbral o hacia abajo para bajarlo. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Para ingresar un valor directamente, haga clic en la etiqueta de valor debajo de cualquier control. Aparecerá una superposición QLineEdit con un sutil fondo oscuro y un borde cian. Escriba el valor deseado y presione Enter. El editor también confirma el cambio cuando pierde el foco (por ejemplo, al hacer clic en otra parte del applet). El valor se ajusta automáticamente al rango válido.
5. Observe la curva de transferencia y la bola de envolvente sobre la fila de controles. Al ajustar el umbral, el punto de inflexión en la curva se desplaza y la posición de la bola respecto a la curva cambia para reflejar dónde cae el nivel de señal actual.
6. Observe la barra de reducción de ganancia. El relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en -6 dB indica una cantidad típica de reducción de ganancia.
7. Suelte el control cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Función de cada control

| Control             | Valor predeterminado                                                                                                 | Rango válido                                                                                                                                                                                                                               |
|---------------------|-----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh              | −18.0 dB                                                                                                              | −60.0 a 0.0 dB                                                                                                                                                                                                                             |
| Ratio               | 3.0                                                                                                                   | 1.0 a 20.0                                                                                                                                                                                                                                 |
| Attack              | 20.0 ms                                                                                                               | 0.1 a 300.0 ms                                                                                                                                                                                                                             |
| Release             | 200 ms                                                                                                                | 5 a 2000 ms                                                                                                                                                                                                                                |
| Makeup              | 0.0 dB                                                                                                                | −12.0 a 24.0 dB                                                                                                                                                                                                                            |
| Curva de transferencia | —                                                                                                                     | —                                                                                                                                                                                                                                          |
| Barra de reducción de ganancia | Franja ámbar horizontal, relleno desde la derecha. Escala máxima en 20 dB de reducción; una marca en -6 dB señala una cantidad de trabajo típica. | Se muestrea a ~30 Hz desde ClientComp::gainReductionDb(); la balística de MeterSmoother (animación a 125 Hz, ataque de 30 ms / liberación de 180 ms) hace que el relleno se lea de forma idéntica en todas las superficies de medición. El widget de curva se actualiza en cada tic de animación. |
| Drive               | 0.0 dB                                                                                                                | 0.0 a 18.0 dB                                                                                                                                                                                                                             |
| Phase               | 0 etapas                                                                                                              | 0 a 6 etapas                                                                                                                                                                                                                              |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y baje el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de inflexión (knee) y limitador, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de inflexión y techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia ofrece retroalimentación visual inmediata: si la bola nunca abandona el segmento recto inferior izquierdo, el umbral está por encima de su nivel de señal típico y el compresor no está actuando.
- Para ingresar valores precisos, haga clic en la etiqueta de valor debajo de cualquier control para abrir el editor en línea. Escriba el número (con reconocimiento de configuración regional; se admite la coma como separador decimal) y presione Enter.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad de brillo. Esto es solo un indicador visual y no afecta ningún valor guardado de los controles.
- La curva de transferencia y la bola de envolvente ahora respetan los colores del tema activo. El fondo, las líneas de la cuadrícula, la curva y el resplandor de la bola reflejan la paleta del tema activo para una apariencia visual consistente en toda la aplicación.

## Solución de problemas

- **El control Thresh está presente pero la barra de reducción de ganancia permanece vacía sin importar la posición del umbral** — La etapa del compresor puede estar aún en bypass, o el motor de audio no está en ejecución. Confirme que la etapa esté habilitada mediante el widget CHAIN y que el audio esté fluyendo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Habilítela desde el widget CHAIN para restaurar el brillo completo y reanudar el procesamiento activo. El mosaico permanece visible mientras está en bypass, a diferencia de versiones anteriores donde se ocultaba.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
- [Ajustar la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque/liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de inflexión y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
