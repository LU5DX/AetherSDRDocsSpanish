# Vea de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (indicadores de estado de RX)

La vista de la cadena de RX en el applet Aetherial Audio Chain incluye tres indicadores de estado — RADIO, ADSP y SPEAK — que muestran el estado en vivo de su ruta de señal de recepción sin necesidad de abrir ningún cuadro de diálogo.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para habilitarlo.
- Debe estar viendo la cadena de RX. Los indicadores de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Aetherial Audio Chain aún no se muestra.
2. En el encabezado del applet, haga clic en **RX**. La tira de la cadena de RX reemplaza a la tira de la cadena de TX, y los tres indicadores de estado aparecen a cada lado de las etapas de procesamiento.
3. Lea los tres indicadores de izquierda a derecha:
   - **RADIO** — se pone verde cuando el Audio de PC (la transmisión SSB estándar) está habilitado en la radio.
   - **ADSP** — refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4` o `BNR`). Cuando ningún reductor de ruido está encendido, la etiqueta del indicador vuelve a `ADSP`. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo AetherDSP Settings.
   - **SPEAK** — se pone verde cuando la salida de audio de AetherSDR está activada (sin silenciar).

Los indicadores RADIO y SPEAK se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Indicador                                                                      | Tipo                         | Comportamiento                                                                                                                                                                                                                                                                                                                                                                                |
|---------------------------------------------------------------------------------|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RADIO**                                                                       | Indicador                    | Se pone verde cuando el Audio de PC está habilitado. No es interactivo.                                                                                                                                                                                                                                                                                                                       |
| **ADSP**                                                                        | Botón de alternancia / indicador | La etiqueta cambia al nombre corto del reductor de ruido activo (`NR2`, `NR4`, `BNR`); muestra `ADSP` cuando ninguno está activo. Un solo clic omite todo el clúster NR; otro solo clic restaura el estado NR anterior. El doble clic abre AetherDSP Settings. Se pone verde cuando un reductor de ruido está encendido.                                                                                                  |
| **SPEAK**                                                                       | Indicador                    | Se pone verde cuando la salida de audio de AetherSDR está activada. No es interactivo.                                                                                                                                                                                                                                                                                                        |
| Etapa de la cadena de RX (**EQ** / **AGC-G** / **AGC-C** / **DESS** / **TUBE** / **EVO**) | Manija de arrastre           | Un solo clic alterna la omisión de la etapa de RX; el doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita caídas no deseadas entre las dos tiras. |

Los indicadores RADIO y SPEAK no son interactivos. El clic simple, el doble clic y el arrastre no tienen efecto sobre ellos.

## Cómo funcionan las omisiones (BYPASS) de TX y RX

El estado de omisión (BYPASS) tanto para TX como para RX es propiedad del motor de audio, no se rastrea localmente en el applet. Esto significa que el botón **BYPASS** en cualquier lado se mantiene sincronizado con el control BYPASS correspondiente en la Aetherial Audio Channel Strip (TX) o los controles internos de la tira de RX. Al presionar **BYPASS** en cualquier lugar, se refleja inmediatamente en el otro.

Al cambiar entre las pestañas TX y RX, la visualización del botón **BYPASS** se actualiza para mostrar el estado actual propiedad del motor para el lado recién activo. No se necesita una gestión de instantáneas separada para ninguna de las cadenas.

El botón BYPASS desactiva todas las etapas de la cadena seleccionada, incluido RN2. Su alcance es global (por motor de audio), no por perfil: el botón permanece presionado al cambiar entre perfiles de la Channel Strip.

## Cómo funciona el doble clic en las etapas de la cadena de TX

Al hacer doble clic en cualquier indicador de etapa de la cadena de TX, se abre la **Aetherial Audio Channel Strip**, la ventana unificada de DSP de TX. Los editores por etapa permanecen accesibles desde el interior de la propia channel strip.

Al hacer doble clic en una etapa de la cadena de RX, se abre el editor flotante sin marco por etapa para esa etapa.

## Cómo funciona la discriminación de clics

Cuando hace un solo clic en una etapa de la cadena, AetherSDR espera la duración establecida en **Interaction Settings** (accesible desde `View > Interaction Settings`) antes de decidir si fue un solo clic o el primer clic de un doble clic. Esto evita alternancias de omisión accidentales cuando tiene la intención de hacer doble clic para abrir un editor.

- Si hace doble clic en una etapa, el editor se abre de inmediato y no se produce ninguna alternancia de omisión.
- Si hace un solo clic en una etapa y luego se detiene, la omisión se alterna después de que transcurra el intervalo de interacción.
- El intervalo predeterminado coincide con el tiempo de doble clic de su sistema operativo, pero puede ajustarlo en Interaction Settings para adaptarlo mejor a su velocidad de clic.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el próximo inicio mediante la configuración persistente `PooDooAudioActiveTab`. Si desea que los indicadores de estado de RX sean visibles de forma predeterminada, deje la pestaña **RX** seleccionada al cerrar AetherSDR.
- Que la etiqueta del indicador **ADSP** cambie a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activado, sin abrir `Settings > AetherDSP Settings...`.
- Las etapas de compuerta (gate) y compresor en la cadena de RX están etiquetadas como **AGC-G** y **AGC-C** respectivamente. Estas corresponden a las etapas Gate y Comp internamente.
- Debido a que el estado de omisión ahora es propiedad del motor para ambos lados, el botón **BYPASS** reflejará correctamente cualquier cambio de omisión realizado desde otras fuentes, incluso si el applet de la cadena no fue la fuente de ese cambio.
- La cadena de RX incluye una etapa DESS (De-Esser) completamente implementada entre AGC-C y TUBE.
- Si descubre que los clics simples a veces activan la omisión cuando pretendía hacer doble clic, ajuste el intervalo de discriminación de clics en `View > Interaction Settings` a un valor más largo.
- El botón BYPASS desactiva todas las etapas, incluido RN2. Permanece activado al cambiar entre perfiles de la Channel Strip, ya que su estado es global por motor de audio.

## Relacionado

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
