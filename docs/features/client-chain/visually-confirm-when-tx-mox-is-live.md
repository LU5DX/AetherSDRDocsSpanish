# Confirmar visualmente cuando TX (MOX) está activo

El applet PooDoo Audio Chain muestra un indicador rojo pulsante en el extremo TX cada vez que su slice está transmitiendo. Úselo para confirmar de un vistazo que MOX está activo sin necesidad de buscar en otra parte de la interfaz.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja `PUDU` en la barra lateral derecha para mostrarlo.
- La vista TX debe estar activa. El botón `TX` en el encabezado del applet debe estar seleccionado (resaltado en ámbar). Si en cambio está seleccionado `RX`, haga clic en `TX`.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha para abrir el contenedor PooDoo Audio si aún no está visible.
2. Confirme que el botón `TX` en el encabezado del applet esté activado (texto y borde en ámbar). Si no lo está, haga clic en `TX`.
3. Active el transmisor usando MOX, PTT o VOX como lo haría normalmente.
4. Observe el indicador del extremo TX en el lado derecho de la tira de cadena. Pulsa en rojo mientras su slice está transmitiendo.
5. Suelte MOX o PTT. El pulso rojo se detiene y el indicador vuelve al estado inactivo.

## Qué hace cada control

| Control | Estados | Significado |
|---|---|---|
| Indicador del extremo TX | Inactivo, pulso rojo | Pulsa en rojo mientras usted está transmitiendo en su propio slice. Controlado por el estado MOX del radio. Vuelve al estado inactivo cuando finaliza la transmisión. |
| `TX` | Activado (ámbar), desactivado | Selecciona la vista de cadena TX. El indicador del extremo TX solo tiene significado en este modo. Valor predeterminado: activado. |
| `RX` | Activado (ámbar), desactivado | Cambia al marcador de posición de cadena RX. Valor predeterminado: desactivado. |

## Consejos

- El pulso rojo es independiente del estado `BYPASS`. Incluso si todas las etapas están en bypass, el indicador del extremo TX sigue reflejando el estado MOX en tiempo real.
- Si usa el botón Record (⏺) del monitor para capturar audio posterior a PUDU, ese botón también pulsa en rojo durante la grabación — esto es independiente del indicador del extremo TX. No confunda ambos.

## Solución de problemas

- **El indicador no pulsa al transmitir** — Confirme que el contenedor PooDoo Audio esté visible y que `TX` sea el modo activo. El indicador no se muestra en el modo `RX`.
- **El botón de bandeja PUDU no está visible** — Abra `View > Applet Panel` para asegurarse de que el panel de applets esté visible y, a continuación, localice el botón de bandeja `PUDU` en la barra lateral derecha.

## Relacionados

- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
