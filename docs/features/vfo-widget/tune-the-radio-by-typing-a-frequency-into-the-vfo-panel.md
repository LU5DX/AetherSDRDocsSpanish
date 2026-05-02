# Sintonizar el radio escribiendo una frecuencia en el panel VFO

La entrada directa de frecuencia permite saltar a una frecuencia exacta sin hacer clic en el panadapter. Escriba un valor en MHz en la pantalla de frecuencia del panel VFO y presione Enter.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El panel VFO del slice de destino debe estar abierto. Si no está visible, haga clic en la bandera marcadora del VFO de ese slice en la pantalla del espectro.

## Pasos

1. Haga clic una vez en la **Frequency display**. La pantalla entra en modo de entrada directa.
2. Escriba la frecuencia deseada en MHz.
3. Presione **Enter** o **Tab** para aplicar. El slice se sintoniza inmediatamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave persistida |
|---|---|---|---|
| **Frequency display** | Muestra la frecuencia actual del slice. Haga clic una vez para iniciar la entrada directa; escriba en MHz y presione Enter o Tab para aplicar. Desplace la rueda del ratón sobre la pantalla para sintonizar hacia arriba o hacia abajo según el tamaño de paso actual. | — | — |
| **Collapse toggle** | Contrae el panel VFO a una barra compacta que muestra solo la frecuencia. En modo contraído, desplazar la rueda en cualquier lugar de la barra sintoniza según el tamaño de paso actual. | Expandido | `SliceFlagCollapsed_{N}` |

## Consejos

- Si el panel está contraído a la barra de solo frecuencia, haga clic en cualquier lugar de ella para expandirlo y acceder a la **Frequency display** para la entrada directa.
- La rueda del ratón también sintoniza el slice cuando el puntero está sobre la **Frequency display**, avanzando según el tamaño de paso actual del slice. En macOS, los eventos de desplazamiento inercial se ignoran para evitar sintonizaciones no deseadas después de terminar un gesto.

## Solución de problemas

- **Escribir no tiene efecto** — Verifique que el slice no esté bloqueado. Un slice bloqueado ignora los comandos de sintonización. Desbloquéelo antes de ingresar una frecuencia.
- **El panel VFO no está visible** — Haga clic en la bandera marcadora del VFO del slice deseado en la pantalla del espectro para abrir el panel.

## Relacionados

- [Descripción general del panel VFO](overview.md)
- [Contraer el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Cambiar el modo desde el panel VFO](change-mode-from-the-vfo-panel.md)
- [Activar el desplazamiento RIT o XIT desde el panel VFO](enable-rit-or-xit-offset-from-the-vfo-panel.md)
