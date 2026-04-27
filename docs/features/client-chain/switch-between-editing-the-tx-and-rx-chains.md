# Cambiar entre la edición de las cadenas TX y RX

El applet Aetherial Audio Chain muestra la cadena DSP de TX o de RX, una a la vez. Use los botones de selección TX y RX para cambiar cuál cadena es visible y editable. La última selección utilizada se restaura al volver a abrir el applet.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja etiquetado PUDU en la barra lateral derecha para mostrarlo.
- La cadena TX se muestra de forma predeterminada. Si nunca ha cambiado la selección, basta con hacer clic en RX.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet Aetherial Audio Chain. Contiene los botones TX, RX y BYPASS.
2. Haga clic en TX para mostrar y editar la cadena DSP de TX (Parametric EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb).
3. Haga clic en RX para mostrar y editar la cadena DSP de RX (RX EQ, AGC-T, AGC-C, Dynamic Tube, RX PUDU), que también muestra los indicadores de estado RADIO, DSP y SPEAK.
4. El botón seleccionado se torna ámbar. La tira de cadena que aparece debajo se actualiza de inmediato para mostrar el lado elegido.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Clave persistida | Comportamiento |
|---|---|---|---|---|
| TX | Botón de selección | Activado | `PooDooAudioActiveTab` | Muestra y permite editar la cadena DSP de TX. Aparece en ámbar cuando está seleccionado. |
| RX | Botón de selección | Desactivado | `PooDooAudioActiveTab` | Muestra y permite editar la cadena DSP de RX. Aparece en ámbar cuando está seleccionado. |

TX y RX forman un par exclusivo: solo uno puede estar activo a la vez. La pestaña activa se guarda como `PooDooAudioActiveTab` con el valor `TX` o `RX`, y se restaura en el siguiente inicio.

Las cadenas TX y RX son completamente independientes: cada una tiene su propio orden de etapas, estado de bypass por etapa e instantánea de BYPASS global. Cambiar de lado no afecta el estado de la otra cadena. El orden de la cadena TX se persiste como `ClientCompTxChainStages`; el orden de la cadena RX como `ClientCompRxChainStages`.

## Consejos

- El botón BYPASS siempre actúa únicamente sobre el lado que se muestra en ese momento. Si cambia de TX a RX y hace clic en BYPASS, solo se aplica el bypass a la cadena RX; el estado de bypass de la cadena TX no se modifica.
- Los botones de monitoreo de grabación (⏺) y reproducción (▶) se ocultan cuando se selecciona RX: son funciones exclusivas de TX.
- El texto de sugerencia que aparece debajo de la tira de cadena, "Click to bypass · Double click to edit · Drag to reorder", se aplica igualmente a las cadenas TX y RX.

## Relacionado

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Aplicar bypass a todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Aplicar bypass a todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Ver de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
