# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo establecer el nivel de umbral en el que el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) comienza a actuar. Reducir el umbral hace que el compresor se active antes y afecte a una mayor parte de la señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Una etapa en bypass oculta el mosaico del applet. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico no es visible.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o el subcontenedor **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Encuentre el control **Thresh** en la fila de cinco mandos en la parte inferior del mosaico.
3. Haga clic y arrastre el control **Thresh** hacia arriba para elevar el umbral o hacia abajo para reducirlo. La etiqueta debajo del mando se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Observe la curva de transferencia y la esfera de envolvente sobre la fila de mandos. Al ajustar el umbral, el punto de rodilla en la curva se desplaza y la posición de la esfera con respecto a la curva cambia para reflejar dónde se encuentra el nivel de señal actual.
5. Observe la barra de reducción de ganancia. El relleno ámbar que aparece desde la derecha indica compresión activa. Una marca de referencia en −6 dB indica una cantidad de reducción de ganancia típica en operación.
6. Suelte el mando cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` | Establece el nivel de entrada por encima del cual comienza la compresión. Los valores más bajos activan el compresor antes. El mapeo es lineal. |
| Curva de transferencia | — | — | — | Visualización de solo lectura de la relación de ganancia entrada/salida. La esfera de envolvente en tiempo real muestra dónde se encuentra la señal actual en la curva. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. Muestra cuánta atenuación está aplicando el compresor en ese momento. Las marcas de referencia indican −6 dB. |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y reduzca el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX), hasta que la barra de reducción de ganancia muestre algunos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de rodilla y limitador, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de rodilla y techo del limitador solo están disponibles allí.
- La esfera de envolvente en la curva de transferencia proporciona retroalimentación visual inmediata: si la esfera nunca abandona el segmento recto inferior izquierdo, el umbral está configurado por encima del nivel de señal típico y el compresor no está actuando.

## Solución de problemas

- **El mando Thresh está presente, pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — La etapa del compresor puede seguir en bypass o el motor de audio no está en funcionamiento. Confirme que la etapa está habilitada mediante el widget CHAIN y que el audio está fluyendo.
- **El mosaico del applet no es visible** — La etapa está en bypass o el contenedor principal Aetherial Audio (TXDSP) está contraído. Habilite el compresor desde el widget CHAIN; el mosaico aparecerá automáticamente.

## Relacionado

- [Descripción general del Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Configurar la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar el ataque y la liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Supervisar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
