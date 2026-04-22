# Grabar hasta 30 segundos de audio TX posterior a PUDU

Use el grabador del monitor en la cadena PooDoo Audio para capturar hasta 30 segundos de su audio TX procesado después de que haya pasado por todas las etapas, incluida PUDU. Esto le permite escuchar exactamente cómo suena su señal antes de transmitir al aire.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja "PUDU" en la barra lateral derecha para mostrarlo.
- La fuente de entrada del micrófono debe estar configurada en PC y DAX debe estar desactivado. El botón de grabación permanece deshabilitado hasta que se cumplan ambas condiciones.
- Debe estar en la vista de cadena TX. Haga clic en "TX" si actualmente está seleccionado "RX".

## Pasos

1. Confirme que el botón "TX" está seleccionado en el encabezado de la cadena PooDoo Audio. El botón es de color ámbar cuando está activo.
2. Localice el botón de grabación (⏺) en la fila del encabezado, a la derecha de los botones "TX" y "RX". Solo está habilitado cuando la entrada del micrófono está lista.
3. Haga clic en ⏺ para iniciar la grabación. El botón pulsa en rojo y su fondo se ilumina para confirmar que la captura está activa. La grabación se detiene automáticamente después de 30 segundos.
4. Para detener antes de los 30 segundos, haga clic en ⏺ nuevamente.
5. La reproducción comienza automáticamente cuando se detiene la grabación. El botón de reproducción (▶) pulsa en verde durante la reproducción.
6. Para reproducir el audio capturado manualmente, haga clic en ▶. Para cancelar una reproducción en curso, haga clic en ▶ nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| ⏺ (grabar) | Captura hasta 30 s de audio TX posterior a PUDU. Haga clic nuevamente para detener antes; la reproducción comienza automáticamente. | Sin marcar | Habilitado solo cuando la fuente del micrófono es PC, DAX está desactivado y la reproducción no está en curso. Deshabilitado cuando no existe ninguna grabación y las condiciones no se cumplen. Pulsa en rojo durante la grabación. |
| ▶ (reproducir) | Reproduce el audio capturado. Haga clic nuevamente para cancelar. | Sin marcar | Habilitado solo cuando existe una grabación y la grabación no está activa. Pulsa en verde durante la reproducción. |

Configuraciones persistentes involucradas: `ClientCompTxChainStages`, `Applet_TXDSP`.

## Consejos

- Si desea escuchar el efecto de una etapa específica, omita las demás etapas haciendo clic simple en cada etapa de la cadena antes de grabar y, luego, compare los resultados.
- El botón de grabación permanece habilitado durante la grabación, por lo que puede hacer clic en él para detenerla en cualquier momento.
- El botón de reproducción permanece habilitado durante la reproducción, por lo que puede cancelarla en cualquier momento.

## Solución de problemas

- **⏺ aparece en gris y no se puede hacer clic** — La fuente de entrada del micrófono no está configurada en PC, DAX está activado o la reproducción está en curso. Verifique la configuración de su fuente de audio y asegúrese de que DAX esté desactivado.
- **La reproducción no comienza después de que se detiene la grabación** — No se capturó audio o la grabación fue demasiado corta. Verifique que el audio esté llegando a la cadena y que MOX haya estado activo durante la grabación.

## Relacionados

- [Descripción general de la cadena PooDoo Audio](overview.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
