# Reproducir el audio PUDU capturado

Esta página explica cómo reproducir el audio que grabó con el monitor TX posterior al PUDU. Utilice esta función para escuchar cómo suena su señal TX después de que la cadena DSP completa del lado del cliente la haya procesado.

## Antes de comenzar

- Debe tener al menos una grabación ya capturada. El botón Play está desactivado hasta que exista una grabación.
- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón "PUDU" de la bandeja en la barra lateral derecha para mostrarlo.
- Asegúrese de no estar grabando en este momento. El botón Play está desactivado mientras la grabación está activa.
- La cadena TX debe estar visible. El botón Play se oculta cuando la cadena RX está activa.

## Pasos

1. Si la cadena RX está visible en este momento, haga clic en **TX** para cambiar a la cadena TX.
2. Localice el botón **Play (símbolo de triángulo)** en la fila de encabezado, a la derecha del botón **Record (símbolo de círculo)**.
3. Haga clic en **Play (símbolo de triángulo)** para iniciar la reproducción. El botón parpadea en verde mientras el audio se está reproduciendo.
4. Para detener la reproducción antes de que finalice, haga clic en **Play (símbolo de triángulo)** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Play (símbolo de triángulo)** | Inicia la reproducción del audio PUDU capturado. Haga clic nuevamente para cancelar. | Activado solo cuando existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. Se oculta cuando la cadena RX está visible. |
| **Record (símbolo de círculo)** | Desactivado durante la reproducción. | Se reactiva automáticamente cuando la reproducción finaliza. |

## Consejos

- La reproducción comienza inmediatamente al hacer clic en **Play (símbolo de triángulo)**; no hay ningún paso de confirmación.
- Si desea realizar una nueva grabación primero, espere a que la reproducción finalice o cancélela, y luego use **Record (símbolo de círculo)**.
- El parpadeo verde del botón **Play (símbolo de triángulo)** alterna entre brillante y tenue cada 500 ms mientras la reproducción está en curso, lo que proporciona una indicación visual clara de que el audio está en progreso.

## Solución de problemas

- **Play (símbolo de triángulo) aparece en gris** — Aún no se ha realizado ninguna grabación, o la grabación está activa en este momento. Complete o detenga la grabación primero.
- **Play (símbolo de triángulo) no está visible** — La cadena RX está visible en este momento. Haga clic en **TX** para cambiar a la cadena TX; los botones de reproducción y grabación solo aparecen en el modo TX.

## Temas relacionados

- [Grabar hasta 30 segundos de audio TX posterior al PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
