# Reproducir el audio PUDU capturado

Use el botón Play del applet PooDoo Audio Chain para escuchar una captura de audio TX post-PUDU grabada anteriormente. Esto le permite oír exactamente cómo suena su señal procesada sin transmitir.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para activarlo.
- El modo TX debe estar seleccionado (el interruptor **TX** debe estar marcado, no **RX**).
- Ya debe existir una grabación. El botón Play permanece deshabilitado hasta que se haya realizado al menos una captura. Consulte [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md).
- No debe haber una grabación en curso. El botón Play permanece deshabilitado mientras el botón Record está activo.

## Pasos

1. Confirme que el interruptor **TX** está marcado en la fila de encabezado del applet. El botón Play no funciona en modo RX.
2. Localice el botón Play (▶) a la derecha del botón Record (⏺) en la fila de encabezado del applet.
3. Haga clic en el botón Play (▶) para iniciar la reproducción. El botón pulsa en verde mientras la reproducción está activa.
4. Para detener la reproducción antes de que finalice, haga clic en el botón Play (▶) nuevamente.

## Qué hace cada control

| Control | Comportamiento | Habilitado cuando | Indicador |
|---|---|---|---|
| Play (▶) | Reproduce el audio PUDU capturado; haga clic nuevamente para cancelar. | Existe una grabación y no hay grabación activa. Durante la reproducción, permanece habilitado para que pueda cancelar. | Pulsa en verde (500 ms alternando brillante/tenue) durante la reproducción. |
| Record (⏺) | Captura hasta 30 s de audio TX post-PUDU; haga clic nuevamente para detener. La grabación se detiene y la reproducción inicia automáticamente. | La entrada MIC está lista (fuente configurada como PC, DAX desactivado) y la reproducción no está en curso. | Pulsa en rojo durante la grabación. |

## Consejos

- Si la reproducción inicia automáticamente después de detener una grabación, ese es el comportamiento esperado: detener el botón Record activa la reproducción de inmediato.
- El botón Play se deshabilita en cuanto hace clic en el botón Record para iniciar una nueva grabación. Cancele o finalice la grabación primero.

## Solución de problemas

- **El botón Play (▶) aparece en gris** — Aún no existe ninguna grabación, o hay una grabación en curso. Realice primero una grabación, o espere a que finalice la grabación actual.
- **El botón Play (▶) aparece en gris aunque se haya realizado una grabación** — Es posible que la grabación siga activa (el botón Record aún pulsa en rojo). Haga clic en el botón Record (⏺) para detener la grabación y luego haga clic en Play.

## Relacionado

- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
