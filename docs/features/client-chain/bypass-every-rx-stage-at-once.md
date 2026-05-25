# Inhabilitar todas las etapas de RX a la vez

Use el botón BYPASS para deshabilitar todas las etapas de la cadena de RX con un solo clic, sin perder el registro de qué etapas estaban activas. Al hacer clic nuevamente en BYPASS, solo se restauran las etapas que estaban habilitadas antes.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrar el contenedor.
- Debe estar viendo la cadena de RX. El botón BYPASS actúa sobre el lado de la cadena que se muestra actualmente.

## Pasos

1. En el encabezado del applet Aetherial Audio Chain, haga clic en **RX**. Las etapas de la cadena de RX aparecen debajo.
2. Haga clic en **BYPASS**. El botón cambia a su apariencia activada (borde y relleno ámbar). Cada etapa en la cadena de RX se deshabilita de inmediato. AetherSDR captura una instantánea de qué etapas estaban habilitadas en el momento en que hizo clic.
3. Para restaurar los estados anteriores de las etapas, haga clic nuevamente en **BYPASS**. Solo se vuelven a habilitar las etapas que estaban habilitadas antes de la inhabilitación.

## Qué hace cada control

| Control                                                     | Tipo                                                                                                                                                                                                                                                                                                                                                                                                                               | Predeterminado                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **RX**                                                      | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                                                               | Desmarcado                                                                                                                                                                                                                                                                                                                              |
| **BYPASS**                                                  | Botón de alternancia                                                                                                                                                                                                                                                                                                                                                                                                               | Desmarcado                                                                                                                                                                                                                                                                                                                              |
| Etapa de la cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Un solo clic alterna la inhabilitación de la etapa de RX; un doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. El intervalo de discriminación de clic es configurable mediante `InteractionSettings`; consulte [Personalizar el intervalo de discriminación de clic](#personalizar-el-intervalo-de-discriminación-de-clic) a continuación.                                                  | Delegado a ClientRxChainWidget. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo MIME distinto 'application/x-aethersdr-rx-chain-stage' evita colocaciones accidentales entre las dos tiras.                    |
| Estado ADSP / mosaico de inhabilitación                     | Mosaico interactivo del lado de RX que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic inhabilita todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado anterior de NR. Un doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de la instantánea vuelve a NR2 si no había módulos activos en el momento de la inhabilitación.                                                                                                  |
| Estado RADIO                                                | Marcador final no interactivo del lado de RX. Se vuelve verde cuando PC Audio (la transmisión SSB estándar) está habilitado.                                                                                                                                                                                                                                                                                                        | Solo visible en modo RX.                                                                                                                                                                                                                                                                                                                |
| Estado SPEAK                                                | Marcador final no interactivo del lado de RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.                                                                                                                                                                                                                                                                                                           | Solo visible en modo RX.                                                                                                                                                                                                                                                                                                                |

## Personalizar el intervalo de discriminación de clic

El applet utiliza un intervalo configurable para distinguir entre un solo clic y un doble clic en cualquier etapa de la cadena. De forma predeterminada, este intervalo coincide con el tiempo de doble clic del sistema operativo.

### Pasos

1. Abra el menú principal: **Settings > Interaction Settings**.
2. En el campo **Click discrimination interval**, ingrese un valor en milisegundos (rango: 100–1000 ms).
3. Haga clic en **Save** o presione Enter. El cambio surte efecto de inmediato; no es necesario reiniciar.

Un intervalo más corto hace que la detección de doble clic sea más sensible, pero puede provocar acciones de un solo clic accidentales durante dobles clics rápidos. Un intervalo más largo facilita la realización de inhabilitaciones con un solo clic, pero puede parecer lento al hacer doble clic para editar.

## Consejos

- TX y RX mantienen instantáneas de BYPASS separadas. Activar BYPASS en la cadena de RX no afecta la cadena de TX, y viceversa.
- Si alterna manualmente una etapa individual mientras BYPASS está marcado, ese cambio se conserva fuera de la instantánea y no se revertirá cuando desmarque BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue el lado de la cadena que esté visible actualmente. Cambie a TX y luego a RX para confirmar el estado de BYPASS de RX de un vistazo.
- El estado de BYPASS tanto para TX como para RX pertenece al motor de audio. En el lado de TX, el botón BYPASS se comparte con Aetherial Audio Channel Strip; activar o desactivar TX BYPASS desde Channel Strip actualiza el botón BYPASS en el applet Aetherial Audio Chain automáticamente, y viceversa. De manera similar, el estado de BYPASS de RX se sincroniza con el motor, por lo que cualquier cambio realizado a través de otros controles se reflejará al ver la cadena de RX.
- El mosaico RADIO se vuelve verde cuando PC Audio (la transmisión SSB estándar) está habilitado. El mosaico SPEAK se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.

## Solución de problemas

- **BYPASS aparece marcado pero algunas etapas siguen activas** — Es posible que haya alternado etapas individuales manualmente después de activar BYPASS. Esos cambios manuales son independientes de la instantánea. Desmarque y vuelva a marcar BYPASS para tomar una instantánea nueva de los estados actuales de las etapas.
- **Al hacer clic en BYPASS se vuelven a habilitar etapas que no esperaba** — La instantánea se tomó cuando se marcó BYPASS por primera vez. Solo se restauran las etapas que estaban habilitadas en ese momento. Las etapas que deshabilitó antes de activar BYPASS permanecerán apagadas.
- **El estado del botón TX BYPASS no coincide con lo que configuró en Channel Strip** — El applet se sincroniza con el motor de audio cuando se muestra el lado de TX. Haga clic en **TX** para cambiar a la cadena de TX; el botón BYPASS reflejará el estado actual del motor de inmediato.
- **El estado del botón RX BYPASS no coincide con lo que espera** — El estado de RX BYPASS también pertenece al motor. Haga clic en **RX** para cambiar a la cadena de RX; el botón BYPASS reflejará el estado actual del motor. Si el estado del motor se cambió en otro lugar, el botón se actualiza automáticamente al ver la cadena de RX.
- **Al hacer clic en una etapa se alterna la inhabilitación cuando pretendía editar, o se abre el editor cuando pretendía inhabilitar** — Ajuste el intervalo de discriminación de clic en **Settings > Interaction Settings**. Un intervalo más largo ayuda si abre editores accidentalmente al intentar inhabilitar; un intervalo más corto ayuda si inhabilita accidentalmente al intentar editar.

## Relacionado

- [Inhabilitar todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Reactivar una etapa específica después de una inhabilitación global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas de TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
- Interaction Settings
