# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo configurar el nivel de umbral en el que el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) comienza a actuar. Bajar el umbral hace que el compresor se active antes y afecte a una mayor parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero se atenúa aproximadamente al 55 % de opacidad. Consulte [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado o si necesita reactivar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Encuentre el mando **Thresh** en la fila de cinco mandos en la parte inferior del mosaico.
3. Haga clic y arrastre el mando **Thresh** hacia arriba para aumentar el umbral o hacia abajo para reducirlo. La etiqueta debajo del mando se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Para ingresar un valor directamente, haga clic en la etiqueta del valor debajo de cualquier mando. Aparecerá una superposición de QLineEdit con un sutil fondo oscuro y un borde cian. Escriba el valor deseado y presione Enter. El editor también confirma el valor cuando pierde el foco (por ejemplo, al hacer clic en otro lugar del applet). El valor se ajusta automáticamente al rango válido.
5. Observe la curva de transferencia y la bola de envolvente sobre la fila de mandos. Al ajustar el umbral, el punto de inflexión en la curva se desplaza y la posición de la bola en relación con la curva cambia para reflejar dónde cae el nivel de señal actual.
6. Observe la barra de reducción de ganancia. El relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en −6 dB indica una cantidad de trabajo típica de reducción de ganancia.
7. Suelte el mando cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Qué hace cada control

| Control            | Valor predeterminado                                                                                                                                                                                                                          | Rango válido                                                                                                                                                                 |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Thresh             | −18.0 dB                                                                                                                                                                                                                                       | −60.0 a 0.0 dB                                                                                                                                                               |
| Ratio              | 3.0                                                                                                                                                                                                                                            | 1.0 a 20.0                                                                                                                                                                   |
| Attack             | 20.0 ms                                                                                                                                                                                                                                        | 0.1 a 300.0 ms                                                                                                                                                               |
| Release            | 200 ms                                                                                                                                                                                                                                         | 5 a 2000 ms                                                                                                                                                                  |
| Makeup             | 0.0 dB                                                                                                                                                                                                                                         | −12.0 a 24.0 dB                                                                                                                                                              |
| Curva de transferencia | —                                                                                                                                                                                                                                              | —                                                                                                                                                                             |
| Barra de reducción de ganancia | —                                                                                                                                                                                                                                              | 0 a 20 dB GR                                                                                                                                                                 |
| Drive              | Aumento de ganancia previo a la compresión. Empuja más señal más allá del umbral para que el compresor actúe con más fuerza, elevando la potencia promedio. Combínelo con Phase para mantener los picos limpios.                     | Se muestra únicamente en el panel flotante StripCompPanel (columna derecha). La etiqueta aparece como '+X.X dB'. La información sobre herramientas explica la reducción de PAPR #2887. |
| Phase              | Número de secciones de paso todo en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase a frecuencias escalonadas (300/700/1500/2500 Hz, más opcionalmente 1000/2000 Hz). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. | Se muestra únicamente en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Rotador de fase previo a la compresión (#2887). 0=desactivado, 4=predeterminado de radiodifusión.' |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y baje el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de knee (rodilla) y limiter (limitador), abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de knee y de techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual inmediata: si la bola nunca sale del segmento recto inferior izquierdo, el umbral está configurado por encima de su nivel de señal típico y el compresor no está actuando.
- Para ingresar valores precisos, haga clic en la etiqueta del valor debajo de cualquier mando para abrir el editor en línea. Escriba el número (con reconocimiento de configuración regional; se admite la coma como separador decimal) y presione Enter.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad de su brillo. Esto es solo un indicador visual y no afecta ningún valor guardado del mando.

## Solución de problemas

- **El mando Thresh está presente pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — La etapa del compresor aún puede estar en bypass o el motor de audio no se está ejecutando. Confirme que la etapa esté habilitada a través del widget CHAIN y que el audio esté fluyendo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Habilítela desde el widget CHAIN para restaurar el brillo completo y reactivar el procesamiento activo. El mosaico permanece visible cuando está en bypass, a diferencia de versiones anteriores donde estaba oculto.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Descripción general del Compresor Aetherial (TX) / AGC-C Aetherial (RX) ](overview.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar attack/release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
