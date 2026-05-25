# Abrir el Editor Flotante sin Marco de una Etapa desde la Cadena

Al hacer doble clic en un mosaico de etapa dentro de la Cadena de Audio Aetherial se abre el editor flotante sin marco de esa etapa, lo que le permite acceder directamente a sus parámetros sin salir del diseño de la ventana principal.

**Nota:** Al hacer doble clic en un mosaico de la cadena TX se abre el Aetherial Audio Channel Strip (la ventana unificada de DSP de TX), en lugar del editor individual de esa etapa. Desde el Channel Strip puede acceder a los controles de cada etapa. Al hacer doble clic en un mosaico de la cadena RX se abre directamente el editor flotante sin marco de esa etapa.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para mostrarlo.
- Decida si desea editar una etapa TX o una etapa RX y asegúrese de que la cadena correcta esté activa.

## Pasos

1. Si la cadena no está mostrando el lado que desea, haga clic en **TX** o **RX** en la fila de encabezado de la Cadena de Audio Aetherial para cambiar a esa cadena.
2. Localice el mosaico de la etapa que desea editar. Los mosaicos de la cadena TX están etiquetados como **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU** y **VERB**. Los mosaicos de la cadena RX están etiquetados como **EQ**, **AGC-G**, **AGC-C**, **DESS**, **TUBE** y **EVO**.
3. Haga doble clic en el mosaico de la etapa:
   - En la cadena **TX**, al hacer doble clic en cualquier mosaico de etapa se abre el Aetherial Audio Channel Strip. Use los controles propios del Channel Strip para acceder a la etapa individual que desea editar.
   - En la cadena **RX**, al hacer doble clic en un mosaico de etapa se abre directamente el editor flotante sin marco de esa etapa.

Un solo clic desvía (bypass) la etapa en lugar de abrir el editor. Asegúrese de hacer doble clic.

## Qué hace cada control

| Control                                                                                   | Tipo          | Comportamiento                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                                                    | Botón de alternancia | Muestra la cadena DSP de TX. Color ámbar 'VUDU' cuando está seleccionado. La pestaña de última actividad se conserva mediante `PooDooAudioActiveTab='TX'` / `'RX'`.                                                                                                                                                                                                                    |
| **RX**                                                                                    | Botón de alternancia | Muestra la cadena DSP de RX. Color ámbar 'VUDU' cuando está seleccionado. La pestaña de última actividad se conserva mediante `PooDooAudioActiveTab='TX'` / `'RX'`.                                                                                                                                                                                                                    |
| **BYPASS**                                                                                | Botón de alternancia | Marcado: captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Desmarcado: reactiva solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas; el estado visual marcado sigue el lado que se muestra actualmente.                                                                              |
| **Record** (glifo de círculo)                                                             | Botón de alternancia | Captura hasta 30 s de audio TX posterior a PUDU; vuelva a hacer clic para detener (la reproducción comienza automáticamente). Tooltip: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX. Solo activo cuando la entrada del micrófono está lista y la reproducción no está en curso. Parpadea en rojo mientras graba.                    |
| **Play** (glifo de triángulo)                                                             | Botón de alternancia | Reproduce el audio PUDU capturado; vuelva a hacer clic para cancelar. Oculto en modo RX. Solo activo cuando existe una grabación y esta no está activa. Parpadea en verde mientras reproduce.                                                                                                                                                                                          |
| Etapa de cadena TX (**EQ** / **COMP** / **GATE** / **DESS** / **TUBE** / **PUDU** / **VERB**) | Mosaico de etapa | Un clic alterna el bypass. Doble clic abre el Aetherial Audio Channel Strip (la ventana de DSP unificada de TX). Arrastre para reordenar la cadena.                                                                                                                                                                                                                                    |
| Etapa de cadena RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**)           | Mosaico de etapa | Un clic alterna el bypass. Doble clic abre el editor flotante sin marco de la etapa en modo RX. Arrastre para reordenar la cadena RX de forma independiente de la cadena TX. Las seis etapas están completamente implementadas. El tipo MIME distintivo `application/x-aethersdr-rx-chain-stage` evita colocaciones accidentales entre las dos tiras.                                |
| **RADIO** mosaico de estado                                                                | Indicador     | Marcador final no interactivo del lado RX. Se vuelve verde cuando el Audio de PC (flujo SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                        |
| **ADSP** mosaico de estado / bypass                                                        | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre abreviado del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un clic desvía todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el cuadro de diálogo AetherDSP Settings. |
| **SPEAK** mosaico de estado                                                                | Indicador     | Marcador final no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                         |
## Consejos

- La línea de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y sirve como recordatorio rápido de estas interacciones.
- Las cadenas TX y RX son independientes. Abrir un editor en el lado TX no afecta la cadena RX, y viceversa.
- La pestaña de última actividad (**TX** o **RX**) se restaura al reabrir el applet, por lo que volverá a la misma cadena que estaba editando anteriormente.
- El botón **BYPASS** se mantiene sincronizado con el estado de bypass establecido desde el Aetherial Audio Channel Strip (TX) o directamente a través del motor RX. Alternar el bypass desde cualquier lugar actualiza tanto el motor como el elemento visual.
- El intervalo de discriminación de clic utilizado para distinguir clics simples de dobles clics se toma de la configuración de Interacción (Interaction Settings) en lugar del intervalo de doble clic del sistema, por lo que puede ajustar la sensibilidad de forma independiente.

## Solución de problemas

- **Un solo clic realizó la acción incorrecta (se activó el bypass en lugar de abrir el editor)** — Hizo clic una vez en lugar de dos. Haga clic en el mosaico de la etapa una segunda vez, o haga un solo clic de nuevo para restaurar el estado de bypass, luego haga doble clic para abrir el editor.
- **Al hacer doble clic en un mosaico de etapa TX se abrió el Channel Strip en lugar del editor de esa etapa** — Este es el comportamiento esperado. El doble clic en la cadena TX es el gesto canónico "editar mi audio TX" y siempre abre el Channel Strip. Use los controles propios del Channel Strip para navegar a la etapa específica.
- **El contenedor TXDSP no está visible, por lo que no se puede acceder a la cadena** — Haga clic en el botón de la bandeja **PUDU** en la barra lateral derecha para activar/desactivar la visualización del contenedor Aetherial Audio.

## Relacionado

- [Aetherial Audio Chain overview](overview.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Reorder the RX DSP chain (independent of TX order)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
