# Reordenar la cadena DSP de TX

Arrastre las etapas de la cadena DSP de TX a un orden diferente para cambiar la secuencia en la que se procesa su audio antes de la transmisión. El nuevo orden se guarda automáticamente y persiste entre reinicios.

## Antes de comenzar

- El contenedor Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena de TX debe ser el lado activo. Si el botón **RX** está actualmente seleccionado, haga clic primero en **TX**.

## Pasos

1. Abra el contenedor Aetherial Audio Chain haciendo clic en el botón de bandeja **PUDU** si aún no está visible.
2. Haga clic en **TX** en la fila del encabezado para asegurarse de que se muestre la cadena de TX.
3. Localice la etapa que desea mover. La cadena de TX contiene estas etapas: **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU**, **VERB**.
4. Mantenga presionado el mosaico de la etapa que desea mover, luego arrástrelo hacia la izquierda o la derecha a lo largo de la tira de la cadena.
5. Aparece una barra cian vertical entre los mosaicos mientras arrastra, que muestra dónde se colocará la etapa.
6. Suelte el botón del ratón para soltar la etapa en la nueva posición.
7. Repita para cualquier otra etapa que desee reordenar.

El nuevo orden de la cadena se guarda automáticamente en `ClientCompTxChainStages`.

## Qué hace cada control

| Control                                                                                                                                             | Tipo          | Comportamiento                                                                                                                                                                                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                                                                                                              | Botón de alternancia | Muestra y permite la edición de la cadena DSP de TX. Debe estar seleccionado para arrastrar etapas de TX. Color ámbar "PooDoo" cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab`.                                                                                                                  |
| **RX**                                                                                                                                              | Botón de alternancia | Cambia la tira a la cadena de RX. Las operaciones de arrastre en la tira de RX no afectan el orden de TX. Cada lado mantiene el estado independiente de las etapas, el orden de la cadena y la instantánea de BYPASS.                                                                                                                         |
| Etapa de la cadena TX (**EQ / COMP / GATE / DESS / TUBE / PUDU / VERB**)                                                                           | Asa de arrastre | Un solo clic alterna la derivación (bypass) de esa etapa. Doble clic abre su editor flotante sin marco (o la tira de canal Aetherial Audio). Arrastre a la izquierda o derecha para reordenar. El texto de ayuda debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder".                                         |
| **BYPASS**                                                                                                                                          | Botón de alternancia | Deshabilita todas las etapas del lado de la cadena mostrado actualmente de una vez. Cuando está marcado, toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Sin marcar: vuelve a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. Refleja la derivación a nivel del motor para el modo actual. |
| Etapa de la cadena RX (**EQ / AGC-G / AGC-C / DESS / TUBE / EVO**)                                                                                 | Asa de arrastre | Un solo clic alterna la derivación de la etapa de RX. Doble clic abre su editor flotante sin marco en modo RX. Arrastre a la izquierda o derecha para reordenar la cadena de RX. El orden es independiente de la cadena de TX. El tipo mime distinto 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Mosaico de estado **RADIO**                                                                                                                         | Indicador      | Extremo final no interactivo del lado RX. Se vuelve verde cuando el audio de PC (la transmisión SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                    |
| Mosaico de estado/derivación **ADSP**                                                                                                               | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (ej. 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic deriva todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. Doble clic abre el diálogo de configuración de AetherDSP. Solo visible en modo RX. Adopta el mismo estilo de anillo azul y punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la derivación. |
| Mosaico de estado **SPEAK**                                                                                                                         | Indicador      | Extremo final no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                              |
| **Record** (glifo de círculo)                                                                                                                       | Botón de alternancia | Captura hasta 30 s de audio TX posterior a PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Tooltip: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)." Oculto en modo RX (función solo de TX). Solo se habilita cuando la entrada del micrófono está lista y la reproducción no está en ejecución. Parpadea en rojo mientras graba.          |
| **Play** (glifo de triángulo)                                                                                                                       | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce.                                                                                                                            |

## Indicadores

| Indicador                    | Estados                                  | Significado                                                                                                          |
|------------------------------|------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Indicador de punto final TX  | inactivo, pulso rojo                     | Pulso rojo mientras el usuario está transmitiendo en su propio segmento (slice) (controlado por TransmitModel::moxChanged). Solo cadena TX. |
| Indicador de micrófono listo | listo, no listo                          | Habilita/deshabilita el botón de grabación según la fuente del micrófono (PC) y el estado de DAX.                     |
| Pulso de monitor de grabación | inactivo, rojo brillante, rojo tenue     | Pulso de 500 ms mientras el grabador posterior a PUDU captura audio.                                                  |
| Pulso de monitor de reproducción | inactivo, verde brillante, verde tenue   | Pulso de 500 ms mientras se reproduce el audio capturado.                                                             |
| Ayuda de interacción          | Click to bypass · Double click to edit · Drag to reorder | Indicación de uso estática, se muestra tanto en modo TX como RX.                                                   |
| Indicador de colocación       | inactivo, barra cian vertical entre dos mosaicos | Vista previa en vivo de dónde aterrizará una etapa arrastrada antes de soltarla; renderizado por ambos widgets de cadena durante el arrastre. |

## Consejos

- El texto de ayuda debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" como un recordatorio rápido de las tres interacciones.
- Los órdenes de las cadenas TX y RX son completamente independientes. Reordenar la cadena TX no afecta a `ClientCompRxChainStages`.
- Las etiquetas de las etapas de la cadena RX son **AGC-G** (puerta) y **AGC-C** (compresor). Estas corresponden a las funciones de puerta y compresor respectivamente. Las seis etapas de RX (EQ, AGC-G, AGC-C, DESS, TUBE, EVO) están completamente implementadas.
- Un solo clic en un mosaico de etapa alterna su estado de derivación, no un reordenamiento. Asegúrese de estar arrastrando, no haciendo clic, cuando pretenda mover una etapa.
- Si **BYPASS** está actualmente marcado cuando reordena, las posiciones de las etapas aún se actualizan. La instantánea de derivación se basa en qué etapas estaban habilitadas, no en su posición.
- Hacer doble clic en cualquier mosaico de etapa de la cadena TX abre la tira de canal Aetherial Audio, que proporciona el editor DSP de TX unificado. El botón **BYPASS** en la tira de canal y el botón **BYPASS** en el applet de la cadena controlan el mismo estado de derivación de TX a nivel del motor y se sincronizan automáticamente entre sí.
- El botón **BYPASS** ahora se sincroniza con la derivación a nivel del motor tanto para el modo TX como para el RX. Cuando alterna la derivación en la tira de canal Aetherial Audio (TX) o en el editor de la cadena RX, el botón BYPASS del applet de la cadena se actualiza automáticamente.

## Solución de problemas

- **Arrastrar no hace nada o se rechaza la colocación** — Confirme que **TX** es el botón de modo seleccionado (resaltado en ámbar). Arrastrar solo está activo en la tira de la cadena mostrada actualmente; si **RX** está seleccionado, no se aceptan colocaciones en la tira de TX.
- **El nuevo orden se pierde después de reiniciar** — Esto no debería ocurrir si la colocación se completó con éxito (apareció el indicador de colocación cian y soltó sobre la tira). Si se repite, verifique que AetherSDR tenga acceso de escritura a su almacenamiento de configuración.
- **El estado del botón BYPASS no coincide con lo que configuré en la tira de canal** — El applet de la cadena refleja el estado de derivación apropiado según el modo actual. Cuando TX está activo, muestra el estado de derivación de TX; cuando RX está activo, muestra el estado de derivación de RX. Ambos están sincronizados con el motor.

## Relacionados

- [Resumen de la cadena Aetherial Audio](overview.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Derivar todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
