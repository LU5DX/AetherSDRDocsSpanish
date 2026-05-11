# Abrir el Editor Flotante Sin Marco de una Etapa desde la Cadena

Al hacer doble clic en un mosaico de etapa en la Cadena de Audio Aetherial, se abre el editor flotante sin marco de esa etapa, brindándole acceso directo a sus parámetros sin salir de la disposición de la ventana principal.

**Nota:** Al hacer doble clic en un mosaico de la cadena TX se abre el Canal de Audio Aetherial (la ventana DSP de TX unificada) en lugar del editor individual de esa etapa. Desde el Canal de Audio puede acceder a los controles de cada etapa. Al hacer doble clic en un mosaico de la cadena RX se abre directamente el editor flotante sin marco de esa etapa.

## Antes de comenzar

- El contenedor de Audio Aetherial (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para mostrarlo.
- Decida si desea editar una etapa TX o una etapa RX, y asegúrese de que la cadena correcta esté activa.

## Pasos

1. Si la cadena aún no muestra el lado que desea, haga clic en **TX** o **RX** en la fila de encabezado de la Cadena de Audio Aetherial para cambiar a esa cadena.
2. Localice el mosaico de etapa que desea editar. Los mosaicos de la cadena TX están etiquetados como **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU** y **VERB**. Los mosaicos de la cadena RX están etiquetados como **EQ**, **AGC-G**, **AGC-C**, **DESS**, **TUBE** y **EVO**.
3. Haga doble clic en el mosaico de etapa:
   - En la cadena **TX**, al hacer doble clic en cualquier mosaico de etapa se abre el Canal de Audio Aetherial. Utilice los controles del Canal de Audio para acceder a la etapa individual que desea editar.
   - En la cadena **RX**, al hacer doble clic en un mosaico de etapa se abre directamente el editor flotante sin marco de esa etapa.

Un solo clic omite la etapa en lugar de abrir el editor. Asegúrese de hacer doble clic.

## Qué hace cada control

| Control                                                                                   | Tipo           | Comportamiento                                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------------------------------------------------------------------------|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                                                    | Botón de alternancia | Muestra la cadena DSP de TX. Color ámbar 'PooDoo' cuando está seleccionado. La pestaña de la última actividad persiste.                                                                                                                                                                                                                                                                 |
| **RX**                                                                                    | Botón de alternancia | Muestra la cadena DSP de RX. Color ámbar 'PooDoo' cuando está seleccionado. La pestaña de la última actividad persiste.                                                                                                                                                                                                                                                                 |
| **BYPASS**                                                                                | Botón de alternancia | Marcado: captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Desmarcado: reactiva solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas: el estado visual marcado sigue el lado que se muestra actualmente.                                                                                |
| **Record** (glifo de círculo)                                                             | Botón de alternancia | Captura hasta 30 s de audio TX posterior a PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)'. Oculto en modo RX. Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo mientras graba. |
| **Play** (glifo de triángulo)                                                             | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita cuando existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce.                                                                                                                                                                                |
| Etapa de cadena TX (**EQ** / **COMP** / **GATE** / **DESS** / **TUBE** / **PUDU** / **VERB**) | Mosaico de etapa | Un clic alterna la omisión. Doble clic abre el Canal de Audio Aetherial (la ventana DSP de TX unificada). Arrastre para reordenar la cadena.                                                                                                                                                                                                                                            |
| Etapa de cadena RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**)       | Mosaico de etapa | Un clic alterna la omisión. Doble clic abre el editor flotante sin marco de la etapa en modo RX. Arrastre para reordenar la cadena RX de forma independiente de la cadena TX. Las seis etapas están completamente implementadas.                                                                                                                                                          |
| **RADIO** mosaico de estado                                                               | Indicador       | Extremo no interactivo del lado RX. Se vuelve verde cuando el Audio de PC (flujo SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                                |
| **ADSP** mosaico de estado/omisión                                                        | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un clic omite todo el grupo de NR con una instantánea en memoria; otro clic restablece el estado de NR anterior. Doble clic abre el diálogo de Configuración de AetherDSP. |
| **SPEAK** mosaico de estado                                                              | Indicador       | Extremo no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                                 |
## Consejos

- La línea de sugerencia debajo de la cadena muestra "Click to bypass · Double click to edit · Drag to reorder" y sirve como recordatorio rápido de estas interacciones.
- Las cadenas TX y RX son independientes. Abrir un editor en el lado TX no afecta a la cadena RX, y viceversa.
- La pestaña de la última actividad (**TX** o **RX**) se restaura al volver a abrir el applet, por lo que llegará a la misma cadena que estaba editando anteriormente.
- El botón **BYPASS** se mantiene sincronizado con el estado de omisión establecido desde el Canal de Audio Aetherial (TX) o directamente a través del motor RX. Alternar la omisión desde cualquier ubicación actualiza tanto el motor como el indicador visual.

## Solución de problemas

- **Un solo clic activó la acción incorrecta (se alternó la omisión en lugar de abrir el editor)** — Hizo clic una vez en lugar de dos. Haga clic en el mosaico de etapa una segunda vez, o haga un solo clic de nuevo para restaurar el estado de omisión y luego haga doble clic para abrir el editor.
- **Al hacer doble clic en un mosaico de etapa TX se abrió el Canal de Audio en lugar del editor de esa etapa** — Este comportamiento es el esperado. El doble clic en la cadena TX es el gesto canónico para "editar mi audio TX" y siempre abre el Canal de Audio. Utilice los controles del Canal de Audio para navegar a la etapa específica.
- **El contenedor TXDSP no está visible, por lo que no se puede acceder a la cadena** — Haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para activar el contenedor de Audio Aetherial.

## Relacionados

- [Descripción general de la Cadena de Audio Aetherial](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
