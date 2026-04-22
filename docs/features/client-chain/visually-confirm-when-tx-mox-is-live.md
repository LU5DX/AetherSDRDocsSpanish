# Confirmar visualmente cuando TX (MOX) está activo

El applet PooDoo Audio Chain muestra un indicador visual cada vez que su slice está transmitiendo. Úselo para confirmar de un vistazo que MOX está activo sin apartar la vista de la tira de cadena.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón `PUDU` de la bandeja en la barra lateral derecha para mostrarlo.
- El modo TX debe estar seleccionado en el applet (TX está seleccionado de forma predeterminada).

## Pasos

1. Haga clic en el botón `PUDU` de la bandeja en la barra lateral derecha si el contenedor PooDoo Audio no está ya abierto.
2. Confirme que el botón TX en la parte superior del applet está seleccionado (muestra texto y borde de color ámbar cuando está activo). Si no lo está, haga clic en TX.
3. Active el transmisor (MOX activado). El indicador del extremo TX al final derecho de la tira de cadena pulsa en rojo mientras su slice está transmitiendo.
4. Suelte MOX. El pulso rojo se detiene y el indicador vuelve al estado inactivo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| TX | Selecciona la vista de la cadena DSP de TX; es necesario para que el indicador del extremo TX sea visible. | Activado | — |
| Indicador del extremo TX | Pulsa en rojo mientras MOX está activo en su propio slice. Vuelve al estado inactivo cuando finaliza la transmisión. | Inactivo | — |

## Consejos

- El pulso rojo es controlado por el estado MOX del radio para su propio slice. No refleja otros slices ni otros clientes conectados.
- Si el contenedor PooDoo Audio se cierra entre sesiones, AetherSDR restaura su visibilidad desde la configuración `Applet_TXDSP`.

## Solución de problemas

- **El indicador del extremo TX no pulsa en rojo durante la transmisión** — Confirme que el botón TX está seleccionado, no RX. El indicador solo es visible en modo TX. Confirme también que el contenedor PooDoo Audio está completamente expandido y no desplazado fuera de la vista.
- **La tira de cadena no es visible** — Haga clic en el botón `PUDU` de la bandeja para abrir el contenedor y luego haga clic en TX para cambiar a la vista de la cadena TX.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
