# Vea de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (bloques de estado de RX)

La vista de la cadena RX en el applet Aetherial Audio Chain incluye tres bloques de estado — dos interactivos y uno no interactivo — llamados RADIO, ADSP y SPEAK, que muestran el estado en vivo de la ruta de señal de recepción sin necesidad de abrir ningún cuadro de diálogo.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para activarlo.
- Debe estar viendo la cadena RX. Los bloques de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Aetherial Audio Chain aún no se muestra.
2. En el encabezado del applet, haga clic en **RX**. La tira de la cadena RX reemplaza a la tira de la cadena TX y los tres bloques de estado aparecen a cada lado de las etapas de procesamiento.
3. Lea los tres bloques de izquierda a derecha:
   - **RADIO** — se ilumina en verde cuando el Audio del PC (la secuencia SSB estándar) está habilitado en la radio.
   - **ADSP** — refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4`, `BNR`, `MNR`, `DFNR` o `RN2`). Cuando no hay ningún reductor de ruido activo, la etiqueta del bloque vuelve a `ADSP`. Un solo clic omite todo el conjunto NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Un doble clic abre el cuadro de diálogo de Configuración de AetherDSP.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

Los bloques RADIO y SPEAK se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Bloque                                                                           | Tipo                      | Comportamiento                                                                                                                                                                                                                                                                                                                                                                          |
|----------------------------------------------------------------------------------|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RADIO**                                                                        | Indicador                 | Se ilumina en verde cuando el Audio del PC está habilitado. No es interactivo.                                                                                                                                                                                                                                                                                                           |
| **ADSP**                                                                         | Botón de alternancia / indicador | La etiqueta cambia al nombre corto del reductor de ruido activo (`NR2`, `NR4`, `BNR`, `MNR`, `DFNR` o `RN2`); muestra `ADSP` cuando ninguno está activo. Un solo clic omite todo el conjunto NR; otro solo clic restaura el estado NR anterior. Un doble clic abre Configuración de AetherDSP. Se ilumina en verde cuando un reductor de ruido está activo. El módulo `BNR` ha sido reemplazado internamente por `NV AFX` — la etiqueta del bloque aún muestra `BNR` si ese módulo estaba activo al ser omitido. |
| **SPEAK**                                                                        | Indicador                 | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. No es interactivo.                                                                                                                                                                                                                                                                                       |
| Etapa de la cadena RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**) | Controlador de arrastre   | Un solo clic alterna la omisión de la etapa RX; un doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |

Los bloques RADIO y SPEAK no son interactivos. Un solo clic, doble clic y arrastre no tienen efecto sobre ellos.

## Cómo funcionan BYPASS en TX y RX

El estado BYPASS tanto para TX como para RX es propiedad del motor de audio, en lugar de rastrearse localmente en el applet. Esto significa que el botón **BYPASS** en cualquier lado se mantiene sincronizado con el control BYPASS correspondiente en la tira del canal de audio Aetherial (TX) o los controles internos de la tira RX. Presionar **BYPASS** en cualquier ubicación se refleja inmediatamente en la otra.

Al cambiar entre las pestañas TX y RX, la visualización del botón **BYPASS** se actualiza para mostrar el estado actual propiedad del motor para el lado recién activado. No se necesita una gestión de instantáneas separada para ninguna de las cadenas.

El botón BYPASS desactiva todas las etapas en la cadena seleccionada, incluido RN2. Su alcance es global (por motor de audio), no por perfil; el botón permanece presionado al cambiar de perfil de la tira del canal.

## Cómo funciona el doble clic en las etapas de la cadena TX

Hacer doble clic en cualquier bloque de etapa de la cadena TX abre la **tira del canal de audio Aetherial** — la ventana unificada de DSP de TX. Los editores por etapa siguen siendo accesibles desde la propia tira del canal.

Hacer doble clic en un bloque de etapa de la cadena RX abre el editor flotante sin marco por etapa para esa etapa.

## Cómo funciona la discriminación de clics

Cuando hace un solo clic en una etapa de la cadena, AetherSDR espera la duración establecida en **Configuración de interacción** (accesible desde `View > Interaction Settings`) antes de decidir si fue un solo clic o el primer clic de un doble clic. Esto evita alternancias de omisión accidentales cuando tiene la intención de hacer doble clic para abrir un editor.

- Si hace doble clic en una etapa, el editor se abre inmediatamente y no ocurre ninguna alternancia de omisión.
- Si hace un solo clic en una etapa y luego se detiene, la omisión se alterna después de que transcurra el intervalo de interacción.
- El intervalo predeterminado coincide con el tiempo de doble clic de su sistema operativo, pero puede ajustarlo en Configuración de interacción para adaptarlo mejor a su velocidad de clic.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el próximo inicio mediante la configuración persistente `PooDooAudioActiveTab`. Si desea que los bloques de estado RX sean visibles de forma predeterminada, deje la pestaña **RX** seleccionada al cerrar AetherSDR.
- Que la etiqueta del bloque **ADSP** cambie a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activado, sin abrir `Settings > AetherDSP Settings...`.
- Las etapas de puerta y compresor en la cadena RX están etiquetadas como **AGC-G** y **AGC-C** respectivamente. Estas corresponden internamente a las etapas Gate y Comp.
- Debido a que el estado de omisión ahora es propiedad del motor para ambos lados, el botón **BYPASS** reflejará correctamente cualquier cambio de omisión realizado desde otras fuentes, incluso si el applet de la cadena no fue la fuente de ese cambio.
- La cadena RX incluye una etapa DESS (De-Esser) completamente implementada entre AGC-C y TUBE.
- Si encuentra que los clics simples a veces activan la omisión cuando pretendía hacer doble clic, ajuste el intervalo de discriminación de clics en `View > Interaction Settings` a un valor más largo.
- El botón BYPASS desactiva todas las etapas, incluido RN2. Permanece activado al cambiar de perfil de la tira del canal, ya que su estado es global por motor de audio.
- El bloque ADSP ahora controla el módulo `NV AFX` en lugar del módulo heredado `BNR`. La etiqueta del bloque aún muestra `BNR` si ese módulo estaba activo cuando se tomó la instantánea y se restaura a `NV AFX` al anular la omisión.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
