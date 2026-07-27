# Cambiar entre la edición de las cadenas de TX y RX

El applet Aetherial Audio Chain muestra la cadena DSP de TX o RX a la vez. Use los botones TX y RX para alternar qué cadena está visible y editable. Su última selección se restaura al reabrir el applet.

## Antes de comenzar

- El contenedor Aetherial Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado PUDU en la barra lateral derecha para mostrarlo.
- La cadena de TX se muestra por defecto. Si nunca ha cambiado la selección, basta con hacer clic en RX.

## Pasos

1. Localice la fila de encabezado en la parte superior del applet Aetherial Audio Chain. Contiene los botones TX, RX y BYPASS.
2. Haga clic en TX para mostrar y editar la cadena DSP de TX (Parametric EQ, Compressor, Gate, De-Ess, Tube, PUDU, Reverb).
3. Haga clic en RX para mostrar y editar la cadena DSP de RX (EQ, AGC-G, AGC-C, DESS, TUBE, EVO), la cual también muestra los mosaicos de estado RADIO, ADSP y SPEAK.
4. El botón seleccionado se vuelve ámbar. La franja de la cadena debajo se actualiza inmediatamente para mostrar el lado elegido.

## Qué hace cada control

| Control                                                        | Tipo                                                                                                                                                                                                                                                                                                                                                                                    | Predeterminado                                                                                                                                                                                                                                                                     |
|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX                                                             | Muestra y edita la cadena DSP de TX (ClientChainWidget) — totalmente interactiva: clic para anular, doble clic para editar, arrastrar para reordenar.                                                                                                                                                                                                                                   | Parte de un par exclusivo con RX; color ámbar 'VUDU' cuando está seleccionada. La última pestaña activa persiste mediante PooDooAudioActiveTab='TX' / 'RX'.                                                                                                                          |
| RX                                                             | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                    | Desmarcado                                                                                                                                                                                                                                                                         |
| BYPASS                                                         | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                    | Desmarcado                                                                                                                                                                                                                                                                         |
| Grabar (glifo circular)                                        | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                    | Desmarcado                                                                                                                                                                                                                                                                         |
| Reproducir (glifo triangular)                                  | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                    | Desmarcado                                                                                                                                                                                                                                                                         |
| Etapa de la cadena TX (EQ / COMP / GATE / DESS / TUBE / PUDU / VERB) | Un solo clic alterna la anulación de la etapa; doble clic abre su editor flotante sin marco; arrastrar reordena la cadena TX.                                                                                                                                                                                                                                                           | Delegado a ClientChainWidget                                                                                                                                                                                                                                                       |
| Etapa de la cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO)      | Un solo clic alterna la anulación de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX.                                                                                                                                                                                                                                            | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita caídas no deseadas entre las dos franjas. |
| Mosaico de estado RADIO                                        | Separador del lado RX no interactivo. Se vuelve verde cuando el audio de PC (la transmisión SSB estándar) está habilitado.                                                                                                                                                                                                                                                              | Solo visible en modo RX                                                                                                                                                                                                                                                            |
| Mosaico de estado/anulación ADSP                               | Mosaico interactivo del lado RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p.ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic anula todo el grupo NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Doble clic abre el diálogo de configuración de AetherDSP. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos al momento de la anulación. |
| Mosaico de estado SPEAK                                        | Separador del lado RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR está activada.                                                                                                                                                                                                                                                                             | Solo visible en modo RX                                                                                                                                                                                                                                                            |

TX y RX forman un par exclusivo — solo uno puede estar activo a la vez. La pestaña activa se guarda como `PooDooAudioActiveTab` con el valor `TX` o `RX` y se restaura en el próximo inicio.

Las cadenas TX y RX son completamente independientes: cada una tiene su propio orden de etapas, estado de anulación por etapa y una instantánea global de BYPASS. Cambiar de lado no afecta el estado de la otra cadena. El orden de la cadena TX se persiste como `ClientCompTxChainStages`; el orden de la cadena RX como `ClientCompRxChainStages`.

## Cómo funciona el doble clic en las etapas de la cadena TX

Al hacer doble clic en cualquier mosaico de etapa de la cadena TX se abre el Aetherial Audio Channel Strip — la ventana unificada DSP de TX. Los editores de etapa individuales siguen siendo accesibles desde el channel strip. Hacer doble clic en un mosaico de etapa TX es la forma canónica de abrir su configuración de audio TX.

Al hacer doble clic en un mosaico de etapa de la cadena RX se abre el editor flotante de esa etapa.

## Cómo se mantiene sincronizado el botón BYPASS

En v26.6.1, el estado de anulación es propiedad del motor de audio para ambos lados TX y RX. El botón BYPASS en el applet de la cadena y el botón BYPASS en el Aetherial Audio Channel Strip (para TX) siempre reflejan el mismo estado. Al hacer clic en BYPASS en cualquiera de los dos controles, el otro se actualiza automáticamente. Al cambiar entre los modos TX y RX, el botón BYPASS inicializa su estado visual a partir del estado de anulación actual del motor para ese lado.

El botón BYPASS desactiva todas las etapas de la cadena seleccionada, incluido RN2 en el lado TX. Su alcance es global (por motor de audio), no por perfil — el botón permanece presionado al cambiar entre perfiles de Channel Strip.

## Cómo maneja el mosaico ADSP el NV AFX

En v26.7.4, el mosaico ADSP en la cadena RX ahora reconoce y gestiona NV AFX como el séptimo módulo de reducción de ruido. Anteriormente, el módulo NV AFX no estaba incluido en el mecanismo de instantánea de anulación.

Al hacer un solo clic en el mosaico ADSP:

- Si algún reductor de ruido (NR2, NR4, MNR, DFNR, RN2 o NV AFX) está activo, al hacer clic en el mosaico ADSP se anulan todos, incluido NV AFX.
- Si ningún reductor de ruido está activo, al hacer clic en el mosaico ADSP se restaura el módulo previamente activo. Si NV AFX era el módulo activo antes de la anulación, se restaura correctamente.

La etiqueta del mosaico ADSP se actualiza para mostrar NV AFX cuando ese módulo está activo, rotando entre los otros nombres cortos (NR2, NR4, BNR, etc.) según corresponda. Cuando ningún reductor de ruido está activo, el mosaico muestra ADSP.

## Intervalo de discriminación de clics

En v26.5.3, el applet de la cadena utiliza un intervalo de discriminación de clics configurable en lugar del intervalo de doble clic del sistema. Este intervalo controla cuánto tiempo espera el applet después de soltar el mouse antes de decidir si la acción es un solo clic o el primero de un doble clic. Para ajustar este intervalo:

1. Abra Settings desde el menú principal.
2. Navegue a la página de configuración Interaction.
3. Ajuste el control deslizante del intervalo de discriminación de clics a su preferencia (en milisegundos).
4. El nuevo intervalo surte efecto inmediatamente para todas las interacciones con las etapas de la cadena.

Esta configuración se aplica tanto a los widgets de la cadena TX como RX. Un intervalo más corto hace que el doble clic sea más sensible, pero puede provocar acciones de un solo clic no deseadas en dobles clics rápidos. Un intervalo más largo hace que las acciones de un solo clic sean más fiables a costa de un ligero retraso antes de ejecutarse.

## Consejos

- El botón BYPASS siempre actúa únicamente sobre el lado mostrado actualmente. Cambiar de TX a RX y hacer clic en BYPASS anula solo la cadena RX; el estado de anulación de la cadena TX no cambia.
- Los botones de monitor de grabar (⏺) y reproducir (▶) están ocultos cuando se selecciona RX — son funciones solo de TX.
- El texto de sugerencia debajo de la franja de la cadena, "Click to bypass · Double click to edit · Drag to reorder", se aplica por igual a las cadenas TX y RX.
- Los mosaicos de etapa RX están etiquetados como AGC-G (gate) y AGC-C (compressor). Estas etiquetas aparecen en los propios mosaicos de etapa y en los títulos de cualquier editor de etapa.
- Si hace clic en BYPASS en el channel strip mientras el applet de la cadena muestra el lado TX, el botón BYPASS del applet se actualiza inmediatamente para coincidir — no es necesario actualizarlo manualmente.
- La etiqueta del mosaico ADSP cambia dinámicamente para mostrar el módulo reductor de ruido activo (p.ej., NR2, NR4, NV AFX). Si ningún reductor de ruido está activo, muestra ADSP.
- El mosaico ADSP ahora maneja correctamente NV AFX como parte del grupo de reducción de ruido. Si tenía NV AFX activo y anuló todos los reductores de ruido con un solo clic, al hacer clic nuevamente en el mosaico ADSP se restaura NV AFX (no NR2) tal como estaba antes de la anulación.

## Relacionados

- [Resumen de Aetherial Audio Chain](overview.md)
- [Anular todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Anular todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (mosaicos de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
