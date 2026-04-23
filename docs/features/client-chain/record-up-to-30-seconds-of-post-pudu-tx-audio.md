# Grabar hasta 30 segundos de audio TX posterior al PUDU

Use el grabador del monitor post-PUDU para capturar hasta 30 segundos de su audio TX procesado después de que pase por toda la cadena PooDoo. Esto le permite escuchar exactamente lo que produce la cadena sin necesitar un segundo receptor.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón "PUDU" de la bandeja en la barra lateral derecha para mostrarlo.
- La entrada de micrófono debe estar configurada en PC y DAX debe estar desactivado. El botón de grabación está deshabilitado si alguna de estas condiciones no se cumple.
- No debe haber reproducción en curso. El botón de grabación está deshabilitado mientras el botón Play esté activo.

## Pasos

1. En el contenedor PooDoo Audio, confirme que el botón TX está seleccionado (ámbar). El grabador del monitor opera únicamente sobre la cadena TX.
2. Haga clic en el botón Record (⏺) en la fila de encabezado, a la derecha de los botones TX y RX.
3. Transmita normalmente. El botón Record parpadea en rojo mientras captura.
4. Haga clic en el botón Record (⏺) nuevamente para detener, o permita que la grabación se detenga automáticamente a los 30 segundos. La reproducción comienza automáticamente una vez que la grabación se detiene.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| Record (⏺) | Inicia o detiene la captura de hasta 30 s de audio TX posterior al PUDU. La reproducción comienza automáticamente al detener. | Desactivado | Habilitado solo cuando la entrada de micrófono está lista y la reproducción no está en curso. Parpadea en rojo durante la grabación. |
| Play (▶) | Reproduce el audio capturado. Haga clic de nuevo para cancelar. | Desactivado | Habilitado solo cuando existe una grabación y no hay grabación activa. Parpadea en verde durante la reproducción. |

## Consejos

- El tooltip del botón Record dice: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off). Click again to stop; playback starts automatically." Si el botón aparece atenuado, verifique primero la configuración de la fuente del micrófono y el estado de DAX.
- El botón Record permanece habilitado mientras la grabación está activa, de modo que puede hacer clic en él para detener la captura en cualquier momento antes del límite de 30 segundos.
- La cadena procesa el audio independientemente de qué etapas estén omitidas. Para evaluar etapas específicas, omita las demás antes de grabar. Consulte [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md).

## Solución de problemas

- **El botón Record (⏺) está atenuado y no se puede hacer clic** — La entrada de micrófono no está configurada en PC, DAX está activado, o la reproducción está en curso. Corrija la configuración del micrófono y DAX, o espere a que finalice la reproducción.
- **La grabación se detiene antes de que termine** — El grabador captura un máximo de 30 segundos. Inicie la captura más cerca de la parte de su transmisión que desea evaluar.
- **La reproducción no comienza después de que se detiene la grabación** — La reproducción requiere una grabación completada. Si detuvo la grabación inmediatamente después de iniciarla, inténtelo de nuevo y permita al menos una captura breve antes de detener.

## Relacionados

- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Descripción general de la cadena PooDoo Audio](overview.md)
