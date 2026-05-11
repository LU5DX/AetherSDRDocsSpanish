# Reordenar la cadena DSP de TX

Arrastre las etapas DSP de TX a un orden diferente para cambiar la secuencia en la que se procesa su audio antes de la transmisión. El nuevo orden se guarda automáticamente y persiste al reiniciar la aplicación.

## Antes de comenzar

- El contenedor Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como **PUDU** en la barra lateral derecha para mostrarlo.
- La cadena de TX debe ser el lado activo. Si el botón **RX** está seleccionado actualmente, haga clic en **TX** primero.

## Pasos

1. Abra el contenedor Aetherial Audio Chain haciendo clic en el botón de bandeja **PUDU** si aún no está visible.
2. Haga clic en **TX** en la fila del encabezado para asegurarse de que se muestre la cadena de TX.
3. Localice la etapa que desea mover. La cadena de TX contiene estas etapas: **EQ**, **COMP**, **GATE**, **DESS**, **TUBE**, **PUDU**, **VERB**.
4. Haga clic y mantenga presionado el mosaico de la etapa que desea mover, luego arrástrelo a la izquierda o derecha a lo largo de la tira de la cadena.
5. Aparecerá una barra cian vertical entre los mosaicos mientras arrastra, mostrando dónde se colocará la etapa.
6. Suelte el botón del ratón para soltar la etapa en la nueva posición.
7. Repita para cualquier otra etapa que desee reordenar.

El nuevo orden de la cadena se guarda automáticamente en `ClientCompTxChainStages`.

## Qué hace cada control

| Control                                                           | Tipo          | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX**                                                            | Botón de alternancia | Muestra y permite la edición de la cadena DSP de TX. Debe estar seleccionado para arrastrar etapas de TX. Color "PooDoo" ámbar cuando está seleccionado. La última pestaña activa persiste mediante `PooDooAudioActiveTab`.                                                                                                                                                                                                                                                                                                                                                           |
| **RX**                                                            | Botón de alternancia | Cambia la tira a la cadena de RX. Las operaciones de arrastre en la tira de RX no afectan el orden de TX. Cada lado mantiene el estado de etapa, el orden de la cadena y la instantánea BYPASS de forma independiente.                                                                                                                                                                                                                                                                                                                                                         |
| Etapa de cadena TX (**EQ / COMP / GATE / DESS / TUBE / PUDU / VERB**) | Controlador de arrastre | Un solo clic alterna la omisión de esa etapa. Doble clic abre su editor flotante sin marco (o el Aetherial Audio Channel Strip). Arrastre a la izquierda o derecha para reordenar. El texto de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder".                                                                                                                                                                                                                                                                        |
| **BYPASS**                                                        | Botón de alternancia | Deshabilita todas las etapas del lado de la cadena que se muestra actualmente de una vez. Cuando está marcado, captura una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas. Sin marcar: vuelve a habilitar solo las etapas que estaban activas antes. TX y RX mantienen instantáneas separadas. Refleja la omisión a nivel del motor para el modo actual.                                                                                                                                                            |
| Etapa de cadena RX (**EQ / AGC-G / AGC-C / DESS / TUBE / EVO**)  | Controlador de arrastre | Un solo clic alterna la omisión de la etapa de RX. Doble clic abre su editor flotante sin marco en modo RX. Arrastre a la izquierda o derecha para reordenar la cadena de RX. El orden es independiente de la cadena de TX. El tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita que se suelten elementos entre las dos tiras.                                                                                                                                                                                                                              |
| Mosaico de estado **RADIO**                                       | Indicador     | Marcador final del lado RX no interactivo. Se vuelve verde cuando el Audio de PC (la transmisión SSB estándar) está habilitado. Solo visible en modo RX.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Mosaico de estado/omisión **ADSP**                                | Botón de alternancia | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic omite todo el grupo NR con una instantánea en memoria; otro solo clic restaura el estado anterior de NR. Doble clic abre el diálogo de configuración de AetherDSP. Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la omisión. |
| Mosaico de estado **SPEAK**                                       | Indicador     | Marcador final del lado RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. Solo visible en modo RX.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| **Record** (glifo de círculo)                                     | Botón de alternancia | Captura hasta 30 s de audio TX post-PUDU; haga clic de nuevo para detener (la reproducción comienza automáticamente). Información sobre herramientas: "Record up to 30 s of post-PooDoo™ TX audio (MIC must be set to PC and DAX off)". Oculto en modo RX (función solo de TX). Solo se habilita cuando la entrada de micrófono está lista y la reproducción no está en curso. Parpadea en rojo mientras graba.                                                                                                                                                                  |
| **Play** (glifo de triángulo)                                     | Botón de alternancia | Reproduce el audio PUDU capturado; haga clic de nuevo para cancelar. Oculto en modo RX. Solo se habilita una vez que existe una grabación y la grabación no está activa. Parpadea en verde mientras reproduce.                                                                                                                                                                                                                                                                                                                                                                    |

## Indicadores

| Indicador                    | Estados                                  | Significado                                                                                                          |
|------------------------------|------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Indicador de punto final TX  | inactivo, pulso rojo                     | Pulso rojo mientras el usuario está transmitiendo en su propio slice (impulsado por TransmitModel::moxChanged). Solo cadena TX. |
| Indicador de micrófono listo | listo, no listo                          | Habilita/deshabilita el botón de grabación según la fuente del micrófono (PC) y el estado de DAX.                    |
| Pulso de monitor de grabación| inactivo, rojo brillante, rojo tenue     | Pulso de 500 ms mientras el grabador post-PUDU está capturando audio.                                                |
| Pulso de monitor de reproducción| inactivo, verde brillante, verde tenue | Pulso de 500 ms mientras se reproduce el audio capturado.                                                            |
| Sugerencia de interacción    | Haga clic para omitir · Doble clic para editar · Arrastre para reordenar | Sugerencia de uso estática, mostrada en los modos TX y RX.                                          |
| Indicador de destino         | inactivo, barra cian vertical entre dos mosaicos | Vista previa en vivo de dónde aterrizará una etapa arrastrada antes de soltarla; renderizado por ambos widgets de cadena durante el arrastre. |

## Consejos

- El texto de sugerencia debajo de la cadena dice "Click to bypass · Double click to edit · Drag to reorder" como recordatorio rápido de las tres interacciones.
- Los órdenes de las cadenas TX y RX son completamente independientes. Reordenar la cadena de TX no tiene efecto en `ClientCompRxChainStages`.
- Las etiquetas de las etapas de la cadena RX son **AGC-G** (compuerta) y **AGC-C** (compresor). Corresponden a las funciones de compuerta y compresor respectivamente. Las seis etapas de RX (EQ, AGC-G, AGC-C, DESS, TUBE, EVO) están completamente implementadas.
- Un solo clic en un mosaico de etapa alterna su estado de omisión, no un reordenamiento. Asegúrese de estar arrastrando, no haciendo clic, cuando pretenda mover una etapa.
- Si **BYPASS** está actualmente marcado cuando reordena, las posiciones de las etapas aún se actualizan. La instantánea de omisión se basa en qué etapas estaban habilitadas, no en su posición.
- El doble clic en cualquier mosaico de etapa de la cadena TX abre el Aetherial Audio Channel Strip, que proporciona el editor DSP de TX unificado. El botón **BYPASS** en el canal strip y el botón **BYPASS** en el applet de la cadena controlan el mismo estado de omisión de TX a nivel del motor y se mantienen sincronizados automáticamente.
- El botón **BYPASS** ahora se sincroniza con la omisión a nivel del motor para los modos TX y RX. Cuando alterna la omisión en el Aetherial Audio Channel Strip (TX) o en el editor de la cadena RX, el botón BYPASS del applet de la cadena se actualiza automáticamente.

## Solución de problemas

- **El arrastre no hace nada o se rechaza el destino** — Confirme que **TX** es el botón de modo seleccionado (resaltado ámbar). El arrastre solo está activo en la tira de cadena que se muestra actualmente; si **RX** está seleccionado, no se aceptan destinos en la tira de TX.
- **El nuevo orden se pierde después de reiniciar** — Esto no debería ocurrir si el destino se completó correctamente (apareció el indicador de destino cian y soltó sobre la tira). Si se repite, verifique que AetherSDR tenga acceso de escritura a su almacenamiento de configuración.
- **El estado del botón BYPASS no coincide con lo que configuré en el channel strip** — El applet de la cadena refleja el estado de omisión apropiado según el modo actual. Cuando TX está activo, muestra el estado de omisión de TX; cuando RX está activo, muestra el estado de omisión de RX. Ambos están sincronizados con el motor.

## Relacionado

- [Aetherial Audio Chain overview](overview.md)
- [Reorder the RX DSP chain (independent of TX order)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Open a stage's frameless floating editor from the chain](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
