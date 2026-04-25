# Confirmar visualmente cuando TX (MOX) está activo

El applet PooDoo Audio Chain incluye un indicador de punto final TX que pulsa en rojo cuando su slice está transmitiendo. Esta página explica dónde encontrarlo y cómo se ve.

## Antes de comenzar

- El applet PooDoo Audio debe estar visible. Si no lo está, haga clic en el botón de bandeja **PUDU** en la barra lateral derecha para abrir el contenedor PooDoo Audio.
- El botón de modo **TX** debe estar seleccionado (está seleccionado por defecto). El indicador de punto final TX no está activo en modo RX.

## Pasos

1. Abra el contenedor PooDoo Audio haciendo clic en el botón de bandeja **PUDU** en la barra lateral derecha.
2. Confirme que el botón **TX** en la parte superior del applet está marcado. Cuando está marcado, se muestra en color ámbar.
3. Active su transmisor (MOX activado). El indicador de punto final TX en la tira de cadena pulsa en rojo mientras su slice está transmitiendo.
4. Suelte MOX. El pulso rojo se detiene y el indicador vuelve a su estado inactivo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **TX** | Selecciona la vista de cadena DSP de TX. Debe estar activo para que el indicador de punto final TX refleje el estado de transmisión. | Marcado (ámbar) | — |
| Indicador de punto final TX | Pulsa en rojo mientras el usuario transmite en su propio slice. Vuelve al estado inactivo cuando se suelta MOX. | Inactivo | — |

## Consejos

- El botón **TX** usa el color ámbar de PooDoo cuando está marcado, por lo que puede confirmar de un vistazo que está viendo la cadena TX antes de transmitir.
- El indicador de punto final TX es independiente del estado del botón **BYPASS**. El indicador sigue pulsando en rojo durante la transmisión incluso cuando todas las etapas están desactivadas (bypass).

## Relacionado

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Desactivar todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Alternar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
