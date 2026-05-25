# Vea de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)

La vista de la cadena RX en el applet Aetherial Audio Chain incluye tres indicadores de estado — RADIO, ADSP y SPEAK —, dos interactivos y uno no interactivo, que muestran el estado en vivo de su ruta de señal de recepción sin necesidad de abrir ningún cuadro de diálogo.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para habilitarlo.
- Debe estar viendo la cadena RX. Los indicadores de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Aetherial Audio Chain aún no se muestra.
2. En el encabezado del applet, haga clic en **RX**. La tira de la cadena RX reemplaza a la tira de la cadena TX, y los tres indicadores de estado aparecen a cada lado de las etapas de procesamiento.
3. Lea los tres indicadores de izquierda a derecha:
   - **RADIO** — se ilumina en verde cuando el audio del PC (el flujo SSB estándar) está habilitado en la radio.
   - **ADSP** — refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4` o `BNR`). Cuando ningún reductor de ruido está activo, la etiqueta del indicador vuelve a `ADSP`. Un solo clic desvía todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Un doble clic abre el cuadro de diálogo AetherDSP Settings.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

Los indicadores RADIO y SPEAK se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Indicador                                                                       | Tipo                         | Comportamiento                                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------------------------------------------------------------|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RADIO**                                                                       | Indicador                    | Se ilumina en verde cuando el audio del PC está habilitado. No es interactivo.                                                                                                                                                                                                                                                                                                            |
| **ADSP**                                                                        | Botón de alternancia/indicador | La etiqueta cambia al nombre corto del reductor de ruido activo (`NR2`, `NR4`, `BNR`); muestra `ADSP` cuando ninguno está activo. Un solo clic desvía todo el clúster NR; otro solo clic restaura el estado NR anterior. Un doble clic abre AetherDSP Settings. Se ilumina en verde cuando un reductor de ruido está activo.                                                            |
| **SPEAK**                                                                       | Indicador                    | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. No es interactivo.                                                                                                                                                                                                                                                                                        |
| Etapa de la cadena RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**) | Asa de arrastre              | Un solo clic alterna el desvío de la etapa RX; un doble clic abre su editor flotante sin marco en modo RX; arrastre reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distintivo `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |

Los indicadores RADIO y SPEAK no son interactivos. Un solo clic, doble clic o arrastre no tiene ningún efecto sobre ellos.

## Cómo funcionan los DESVÍOS TX y RX

El estado de DESVÍO tanto para TX como para RX es propiedad del motor de audio, en lugar de rastrearse localmente en el applet. Esto significa que el botón **BYPASS** en ambos lados se mantiene sincronizado con el control **BYPASS** correspondiente en la tira de canal de audio de Aetherial (TX) o los controles internos de la tira RX. Al presionar **BYPASS** en cualquier lugar, se refleja inmediatamente en el otro lugar.

Al cambiar entre las pestañas TX y RX, la visualización del botón **BYPASS** se actualiza para mostrar el estado actual propiedad del motor para el lado recién activado. No se necesita una gestión de instantáneas separada para ninguna de las cadenas.

## Cómo funciona el doble clic en las etapas de la cadena TX

Al hacer doble clic en cualquier indicador de etapa de la cadena TX, se abre la **Aetherial Audio Channel Strip** — la ventana unificada de DSP de TX. Los editores por etapa permanecen accesibles desde la propia tira de canal.

Al hacer doble clic en una etapa de la cadena RX, se abre el editor flotante sin marco por etapa para esa etapa.

## Cómo funciona la discriminación de clics

Cuando hace un solo clic en una etapa de la cadena, AetherSDR espera la duración establecida en **Interaction Settings** (accesible desde `View > Interaction Settings`) antes de decidir si fue un solo clic o el primer clic de un doble clic. Esto evita alternancias de desvío accidentales cuando tiene la intención de hacer doble clic para abrir un editor.

- Si hace doble clic en una etapa, el editor se abre inmediatamente y no se produce ninguna alternancia de desvío.
- Si hace un solo clic en una etapa y luego se detiene, el desvío se alterna después de que transcurra el intervalo de interacción.
- El intervalo predeterminado coincide con el tiempo de doble clic de su sistema operativo, pero puede ajustarlo en Interaction Settings para adaptarlo mejor a su velocidad de clic.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el próximo inicio mediante la configuración persistida `PooDooAudioActiveTab`. Si desea que los indicadores de estado RX estén visibles de forma predeterminada, deje la pestaña **RX** seleccionada cuando cierre AetherSDR.
- El cambio de la etiqueta del indicador **ADSP** a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activado, sin tener que abrir `Settings > AetherDSP Settings...`.
- Las etapas de puerta y compresor en la cadena RX están etiquetadas como **AGC-G** y **AGC-C** respectivamente. Estas corresponden internamente a las etapas Gate y Comp.
- Debido a que el estado de desvío ahora es propiedad del motor para ambos lados, el botón **BYPASS** reflejará correctamente cualquier cambio de desvío realizado desde otras fuentes, incluso si el applet de cadena no fue la fuente de ese cambio.
- La cadena RX incluye una etapa DESS (De-Esser) completamente implementada entre AGC-C y TUBE.
- Si descubre que los clics simples a veces activan el desvío cuando tenía la intención de hacer doble clic, ajuste el intervalo de discriminación de clics en `View > Interaction Settings` a un valor más largo.

## Relacionados

- [Resumen de Aetherial Audio Chain](overview.md)
- [Cambie entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Desvíe todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
