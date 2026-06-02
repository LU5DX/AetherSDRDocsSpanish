# Omitir todas las etapas de RX a la vez

Use el botón BYPASS para deshabilitar todas las etapas de la cadena de RX de un solo clic, sin perder de vista qué etapas estaban activas. Al hacer clic nuevamente en BYPASS, solo se restauran las etapas que estaban habilitadas antes.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrar el contenedor.
- Debe estar viendo la cadena de RX. El botón BYPASS actúa sobre el lado de la cadena que se muestra actualmente.

## Pasos

1. En el encabezado del applet Aetherial Audio Chain, haga clic en **RX**. Las etapas de la cadena de RX aparecen debajo.
2. Haga clic en **BYPASS**. El botón cambia a su apariencia activada (borde y relleno ámbar). Cada etapa en la cadena de RX se deshabilita de inmediato, incluido RN2. AetherSDR toma una instantánea de qué etapas estaban habilitadas en el momento en que hizo clic.
3. Para restaurar los estados anteriores de las etapas, haga clic nuevamente en **BYPASS**. Solo se vuelven a habilitar las etapas que estaban habilitadas antes de la omisión.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Notas |
|---------|------|---------------|----------------|-------|
| **RX** | Botón de alternancia | Desmarcado | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — completamente interactivo con clic para omitir, doble clic para editar, arrastrar para reordenar; enmarcado por los mosaicos de estado RADIO / DSP / SPEAK. | Es parte de un par exclusivo con TX; estilo de borde azul cuando está seleccionado. Cada lado mantiene un estado de etapa independiente, orden de cadena e instantánea de BYPASS. |
| **BYPASS** | Botón de alternancia | Desmarcado | Marcado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas (incluido RN2). Desmarcado: vuelve a habilitar solo las etapas que estaban antes. La instantánea es global (por motor de audio), no por perfil — el botón permanece presionado al cambiar de perfil de Channel Strip. | Las etapas alternadas manualmente mientras BYPASS estaba activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas separadas — el estado visual marcado sigue el lado que se muestra actualmente. |
| Etapa de cadena RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Asa de arrastre | Ninguno | Un solo clic alterna la omisión de la etapa RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. | Delegado a ClientRxChainWidget. Las seis etapas RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena TX. El tipo mime distintivo 'application/x-aethersdr-rx-chain-stage' evita caídas no deseadas entre las dos tiras. |
| Mosaico de estado RADIO | Indicador | Ninguno | Extremo no interactivo del lado RX. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. | Solo visible en modo RX. |
| Mosaico de estado/omisión ADSP | Botón de alternancia | Desmarcado | Mosaico interactivo del lado RX que refleja cuál reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (p. ej., 'NR2', 'NR4', 'BNR'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic omite todo el clúster NR con una instantánea en memoria; otro clic restaura el estado NR anterior. El doble clic abre el cuadro de diálogo AetherDSP Settings. | Solo visible en modo RX. Adopta el mismo estilo de borde azul + punto LED verde que las etapas implementadas. La restauración de la instantánea vuelve a NR2 si no había módulos activos al momento de la omisión. |
| Mosaico de estado SPEAK | Indicador | Ninguno | Extremo no interactivo del lado RX. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. | Solo visible en modo RX. |

## Personalizar el intervalo de discriminación de clics

El applet utiliza un intervalo configurable para distinguir entre un solo clic y un doble clic en cualquier etapa de la cadena. De forma predeterminada, este intervalo coincide con el tiempo de doble clic del sistema operativo.

### Pasos

1. Abra el menú principal: **Settings > Interaction Settings**.
2. En el campo **Click discrimination interval**, ingrese un valor en milisegundos (rango: 100–1000 ms).
3. Haga clic en **Save** o presione Enter. El cambio surte efecto de inmediato; no es necesario reiniciar.

Un intervalo más corto hace que la detección de doble clic sea más sensible, pero puede provocar acciones de un solo clic accidentales durante dobles clics rápidos. Un intervalo más largo facilita la ejecución de omisiones con un solo clic, pero puede sentirse lento al hacer doble clic para editar.

## Consejos

- TX y RX mantienen instantáneas de BYPASS separadas. Activar BYPASS en la cadena RX no afecta a la cadena TX, y viceversa.
- Si alterna manualmente una etapa individual mientras BYPASS está marcado, ese cambio se conserva fuera de la instantánea y no se revertirá al desmarcar BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue el lado de la cadena que está visible actualmente. Cambie a TX y luego a RX para confirmar el estado de BYPASS de RX de un vistazo.
- El estado de BYPASS tanto para TX como para RX es propiedad del motor de audio. En el lado TX, el botón BYPASS se comparte con el Aetherial Audio Channel Strip: activar o desactivar BYPASS de TX desde el Channel Strip actualiza el botón BYPASS en el applet Aetherial Audio Chain automáticamente, y viceversa. De manera similar, el estado de BYPASS de RX se sincroniza con el motor, por lo que cualquier cambio realizado a través de otros controles se reflejará al ver la cadena RX.
- BYPASS es global (por motor de audio), no por perfil. Si cambia de perfil de Channel Strip mientras BYPASS está activo, el botón BYPASS permanece marcado y continúa deshabilitando todas las etapas independientemente del perfil cargado.
- El mosaico RADIO se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. El mosaico SPEAK se vuelve verde cuando la salida de audio de AetherSDR no está silenciada.

## Solución de problemas

- **BYPASS aparece marcado pero algunas etapas siguen activas** — Es posible que haya alternado etapas individuales manualmente después de activar BYPASS. Esos cambios manuales son independientes de la instantánea. Desmarque y vuelva a marcar BYPASS para tomar una instantánea nueva de los estados actuales de las etapas.
- **Al hacer clic en BYPASS se vuelven a habilitar etapas que no esperaba** — La instantánea se tomó cuando BYPASS se marcó por primera vez. Solo se restauran las etapas que estaban habilitadas en ese momento. Las etapas que deshabilitó antes de activar BYPASS permanecerán apagadas.
- **El estado del botón BYPASS de TX no coincide con lo que configuró en el Channel Strip** — El applet se sincroniza con el motor de audio cuando se muestra el lado TX. Haga clic en **TX** para cambiar a la cadena TX; el botón BYPASS reflejará el estado actual del motor de inmediato.
- **El estado del botón BYPASS de RX no coincide con lo que espera** — El estado de BYPASS de RX también es propiedad del motor. Haga clic en **RX** para cambiar a la cadena RX; el botón BYPASS reflejará el estado actual del motor. Si el estado del motor se cambió en otro lugar, el botón se actualiza automáticamente al ver la cadena RX.
- **BYPASS aparece desmarcado después de cambiar de perfil de Channel Strip** — El estado de BYPASS es por motor de audio, no por perfil. Si cambia de perfil, el botón BYPASS puede aparecer desmarcado incluso si el motor aún lo tiene activado. Haga clic en **RX** para actualizar la visualización, o simplemente vuelva a hacer clic en BYPASS para desactivarlo y activarlo.
- **RN2 permanece activo después de activar BYPASS** — En v26.6.1, BYPASS ahora deshabilita RN2 junto con todas las demás etapas. Si RN2 permanece activo, asegúrese de estar usando la versión más reciente y de que el botón BYPASS esté completamente marcado (borde y relleno ámbar).
- **Al hacer clic en una etapa se alterna la omisión cuando pretendía editar, o se abre el editor cuando pretendía omitir** — Ajuste el intervalo de discriminación de clics en **Settings > Interaction Settings**. Un intervalo más largo ayuda si abre editores accidentalmente al intentar omitir; un intervalo más corto ayuda si omite accidentalmente al intentar editar.

## Relacionados

- [Bypass every TX stage at once](bypass-every-tx-stage-at-once.md)
- [Re-enable a specific stage after a global bypass](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Switch between editing the TX and RX chains](switch-between-editing-the-tx-and-rx-chains.md)
- [Aetherial Audio Chain overview](overview.md)
- Interaction Settings
