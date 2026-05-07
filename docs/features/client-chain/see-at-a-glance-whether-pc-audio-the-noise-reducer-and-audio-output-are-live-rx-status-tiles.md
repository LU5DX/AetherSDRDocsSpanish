# Vea de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (azulejos de estado de RX)

La vista de la cadena de RX en el applet Cadena de Audio Aetherial incluye tres azulejos de estado — RADIO, ADSP y SPEAK — que muestran el estado en vivo de su ruta de señal de recepción sin necesidad de abrir ningún diálogo.

## Antes de comenzar

- El applet Cadena de Audio Aetherial debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado como `PUDU` en la barra lateral derecha para activarlo.
- Debe estar viendo la cadena de RX. Los azulejos de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Cadena de Audio Aetherial aún no se muestra.
2. En el encabezado del applet, haga clic en **RX**. La tira de la cadena de RX reemplaza a la tira de la cadena de TX y los tres azulejos de estado aparecen a cada lado de las etapas de procesamiento.
3. Lea los tres azulejos de izquierda a derecha:
   - **RADIO** — se ilumina en verde cuando el Audio del PC (el flujo SSB estándar) está habilitado en la radio.
   - **ADSP** — refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4` o `BNR`). Cuando no hay ningún reductor de ruido activo, la etiqueta del azulejo vuelve a `ADSP`. Un solo clic omite todo el grupo NR con una instantánea en memoria; otro solo clic restaura el estado anterior del NR. Un doble clic abre el diálogo de Configuración de AetherDSP.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

Los azulejos RADIO y SPEAK se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Azulejo                                                               | Tipo                                                                                                                                                                                                                                                                                                                                                                                   | Comportamiento                                                                                                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RADIO**                                                             | Indicador                                                                                                                                                                                                                                                                                                                                                                              | Se ilumina en verde cuando el Audio del PC está habilitado. No es interactivo.                                                                                                                                                                                                                                                 |
| **ADSP**                                                              | Botón de alternancia / indicador                                                                                                                                                                                                                                                                                                                                                       | La etiqueta cambia al nombre corto del reductor de ruido activo (`NR2`, `NR4`, `BNR`); muestra `ADSP` cuando ninguno está activo. Un solo clic omite todo el grupo NR; otro solo clic restaura el estado anterior del NR. Un doble clic abre Configuración de AetherDSP. Se ilumina en verde cuando un reductor de ruido está activo. |
| **SPEAK**                                                             | Indicador                                                                                                                                                                                                                                                                                                                                                                              | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. No es interactivo.                                                                                                                                                                                                                              |
| Etapa de la cadena de RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**) | Mango de arrastre                                                                                                                                                                                                                                                                                                                                                                     | Un solo clic alterna la omisión de la etapa de RX; un doble clic abre su editor flotante sin marco en modo RX; arrastre reordena la cadena de RX. Las seis etapas de RX (EQ, AGC-G/Puerta, AGC-C/Comp, DESS/De-Esser, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita caídas accidentales entre las dos tiras. |

Los azulejos RADIO y SPEAK no son interactivos. Un solo clic, doble clic y arrastre no tienen efecto sobre ellos.

## Cómo funcionan BYPASS en TX y RX en v0.9.8

En v0.9.8, el estado BYPASS tanto para TX como para RX es propiedad del motor de audio en lugar de ser rastreado localmente en el applet. Esto significa que el botón **BYPASS** en cualquier lado permanece sincronizado con el control BYPASS correspondiente en la Tira de Canales de Audio Aetherial (TX) o los controles internos de la tira de RX. Presionar **BYPASS** en cualquier ubicación se refleja inmediatamente en la otra.

Al cambiar entre las pestañas TX y RX, la actualización visual del botón **BYPASS** muestra el estado actual de propiedad del motor para el lado recién activo. No se necesita ninguna gestión de instantáneas separada para ninguna de las cadenas.

## Cómo funciona el doble clic en las etapas de la cadena de TX en v0.9.8

Un doble clic en cualquier azulejo de la etapa de la cadena de TX abre la **Tira de Canales de Audio Aetherial** — la ventana unificada de DSP de TX. Los editores por etapa permanecen accesibles desde la propia tira de canales.

Un doble clic en una etapa de la cadena de RX abre el editor flotante sin marco para esa etapa.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el próximo inicio mediante el ajuste persistente `PooDooAudioActiveTab`. Si desea que los azulejos de estado de RX estén visibles por defecto, deje la pestaña **RX** seleccionada cuando cierre AetherSDR.
- Que la etiqueta del azulejo **ADSP** cambie a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activado, sin abrir `Ajustes > Configuración de AetherDSP...`.
- Las etapas de puerta y compresor en la cadena de RX están etiquetadas como **AGC-G** y **AGC-C** respectivamente. Estas corresponden internamente a las etapas de Puerta y Comp.
- Debido a que el estado de bypass ahora es propiedad del motor para ambos lados, el botón **BYPASS** reflejará correctamente cualquier cambio de bypass realizado desde otras fuentes, incluso si el applet de la cadena no fue la fuente de dicho cambio.
- La cadena de RX incluye una etapa DESS (De-Esser) completamente implementada entre AGC-C y TUBE.

## Relacionados

- [Descripción general de la Cadena de Audio Aetherial](overview.md)
- [Cambie entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omita todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
