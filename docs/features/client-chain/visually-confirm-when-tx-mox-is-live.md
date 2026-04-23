# Confirmar visualmente cuando TX (MOX) está activo

El applet PooDoo Audio Chain incluye un indicador de punto final TX que parpadea en rojo cada vez que su slice está transmitiendo. Esto le permite confirmar de un vistazo que MOX está activo sin apartar la vista de la cadena.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar abierto. Si no está visible, haga clic en el botón de bandeja PUDU en la barra lateral derecha para mostrarlo.
- El modo TX debe estar seleccionado en el applet. El botón TX debe estar marcado (ámbar). Si no lo está, haga clic en TX.
- Su radio debe estar conectada.

## Pasos

1. Abra el contenedor PooDoo Audio haciendo clic en el botón de bandeja PUDU en la barra lateral derecha.
2. Confirme que el botón TX en la parte superior del applet está marcado. Si no lo está, haga clic en TX.
3. Active su transmisor (PTT, MOX o VOX).
4. Observe el indicador de punto final TX en la tira de la cadena. Parpadea en rojo mientras su slice está transmitiendo.
5. Suelte PTT. El parpadeo rojo se detiene y el indicador vuelve al estado inactivo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de ajuste |
|---|---|---|---|
| TX | Selecciona la vista de cadena TX; necesario para que el indicador de punto final TX sea visible | Marcado | — |
| RX | Cambia a la vista de marcador de posición RX; el indicador de punto final TX no se muestra | Desmarcado | — |
| Indicador de punto final TX | Parpadea en rojo mientras la radio transmite en su slice (controlado por el estado de MOX) | Inactivo | — |

## Consejos

- El parpadeo rojo es controlado directamente por el estado de MOX. Refleja la actividad de transmisión real en su slice, no solo una pulsación del botón PTT.
- Si BYPASS está marcado mientras transmite, el indicador sigue parpadeando en rojo. El indicador de punto final TX es independiente del estado de BYPASS.
- El botón TX utiliza un resaltado ámbar cuando está seleccionado. Si el encabezado del applet muestra RX resaltado en su lugar, haga clic primero en TX — el indicador de punto final solo está presente en el modo TX.

## Solución de problemas

- **El indicador no parpadea en rojo al transmitir** — Confirme que el botón TX está marcado, no RX. El indicador no se muestra en el modo RX.
- **El botón de bandeja PUDU no está visible** — Abra el panel de applets mediante View > Applet Panel, luego localice el botón de bandeja PUDU en la barra lateral derecha.
- **El applet no muestra tira de cadena, solo un marcador de posición** — El botón RX está seleccionado. Haga clic en TX para volver a la vista de cadena TX.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
