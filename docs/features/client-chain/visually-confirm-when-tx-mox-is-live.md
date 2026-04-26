# Confirmar visualmente cuando TX (MOX) está activo

El applet Aetherial Audio Chain muestra un indicador rojo parpadeante en el extremo TX cada vez que su slice está transmitiendo activamente. Esto le permite confirmar de un vistazo que MOX está activo sin apartar la vista de la cadena.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja `PUDU` en la barra lateral derecha para habilitar el contenedor.
- La cadena TX debe estar visible. Haga clic en TX en el encabezado del applet si actualmente está seleccionado RX.
- Su radio debe estar conectada y un slice debe estar activo.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón de bandeja `PUDU` en la barra lateral derecha.
2. Haga clic en `TX` en el encabezado del applet para mostrar la cadena TX. El botón TX se vuelve ámbar cuando está seleccionado.
3. Active el transmisor mediante su método habitual (PTT, MOX o atajo de teclado).
4. Observe el indicador del extremo TX al final de la tira de la cadena TX. Parpadea en rojo mientras su slice está transmitiendo.
5. Suelte el transmisor. El parpadeo rojo se detiene y el indicador vuelve a su estado inactivo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado |
|---|---|---|---|
| `TX` | Botón de alternancia | Muestra y edita la cadena DSP de TX. Color ámbar cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Activado |
| `RX` | Botón de alternancia | Muestra y edita la cadena DSP de RX. Oculta el indicador del extremo TX. La última pestaña activa persiste mediante `PooDooAudioActiveTab`. | Desactivado |
| Indicador del extremo TX | Indicador | Parpadea en rojo mientras el slice activo está transmitiendo (MOX activado). Vuelve al estado inactivo cuando finaliza la transmisión. | Inactivo |

## Consejos

- El indicador del extremo TX solo es visible cuando se muestra la cadena `TX`. Cambiar a `RX` lo oculta. Si necesita supervisar el estado de TX mientras edita la configuración de RX, vuelva primero a `TX`.
- El parpadeo rojo es activado únicamente por el estado de transmisión de su propio slice. Los demás operadores en una sesión multiFLEX no lo activan.

## Relacionado

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Ver de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
