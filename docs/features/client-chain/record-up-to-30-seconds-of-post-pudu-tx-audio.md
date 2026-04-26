# Grabar hasta 30 segundos de audio TX posterior a PUDU

Use el grabador de monitor integrado para capturar una muestra breve de su audio TX procesado — después de cada etapa en la cadena, incluida PUDU — para escuchar exactamente cómo suena su señal en el aire sin necesidad de un segundo receptor.

## Antes de comenzar

- El contenedor de PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU del área de notificación en la barra lateral derecha para mostrarlo.
- La entrada de micrófono debe estar configurada como fuente PC y DAX debe estar desactivado. El botón de grabación permanece deshabilitado hasta que ambas condiciones se cumplan.
- Debe estar en la vista de cadena TX. Haga clic en TX en el encabezado del applet si actualmente está seleccionado RX.

## Pasos

1. Confirme que el botón ⏺ (grabar) en el encabezado del applet está habilitado. Si aparece atenuado, revise la fuente de micrófono y el estado de DAX como se describió anteriormente.
2. Haga clic en ⏺ para iniciar la grabación. El botón parpadea en rojo mientras la captura está activa. La grabación se detiene automáticamente después de 30 segundos.
3. Para detener la grabación antes de que transcurran 30 segundos, haga clic en ⏺ nuevamente.
4. La reproducción comienza automáticamente cuando la grabación se detiene. El botón ▶ (reproducir) parpadea en verde durante la reproducción.
5. Para detener la reproducción antes de que termine, haga clic en ▶.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| ⏺ (grabar) | Inicia o detiene la captura del audio TX posterior a PUDU. La duración máxima de grabación es de 30 segundos. | Habilitado cuando la entrada de micrófono está lista y la reproducción no está activa. Parpadea en rojo durante la grabación. Deshabilitado cuando está atenuado. |
| ▶ (reproducir) | Reproduce la grabación más reciente. Haga clic nuevamente para cancelar. | Habilitado solo después de que existe una grabación y no hay ninguna grabación en curso. Parpadea en verde durante la reproducción. |

## Consejos

- No es necesario transmitir para usar el grabador; el grabador captura el audio procesado de la cadena del lado del cliente, no el audio emitido al aire.
- Si desea escuchar el efecto de una sola etapa, omita todas las demás usando BYPASS antes de grabar y luego compare una segunda grabación con BYPASS desactivado. Consulte [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md).
- El grabador captura el audio después de cada etapa en la cadena, incluido el excitador PUDU. Para escuchar la cadena sin PUDU, haga clic una sola vez en el mosaico de la etapa PUDU para omitirla antes de grabar.

## Solución de problemas

- **⏺ permanece atenuado** — La entrada de micrófono no está configurada como fuente PC, DAX está activo o hay una reproducción en curso. Desactive DAX, configure la fuente de micrófono como PC y espere a que finalice cualquier reproducción.
- **La reproducción no comienza automáticamente después de que la grabación se detiene** — No se capturó audio (por ejemplo, la grabación se detuvo de inmediato). Haga clic en ⏺ para grabar nuevamente y hable al micrófono durante la sesión.
- **▶ está atenuado después de grabar** — La grabación aún está en curso. Haga clic en ⏺ para detenerla primero.

## Relacionados

- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Descripción general de la cadena PooDoo Audio](overview.md)
