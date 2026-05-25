# Cambiar entre la edición de las cadenas de TX y RX

El applet Aetherial Audio Chain muestra la cadena DSP de TX o RX a la vez. Utilice los botones de alternancia TX y RX para cambiar qué cadena es visible y editable. Su última selección se restaura al reabrir el applet.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado PUDU en la barra lateral derecha para mostrarlo.
- La cadena de TX se muestra de forma predeterminada. Si nunca ha cambiado la selección, solo necesita hacer clic en RX.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet Aetherial Audio Chain. Contiene los botones TX, RX y BYPASS.
2. Haga clic en TX para mostrar y editar la cadena DSP de TX (Parametric EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb).
3. Haga clic en RX para mostrar y editar la cadena DSP de RX (EQ, AGC-G, AGC-C, DESS, TUBE, EVO), que también muestra los mosaicos de estado RADIO, ADSP y SPEAK.
4. El botón seleccionado se vuelve ámbar. La tira de la cadena que está debajo se actualiza inmediatamente para mostrar el lado elegido.

## Qué hace cada control

| Control                                                        | Tipo                                                                                                                                                                                                                                                                                                                                                                                   | Valor predeterminado                                                                                                                                                                                                                                                               |
|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                             | Muestra y edita la cadena DSP de TX (ClientChainWidget), completamente interactiva: clic para bypass, doble clic para editar, arrastrar para reordenar.                                                                                                                                                                                                                                | Forma parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionado. La última pestaña activa se conserva mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                |
| RX                                                             | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| BYPASS                                                         | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| Grabar (glifo de círculo)                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| Reproducir (glifo de triángulo)                                | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                   | Sin marcar                                                                                                                                                                                                                                                                         |
| Etapa de cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic activa/desactiva el bypass de la etapa; doble clic abre su editor flotante sin marco; arrastrar reordena la cadena de TX.                                                                                                                                                                                                                                                | Delegado a ClientChainWidget                                                                                                                                                                                                                                                       |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)       | Un solo clic activa/desactiva el bypass de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX.                                                                                                                                                                                                                                   | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distintivo 'application/x-aethersdr-rx-chain-stage' evita colocaciones accidentales entre las dos tiras. |
| Mosaico de estado RADIO                                        | Final de libro no interactivo del lado RX. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado.                                                                                                                                                                                                                                                                    | Solo visible en modo RX                                                                                                                                                                                                                                                            |
| Mosaico de estado/bypass ADSP                                  | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activado. Un solo clic desvía todo el clúster de NR con una instantánea en memoria; otro solo clic restaura el estado de NR anterior. Doble clic abre el diálogo de configuración de AetherDSP. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul con punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento del bypass.                                                     |
| Mosaico de estado SPEAK                                        | Final de libro no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR está activada (sin silenciar).                                                                                                                                                                                                                                                        | Solo visible en modo RX                                                                                                                                                                                                                                                            |

TX y RX forman un par exclusivo; solo uno puede estar activo a la vez. La pestaña activa se guarda como `PooDooAudioActiveTab` con el valor `TX` o `RX` y se restaura en el siguiente inicio.

Las cadenas de TX y RX son completamente independientes: cada una tiene su propio orden de etapas, estado de bypass por etapa e instantánea global BYPASS. Cambiar de lado no afecta el estado de la otra cadena. El orden de la cadena TX se conserva como `ClientCompTxChainStages`; el orden de la cadena RX como `ClientCompRxChainStages`.

## Cómo funciona el doble clic en las etapas de la cadena TX

Hacer doble clic en cualquier mosaico de etapa de la cadena TX abre Aetherial Audio Channel Strip, la ventana unificada de DSP de TX. Los editores de etapa individuales siguen siendo accesibles desde el panel del canal. Hacer doble clic en un mosaico de etapa TX es la forma canónica de abrir sus ajustes de audio de TX.

Hacer doble clic en un mosaico de etapa de la cadena RX abre el editor flotante de esa etapa.

## Cómo se mantiene sincronizado el botón BYPASS

En v0.9.8, el estado de bypass es propiedad del motor de audio tanto para el lado TX como para el RX. El botón BYPASS en el applet de la cadena y el botón BYPASS en Aetherial Audio Channel Strip (para TX) siempre reflejan el mismo estado. Hacer clic en BYPASS en cualquiera de los controles actualiza el otro automáticamente. Cuando cambia entre los modos TX y RX, el botón BYPASS inicializa su estado visual a partir del estado de bypass actual del motor para ese lado.

## Intervalo de discriminación de clic

En v26.5.3, el applet de la cadena utiliza un intervalo de discriminación de clic configurable en lugar del intervalo de doble clic del sistema. Este intervalo controla cuánto tiempo espera el applet después de soltar el mouse antes de decidir si la acción es un solo clic o el primero de un doble clic. Para ajustar este intervalo:

1. Abra Settings desde el menú principal.
2. Navegue a la página de configuración Interaction.
3. Ajuste el control deslizante del intervalo de discriminación de clic según su preferencia (en milisegundos).
4. El nuevo intervalo surte efecto inmediatamente para todas las interacciones con las etapas de la cadena.

Esta configuración se aplica tanto a los widgets de la cadena TX como a los de la cadena RX. Un intervalo más corto hace que el doble clic sea más sensible, pero puede provocar acciones involuntarias de un solo clic en dobles clics rápidos. Un intervalo más largo hace que las acciones de un solo clic sean más fiables a costa de un ligero retraso antes de que se ejecuten.

## Consejos

- El botón BYPASS siempre actúa solo en el lado que se muestra actualmente. Cambiar de TX a RX y hacer clic en BYPASS solo desvía la cadena RX; el estado de bypass de la cadena TX no cambia.
- Los botones de monitor de grabación (⏺) y reproducción (▶) están ocultos cuando se selecciona RX; son funciones solo de TX.
- El texto de sugerencia debajo de la tira de la cadena, "Click to bypass · Double click to edit · Drag to reorder", se aplica por igual a las cadenas TX y RX.
- Las etiquetas de las etapas RX son AGC-G (gate) y AGC-C (compressor). Estas etiquetas aparecen en los propios mosaicos de etapa y en los títulos de cualquier editor de etapa.
- Si hace clic en BYPASS en el panel del canal mientras el applet de la cadena muestra el lado TX, el botón BYPASS del applet se actualiza inmediatamente para coincidir; no es necesario actualizar manualmente.
- La etiqueta del mosaico ADSP cambia dinámicamente para mostrar el módulo reductor de ruido activo (p. ej., NR2, NR4, BNR). Si no hay ningún reductor de ruido activo, muestra ADSP.

## Relacionados

- [Aetherial Audio Chain overview](overview.md)
- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Bypass every RX stage at once](bypass-every-rx-stage-at-once.md)
- [Reorder the TX DSP chain](reorder-the-tx-dsp-chain.md)
- [Reorder the RX DSP chain (independent of TX order)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [See at a glance whether PC Audio, the noise reducer, and audio output are live (RX status tiles)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
