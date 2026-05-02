# Habilitar el desplazamiento RIT o XIT desde el panel VFO

RIT (Receiver Incremental Tuning) y XIT (Transmitter Incremental Tuning) permiten desplazar la frecuencia de recepción o transmisión un pequeño offset sin mover el VFO principal. Esto es útil para trabajar contactos en frecuencias divididas o para compensar una estación que está ligeramente fuera de su frecuencia de sintonía.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice (canal) objetivo debe estar abierto y expandido. Si está contraído en la barra de solo frecuencia, haga clic en cualquier parte de él para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora del VFO en la pantalla del espectro correspondiente al slice que desea ajustar. El panel VFO aparece anclado al marcador.
2. Haga clic en la pestaña **X/RIT** dentro del panel VFO.
3. Para habilitar el desplazamiento de recepción, haga clic en el botón **RIT**. El botón se activa y la etiqueta muestra el offset RIT actual.
4. Para habilitar el desplazamiento de transmisión, haga clic en el botón **XIT**. El botón se activa y la etiqueta muestra el offset XIT actual.
5. Con RIT o XIT activo, coloque el puntero del mouse sobre el botón correspondiente y gire la rueda del mouse para ajustar el offset. Cada paso de la rueda cambia el offset en 10 Hz.
6. Para deshabilitar RIT o XIT, haga clic nuevamente en el botón activo.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Configuración persistente |
|---|---|---|---|---|
| Botón + etiqueta RIT | Botón de alternancia | desactivado | — | — |
| Botón + etiqueta XIT | Botón de alternancia | desactivado | — | — |

**Botones + etiquetas RIT / XIT** — Habilitan la sintonía incremental de recepción (RIT) o transmisión (XIT) para este slice. Cuando están activos, la etiqueta junto a cada botón muestra el valor del offset actual. Gire la rueda del mouse sobre el botón para ajustar el offset en pasos de 10 Hz. Ninguna de las dos configuraciones es persistente; el estado refleja el estado actual del radio.

## Consejos

- Los offsets RIT y XIT son independientes. Puede habilitar ambos al mismo tiempo para desplazar la recepción y la transmisión de forma independiente.
- El ajuste con la rueda del mouse es de 10 Hz por paso. Para offsets mayores, gire la rueda varios pasos.

## Relacionado

- [Descripción general del panel VFO](overview.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Sintonizar el radio escribiendo una frecuencia en el panel VFO](tune-the-radio-by-typing-a-frequency-into-the-vfo-panel.md)
- [Contraer el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
