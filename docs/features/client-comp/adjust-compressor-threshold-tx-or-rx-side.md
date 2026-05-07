# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo establecer el nivel de umbral en el que el Compresor Aetherial (TX) o el AGC-C Aetherial (RX) comienza a actuar. Reducir el umbral hace que el compresor se active antes y afecte a una mayor parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero atenuado aproximadamente al 55% de opacidad. Consulte [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado o si necesita reactivar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Busque el control **Thresh** en la fila de cinco controles en la parte inferior del mosaico.
3. Haga clic y arrastre el control **Thresh** hacia arriba para aumentar el umbral o hacia abajo para reducirlo. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Observe la curva de transferencia y la bola de envolvente sobre la fila de controles. Al ajustar el umbral, el punto de rodilla en la curva se desplaza y la posición de la bola en relación con la curva cambia para reflejar dónde cae el nivel de señal actual.
5. Observe la barra de reducción de ganancia. Un relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en −6 dB indica una cantidad típica de reducción de ganancia de trabajo.
6. Suelte el control cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` | Establece el nivel de entrada por encima del cual comienza la compresión. Valores más bajos activan el compresor antes. El mapeo es lineal. |
| Curva de transferencia | — | — | — | Visualización solo de la relación ganancia entrada/salida. La bola de envolvente en vivo muestra dónde se ubica la señal actual en la curva. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. Muestra cuánta atenuación está aplicando el compresor en este momento. La marca es −6 dB. |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y reduzca el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de rodilla y limitador, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de rodilla y techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual inmediata: si la bola nunca sale del segmento recto inferior izquierdo, el umbral está configurado por encima de su nivel de señal típico y el compresor no está actuando.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad del brillo. Esto es solo un indicador visual y no afecta ningún valor guardado de los controles.

## Solución de problemas

- **El control Thresh está presente pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — Es posible que la etapa del compresor todavía esté en bypass, o que el motor de audio no esté funcionando. Confirme que la etapa esté habilitada a través del widget CHAIN y que el audio esté fluyendo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Actívela desde el widget CHAIN para restaurar el brillo completo y restablecer el procesamiento activo. El mosaico permanece visible mientras está en bypass, a diferencia de versiones anteriores donde estaba oculto.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ajustar la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Ajustar ataque / liberación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
