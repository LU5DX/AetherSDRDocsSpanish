# Reordenar la cadena DSP de RX (independiente del orden de TX)

Esta página explica cómo arrastrar las etapas DSP de RX a un nuevo orden dentro del applet Aetherial Audio Chain. El orden de la cadena RX se almacena y se aplica de forma independiente respecto a la cadena TX.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como "PUDU" en el panel del applet para mostrarlo.
- La tira de la cadena RX debe estar activa. Si actualmente se muestra la cadena TX, cambie primero a RX (consulte [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)).

## Pasos

1. En la fila de encabezado de Aetherial Audio Chain, haga clic en "RX" para mostrar la tira de la cadena RX. El botón RX se vuelve ámbar cuando está seleccionado.
2. Localice la etapa que desea mover. La cadena RX contiene hasta cinco etapas: EQ, GATE, COMP, TUBE y PUDU, delimitadas en sus extremos por los mosaicos de estado no interactivos RADIO, DSP y SPEAK.
3. Haga clic y mantenga presionado el mosaico de etapa que desea reordenar.
4. Arrástrelo hacia la izquierda o hacia la derecha a lo largo de la tira de la cadena. Aparece una barra vertical de color cian entre los mosaicos para indicar dónde se colocará la etapa.
5. Suelte para depositar la etapa en la nueva posición. La cadena se reordena de inmediato y el nuevo orden se guarda en `ClientCompRxChainStages`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave persistida |
|---|---|---|---|
| RX | Botón de alternancia | Muestra la tira de la cadena RX; se convierte en el lado activo para arrastrar y reordenar, omitir y editar. Predeterminado: sin marcar. | `PooDooAudioActiveTab` |
| Etapa de la cadena RX (EQ / GATE / COMP / TUBE / PUDU) | Controlador de arrastre | Un clic activa o desactiva la omisión (bypass); doble clic abre el editor sin marco; arrastrar reordena la cadena. | `ClientCompRxChainStages` |
| Mosaico de estado RADIO | Indicador | Extremo izquierdo no interactivo; se pone en verde cuando PC Audio está habilitado. No se puede arrastrar. | — |
| Mosaico de estado DSP | Indicador | Mosaico no interactivo que muestra el nombre corto del reductor de ruido activo (p. ej. NR2, NR4, BNR) o el genérico "DSP". No se puede arrastrar. | — |
| Mosaico de estado SPEAK | Indicador | Extremo derecho no interactivo; se pone en verde cuando la salida de audio de AetherSDR está sin silenciar. No se puede arrastrar. | — |

## Consejos

- El texto de ayuda debajo de la cadena indica "Click to bypass · Double click to edit · Drag to reorder" y se aplica tanto al modo TX como al modo RX.
- La cadena RX utiliza internamente un tipo de arrastrar y soltar distinto, por lo que las etapas no pueden depositarse accidentalmente en la tira de la cadena TX, ni viceversa.
- Cambiar a TX con "TX" y reordenar allí no afecta el orden guardado de RX. Las dos cadenas mantienen secuencias de etapas independientes.

## Solución de problemas

- **Arrastrar una etapa no tiene efecto** — Confirme que el botón "RX" esté marcado (ámbar). Si la tira de la cadena TX está visible, los depósitos son ignorados por la cadena RX.
- **Los mosaicos RADIO, DSP o SPEAK se mueven de forma inesperada** — Estos mosaicos son indicadores de estado y no se pueden arrastrar. Solo los cinco mosaicos de etapa con nombre (EQ, GATE, COMP, TUBE, PUDU) pueden reordenarse.
- **La cadena reordenada vuelve al orden anterior tras reiniciar** — Esto no debería ocurrir si `ClientCompRxChainStages` se está escribiendo correctamente. Verifique que AetherSDR tenga acceso de escritura a la ubicación de almacenamiento de su configuración.

## Relacionados

- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Ver de un vistazo si PC Audio, el reductor de ruido y la salida de audio están activos (mosaicos de estado de RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
