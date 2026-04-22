# Reproducir el audio PUDU capturado

Use el botón Play del applet PooDoo Audio Chain para escuchar el audio que ya ha grabado a través del monitor post-PUDU. Esto le permite evaluar cómo suena su cadena TX DSP sin necesidad de transmitir.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU del panel lateral derecho para habilitarlo.
- Debe haber capturado previamente una grabación usando el botón Record. El botón Play permanece deshabilitado hasta que exista una grabación.
- La grabación no debe estar activa cuando inicie la reproducción.

## Pasos

1. Abra el applet PooDoo Audio Chain haciendo clic en el botón PUDU del panel lateral derecho.
2. Confirme que TX está seleccionado (el botón de alternancia TX aparece marcado en ámbar). Los botones del monitor solo están activos en modo TX.
3. Haga clic en el botón Play (▶) en la fila de encabezado del applet.
4. El botón Play pulsa en verde mientras se ejecuta la reproducción. Para detenerla antes de que finalice la grabación, haga clic en el botón Play (▶) nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| Play (▶) | Inicia la reproducción del audio PUDU capturado; haga clic de nuevo para cancelar. | Sin marcar | Habilitado solo cuando existe una grabación y la grabación no está activa. Pulsa en verde durante la reproducción. |
| Record (⏺) | Deshabilitado durante la reproducción. | Sin marcar | Vuelve a estar disponible una vez que la reproducción se detiene. |

## Consejos

- Si la reproducción comienza inmediatamente después de que se detiene la grabación, es porque el botón Record activa automáticamente la reproducción al detener la grabación. En ese caso, no es necesario hacer clic en Play (▶) por separado.
- El botón Play (▶) permanece habilitado mientras la reproducción está en curso, de modo que puede cancelarla en cualquier momento haciendo clic en él nuevamente.

## Solución de problemas

- **Play (▶) aparece en gris** — Aún no se ha capturado ninguna grabación, o la grabación está actualmente activa. Complete una grabación primero y luego haga clic en Play (▶).
- **Play (▶) aparece en gris incluso después de grabar** — Confirme que la grabación se ha detenido por completo (el botón Record (⏺) ya no pulsa en rojo) antes de intentar la reproducción.

## Temas relacionados

- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
