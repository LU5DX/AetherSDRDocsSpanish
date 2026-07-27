# Abrir el Editor Flotante sin Marco de una Etapa desde la Cadena

Al hacer doble clic en un mosaico de etapa dentro de la Cadena de Audio Aetherial, se abre el editor flotante sin marco de esa etapa, lo que le permite acceder directamente a sus parámetros sin salir de la disposición de la ventana principal.

**Nota:** Al hacer doble clic en un mosaico de la cadena de TX, se abre la Tira de Canal de Audio Aetherial (la ventana unificada de DSP de TX) en lugar del editor individual de esa etapa. Desde la Tira de Canal puede acceder a los controles de cada etapa. Al hacer doble clic en un mosaico de la cadena de RX, se abre directamente el editor flotante sin marco de esa etapa.

## Antes de comenzar

- El contenedor de Audio Aetherial (TXDSP) debe estar visible. Si no lo está, haga clic en el botón **PUDU** de la bandeja en la barra lateral derecha para mostrarlo.
- Decida si desea editar una etapa de TX o de RX, y asegúrese de que la cadena correcta esté activa.

## Pasos

1. Si la cadena no muestra ya el lado deseado, haga clic en **TX** o **RX** en la fila de encabezado de la Cadena de Audio Aetherial para cambiar a esa cadena.
2. Localice el mosaico de la etapa que desea editar. Los mosaicos de la cadena de TX están etiquetados como **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU** y **VERB**. Los mosaicos de la cadena de RX están etiquetados como **EQ**, **AGC-G**, **AGC-C**, **DESS**, **TUBE** y **EVO**.
3. Haga doble clic en el mosaico de la etapa:
   - En la cadena de **TX**, al hacer doble clic en cualquier mosaico de etapa se abre la Tira de Canal de Audio Aetherial. Use los controles de la propia Tira de Canal para acceder a la etapa individual que desea editar.
   - En la cadena de **RX**, al hacer doble clic en un mosaico de etapa se abre directamente el editor flotante sin marco de esa etapa.

Un solo clic pone la etapa en bypass en lugar de abrir el editor. Asegúrese de hacer doble clic.

## Función de cada control

| Control                                                                                   | Tipo          | Comportamiento                                                                                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                                                    | Botón de alternancia | Muestra la cadena de DSP de TX. Color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante `PooDooAudioActiveTab='TX'` / `'RX'`.                                                                                                                                                                                                                          |
| **RX**                                                                                    | Botón de alternancia | Muestra la cadena de DSP de RX. Color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante `PooDooAudioActiveTab='TX'` / `'RX'`.                                                                                                                                                                                                                          |
| **BYPASS**                                                                                | Botón de alternancia | Desactiva todas las etapas de la cadena seleccionada (incluyendo RN2). Haga clic de nuevo para restaurar las etapas que estaban activadas antes. El alcance es global (por motor de audio), no por perfil; el botón permanece presionado al cambiar de perfil en la Tira de Canal. TX y RX mantienen instantáneas separadas; el estado visual marcado sigue al lado que se muestra actualmente. |
| **Record** (glifo de círculo)                                                             | Botón de alternancia | Captura hasta 30 s de audio de TX posterior a PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Información sobre herramientas: 'Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off).' Oculto en modo RX. Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está activa. Parpadea en rojo mientras graba. |
| **Play** (glifo de triángulo)                                                             | Botón de alternancia | Reproduce el audio de PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita si existe una grabación y no hay una grabación en curso. Parpadea en verde mientras reproduce.                                                                                                                                                                                |
| Etapa de cadena de TX (**EQ** / **COMP** / **GATE** / **DESS** / **TUBE** / **PUDU** / **VERB**) | Mosaico de etapa | Un clic alterna bypass. Doble clic abre la Tira de Canal de Audio Aetherial (la ventana unificada de DSP de TX). Arrastrar reordena la cadena.                                                                                                                                                                                                                                          |
| Etapa de cadena de RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**)           | Mosaico de etapa | Un clic alterna bypass. Doble clic abre el editor flotante sin marco de la etapa en modo RX. Arrastrar reordena la cadena de RX independientemente de la cadena de TX. Las seis etapas están completamente implementadas. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita que se suelten elementos entre las dos tiras. |
| **RADIO** mosaico de estado                                                                | Indicador      | Libro final no interactivo del lado de RX. Se vuelve verde cuando el audio de PC (flujo SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                       |
| **ADSP** mosaico de estado / bypass                                                       | Botón de alternancia | Mosaico interactivo del lado de RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'NVFX'); vuelve a 'ADSP' cuando ninguno está activo. Un clic pone en bypass todo el clúster de NR con una instantánea en memoria; otro clic restaura el estado de NR anterior. Doble clic abre el diálogo de Configuración de AetherDSP. |
| **SPEAK** mosaico de estado                                                               | Indicador      | Libro final no interactivo del lado de RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                       |

## Consejos

- La línea de sugerencias debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" y sirve como recordatorio rápido de estas interacciones.
- Las cadenas de TX y RX son independientes. Abrir un editor en el lado de TX no afecta la cadena de RX, y viceversa.
- La última pestaña activa (**TX** o **RX**) se restaura al volver a abrir el applet, por lo que se situará en la misma cadena que estaba editando anteriormente.
- El botón **BYPASS** se mantiene sincronizado con el estado de bypass establecido desde la Tira de Canal de Audio Aetherial (TX) o directamente a través del motor de RX. Alternar el bypass desde cualquier ubicación actualiza tanto el motor como el elemento visual.
- El botón **BYPASS** funciona globalmente en el motor de audio, no por perfil. Permanece presionado incluso cuando cambia de perfil en la Tira de Canal usando el editor de TX.
- El intervalo de discriminación de clics utilizado para distinguir un solo clic de un doble clic se toma de la Configuración de Interacción, no del intervalo de doble clic del sistema, por lo que puede ajustar la sensibilidad de forma independiente.
- Los colores en la cadena (fondos, bordes, LEDs) ahora siguen el tema activo en lugar de estar codificados, por lo que la cadena se adapta a su estilo visual elegido.

## Solución de problemas

- **Un solo clic activó la acción incorrecta (el bypass se alternó en lugar de abrir el editor)** — Hizo clic una vez en lugar de dos. Haga clic en el mosaico de etapa una segunda vez, o haga un solo clic de nuevo para restaurar el estado de bypass y luego haga doble clic para abrir el editor.
- **Al hacer doble clic en un mosaico de etapa de TX se abrió la Tira de Canal en lugar del editor de esa etapa** — Este comportamiento es el esperado. El doble clic en la cadena de TX es el gesto canónico "editar mi audio de TX" y siempre abre la Tira de Canal. Use los controles de la propia Tira de Canal para navegar a la etapa específica.
- **El contenedor TXDSP no está visible, por lo que no se puede acceder a la cadena** — Haga clic en el botón **PUDU** de la bandeja en la barra lateral derecha para activar el contenedor de Audio Aetherial.
- **El estado del botón BYPASS parece inconsistente entre perfiles** — El BYPASS es una configuración global del motor de audio, no por perfil. Permanecerá activado incluso si cambia de perfil en la Tira de Canal, lo cual es intencional.

## Relacionado

- [Resumen de la Cadena de Audio Aetherial](overview.md)
- [Cambiar entre la edición de las cadenas de TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Poner en bypass todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Poner en bypass todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena de DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena de DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
