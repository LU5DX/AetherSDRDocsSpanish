# Cambiar entre la edición de las cadenas TX y RX

El applet Aetherial Audio Chain muestra la cadena DSP de TX o de RX de una vez. Use los botones de alternancia TX y RX para seleccionar cuál cadena es visible y editable. La última selección realizada se restaura al volver a abrir AetherSDR.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar abierto. Si no está visible, haga clic en el botón de bandeja etiquetado PUDU en la barra lateral derecha para mostrarlo.
- Ambas cadenas están disponibles sin una conexión de radio.

## Pasos

1. Ubique la fila de encabezado en la parte superior del applet Aetherial Audio Chain. Contiene dos botones de modo: TX y RX.
2. Haga clic en TX para mostrar y editar la cadena DSP de TX (Parametric EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb).
3. Haga clic en RX para mostrar y editar la cadena DSP de RX (RX EQ, AGC-T, AGC-C, Dynamic Tube, RX PUDU), junto con los indicadores de estado RADIO, DSP y SPEAK.
4. El botón seleccionado se torna ámbar. La cadena visible anteriormente se oculta y la cadena recién seleccionada aparece en su lugar.

Su selección persiste entre sesiones mediante `PooDooAudioActiveTab`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Configuración persistente |
|---|---|---|---|---|
| TX | Botón de alternancia | Activado | Muestra y habilita la edición de la cadena DSP de TX. Ámbar cuando está seleccionado. | `PooDooAudioActiveTab` = `TX` |
| RX | Botón de alternancia | Desactivado | Muestra y habilita la edición de la cadena DSP de RX. Ámbar cuando está seleccionado. | `PooDooAudioActiveTab` = `RX` |

TX y RX forman un par exclusivo: solo uno puede estar seleccionado a la vez. Cada lado mantiene su propio estado de etapa, orden de cadena e instantánea de BYPASS de manera independiente. El orden de etapas en la cadena TX (`ClientCompTxChainStages`) no tiene efecto sobre el orden de la cadena RX (`ClientCompRxChainStages`), y viceversa.

## Sugerencias

- El botón BYPASS actúa siempre sobre la cadena que esté visible en ese momento. Verifique qué modo está activo antes de activar BYPASS para evitar silenciar la cadena incorrecta.
- Los botones de monitoreo Record y Play son visibles solo en el modo TX; se ocultan cuando RX está seleccionado.
- El texto de ayuda debajo de la tira de la cadena — "Click to bypass · Double click to edit · Drag to reorder" — aplica tanto para el modo TX como para el modo RX.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Ver de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (indicadores de estado de RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
