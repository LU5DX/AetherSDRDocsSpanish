# Evite todas las etapas de la cadena de RX de una sola vez

Use el botón **BYPASS** para deshabilitar todas las etapas de la cadena de RX con un solo clic, sin perder de vista qué etapas estaban activas. Al hacer clic de nuevo en **BYPASS**, solo se restauran las etapas que estaban habilitadas antes.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de la bandeja PUDU en la barra lateral derecha para mostrar el contenedor.
- Debe estar viendo la cadena de RX. El botón **BYPASS** actúa sobre el lado de la cadena que se muestra actualmente.

## Pasos

1. En el encabezado del applet Aetherial Audio Chain, haga clic en **RX**. Las etapas de la cadena de RX aparecen debajo.
2. Haga clic en **BYPASS**. El botón cambia a su apariencia activada (borde y relleno ámbar). Cada etapa en la cadena de RX se deshabilita inmediatamente, incluidos todos los módulos de reducción de ruido (NR2, NR4, MNR, DFNR, RN2, NVAFX). AetherSDR toma una instantánea de qué etapas estaban habilitadas en el momento en que hizo clic.
3. Para restaurar los estados anteriores de las etapas, haga clic en **BYPASS** nuevamente. Solo se re-habilitan las etapas que estaban habilitadas antes de la evasión.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Notas |
|---------|------|----------------|----------------|-------|
| **RX** | Botón de alternancia | Desmarcado | Muestra y edita la cadena DSP de RX (ClientRxChainWidget) — totalmente interactiva con clic para evadir, doble clic para editar, arrastrar para reordenar; flanqueada por los mosaicos de estado RADIO / DSP / SPEAK. | Parte de un par exclusivo con TX; color 'VUDU' ámbar cuando está seleccionado. Cada lado mantiene un estado de etapas, orden de cadena e instantánea BYPASS independientes. La última pestaña activa persiste mediante PooDooAudioActiveTab. |
| **BYPASS** | Botón de alternancia | Desmarcado | Marcado: toma una instantánea de las etapas actualmente habilitadas en el lado activo (TX o RX) y las deshabilita todas (incluidos todos los módulos de reducción de ruido). Desmarcado: re-habilita solo las etapas que estaban activas antes. La instantánea es global (por motor de audio), no por perfil — el botón permanece presionado al cambiar de perfil de Channel Strip. | Las etapas activadas manualmente mientras BYPASS estaba activo se conservan fuera de la instantánea. TX y RX mantienen instantáneas separadas — el estado visual marcado sigue el lado que se muestra actualmente. |
| Etapa de la cadena de RX (EQ / AGC-G / AGC-C / DESS / TUBE / EVO) | Asa de arrastre | Ninguno | Un solo clic alterna la evasión de la etapa de RX; doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena de RX. | Delegado a ClientRxChainWidget. Las seis etapas de RX (EQ, AGC-G/Gate, AGC-C/Comp, DESS/DeEss, TUBE, EVO/Pudu) están completamente implementadas. El orden es independiente de la cadena de TX. El tipo mime distintivo 'application/x-aethersdr-rx-chain-stage' evita caídas accidentales entre las dos tiras. |
| Mosaico de estado RADIO | Indicador | Ninguno | Flanco final del lado RX no interactivo. Se vuelve verde cuando PC Audio (el flujo SSB estándar) está habilitado. | Solo visible en modo RX. |
| Mosaico de estado/evasión ADSP | Botón de alternancia | Desmarcado | Mosaico del lado RX interactivo que refleja qué reductor de ruido del lado del cliente está activo actualmente. La etiqueta cambia al nombre corto del módulo activo (ej. 'NR2', 'NR4', 'NVAFX'); vuelve a 'ADSP' cuando ninguno está activo. Un solo clic evita todo el clúster NR con una instantánea en memoria; otro solo clic restaura el estado NR anterior. Doble clic abre el diálogo de configuración de AetherDSP. | Solo visible en modo RX. Adopta el mismo estilo de anillo azul + punto LED verde que los mosaicos de etapa implementados. La restauración de instantánea vuelve a NR2 si no había módulos activos en el momento de la evasión. La etiqueta 'BNR' ha sido reemplazada por 'NVAFX' en v26.7.4. |
| Mosaico de estado SPEAK | Indicador | Ninguno | Flanco final del lado RX no interactivo. Se vuelve verde cuando la salida de audio de AetherSDR no está silenciada. | Solo visible en modo RX. |

## Personalice el intervalo de discriminación de clics

El applet utiliza un intervalo configurable para distinguir entre un solo clic y un doble clic en cualquier etapa de la cadena. Por defecto, este intervalo coincide con el tiempo de doble clic del sistema operativo.

### Pasos

1. Abra el menú principal: **Settings > Interaction Settings**.
2. En el campo **Click discrimination interval**, ingrese un valor en milisegundos (rango: 100–1000 ms).
3. Haga clic en **Save** o presione Enter. El cambio surte efecto de inmediato — no se requiere reinicio.

Un intervalo más corto hace que la detección de doble clic sea más receptiva, pero puede provocar acciones accidentales de un solo clic durante dobles clics rápidos. Un intervalo más largo facilita realizar evasiones con un solo clic, pero puede sentirse lento al hacer doble clic para editar.

## Consejos

- TX y RX mantienen instantáneas BYPASS separadas. Activar BYPASS en la cadena de RX no afecta la cadena de TX, y viceversa.
- Si alterna manualmente una etapa individual mientras BYPASS está marcado, ese cambio se conserva fuera de la instantánea y no se revertirá cuando desmarque BYPASS.
- El estado marcado de BYPASS que se muestra en el encabezado sigue el lado de la cadena que esté visible actualmente. Cambie a TX y luego de vuelta a RX para confirmar el estado de BYPASS de RX de un vistazo.
- El estado BYPASS tanto para TX como para RX es propiedad del motor de audio. En el lado TX, el botón **BYPASS** se comparte con Aetherial Audio Channel Strip — activar o desactivar TX BYPASS desde Channel Strip actualiza automáticamente el botón **BYPASS** en el applet Aetherial Audio Chain, y viceversa. De manera similar, el estado BYPASS de RX se sincroniza con el motor, por lo que cualquier cambio realizado a través de otros controles se reflejará al visualizar la cadena de RX.
- BYPASS es global (por motor de audio), no por perfil. Si cambia de perfil de Channel Strip mientras BYPASS está activo, el botón BYPASS permanece marcado y continúa deshabilitando todas las etapas independientemente del perfil cargado.
- El mosaico RADIO se pone verde cuando PC Audio (el flujo SSB estándar) está habilitado. El mosaico SPEAK se pone verde cuando la salida de audio de AetherSDR no está silenciada.

## Solución de problemas

- **BYPASS aparece marcado pero algunas etapas aún están activas** — Es posible que haya alternado etapas individuales manualmente después de activar BYPASS. Esos cambios manuales son independientes de la instantánea. Desmarque y vuelva a marcar BYPASS para tomar una instantánea nueva de los estados actuales de las etapas.
- **Al hacer clic en BYPASS se re-habilitan etapas que no esperaba** — La instantánea se tomó cuando BYPASS se marcó por primera vez. Solo se restauran las etapas que estaban habilitadas en ese momento. Las etapas que deshabilitó antes de activar BYPASS permanecerán apagadas.
- **El estado del botón BYPASS de TX no coincide con lo que configuró en Channel Strip** — El applet se sincroniza con el motor de audio cuando se muestra el lado TX. Haga clic en **TX** para cambiar a la cadena TX; el botón BYPASS reflejará el estado actual del motor inmediatamente.
- **El estado del botón BYPASS de RX no coincide con lo que espera** — El estado BYPASS de RX también es propiedad del motor. Haga clic en **RX** para cambiar a la cadena RX; el botón BYPASS reflejará el estado actual del motor. Si el estado del motor se cambió en otro lugar, el botón se actualiza automáticamente al visualizar la cadena RX.
- **BYPASS aparece desmarcado después de cambiar perfiles de Channel Strip** — El estado BYPASS es por motor de audio, no por perfil. Si cambia de perfil, el botón BYPASS puede aparecer desmarcado aunque el motor aún lo tenga habilitado. Haga clic en **RX** para actualizar la visualización, o simplemente vuelva a hacer clic en BYPASS para desactivarlo y activarlo.
- **La reducción de ruido permanece activa después de activar BYPASS** — En v26.7.4, BYPASS ahora deshabilita NVAFX junto con todos los demás módulos de reducción de ruido. Si la reducción de ruido permanece activa, asegúrese de estar usando la última versión y que el botón BYPASS esté completamente marcado (borde y relleno ámbar).
- **La etiqueta del mosaico ADSP muestra 'BNR' en lugar de 'NVAFX'** — En v26.7.4, el módulo de reducción de ruido 'BNR' ha sido renombrado a 'NVAFX'. El mosaico ADSP ahora mostrará 'NVAFX' cuando ese módulo esté activo. Si ve 'BNR', es posible que necesite actualizar a la última versión.
- **Al hacer clic en una etapa se alterna la evasión cuando pretendía editar, o se abre el editor cuando pretendía evadir** — Ajuste el intervalo de discriminación de clics en **Settings > Interaction Settings**. Un intervalo más largo ayuda si abre editores accidentalmente al intentar evadir; un intervalo más corto ayuda si evade accidentalmente al intentar editar.

## Relacionados

- [Evite todas las etapas de TX de una sola vez](bypass-every-tx-stage-at-once.md)
- [Re-habilite una etapa específica después de una evasión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambie entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
- Configuración de interacción
