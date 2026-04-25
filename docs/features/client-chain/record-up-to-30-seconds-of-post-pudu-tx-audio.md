# Grabar hasta 30 segundos de audio TX post-PUDU

La cadena de audio PooDoo incluye un grabador de monitoreo que captura hasta 30 segundos de audio tomado después de la etapa PUDU. Úselo para verificar cómo suena su cadena DSP en el aire sin necesidad de un segundo receptor.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- La entrada de micrófono debe estar configurada en PC y DAX debe estar desactivado. El botón de grabación está deshabilitado cuando estas condiciones no se cumplen.
- No inicie una grabación mientras se reproduzca una grabación anterior. El botón de grabación está deshabilitado durante la reproducción.

## Pasos

1. Confirme que el botón TX en la parte superior de la cadena de audio PooDoo esté seleccionado. El grabador solo es accesible en modo TX.
2. Haga clic en el botón Record (⏺) en la fila de encabezado, a la derecha de los botones TX y RX. El botón parpadea en rojo mientras la grabación está activa.
3. Hable al micrófono con normalidad. El grabador captura hasta 30 segundos de audio post-PUDU.
4. Haga clic en el botón Record (⏺) nuevamente para detener antes de los 30 segundos, o espere a que el grabador se detenga automáticamente al alcanzar el límite de 30 segundos. La reproducción comienza automáticamente cuando se detiene la grabación.

## Qué hace cada control

| Control | Comportamiento | Habilitado cuando | Estado visual |
|---|---|---|---|
| Record (⏺) | Inicia la captura de audio TX post-PUDU; haga clic nuevamente para detener antes de tiempo. | La entrada de micrófono está lista (PC, DAX desactivado) y la reproducción no está en curso. También habilitado durante la grabación (para poder detenerla). | Parpadea en rojo en intervalos de 500 ms durante la grabación. |
| Play (▶) | Reproduce el audio capturado; haga clic nuevamente para cancelar. | Existe una grabación y la grabación no está activa. También habilitado durante la reproducción (para poder cancelarla). | Parpadea en verde en intervalos de 500 ms durante la reproducción. |

## Consejos

- El límite de 30 segundos es fijo. Si solo necesita verificar una frase corta, haga clic en Record (⏺) nuevamente en cuanto termine de hablar, en lugar de esperar la detención automática.
- El grabador captura el audio después de la etapa PUDU, por lo que refleja el efecto completo de cada etapa habilitada en la cadena, en el orden actual.
- Si desea comparar la cadena habilitada frente a la omitida, grabe un fragmento, luego haga clic en BYPASS y grabe nuevamente.

## Solución de problemas

- **Record (⏺) aparece en gris** — DAX está activo, la entrada de micrófono no está configurada en PC, o la reproducción está en curso. Desactive DAX, configure la entrada de micrófono en PC y espere a que finalice cualquier reproducción activa.
- **La reproducción no comienza automáticamente después de detener la grabación** — Es posible que la grabación se haya detenido antes de capturar audio. Asegúrese de estar hablando al micrófono mientras el botón parpadea en rojo.
- **Record (⏺) aparece en gris aunque MIC esté configurado en PC y DAX esté desactivado** — Confirme que el botón TX esté seleccionado en la parte superior de la cadena. El grabador no está activo en modo RX.

## Relacionado

- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Descripción general de la cadena de audio PooDoo](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
