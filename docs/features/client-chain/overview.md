# Descripción general de la cadena de audio Aetherial

La cadena de audio Aetherial es el pipeline DSP del lado del cliente de AetherSDR. Permite moldear tanto el audio transmitido como el recibido mediante una secuencia de etapas de procesamiento que puede reordenar, omitir individualmente o desactivar todas a la vez, sin modificar la configuración DSP propia del radio.

## Antes de comenzar

- Abra el contenedor de audio Aetherial haciendo clic en el botón de bandeja PUDU en el panel derecho de applets. El applet de cadena siempre es visible como la sección superior de ese contenedor cuando está habilitado.
- No se requiere una conexión de radio para configurar la cadena, pero el procesamiento de audio solo tiene efecto cuando hay audio fluyendo.

## Cómo funciona

El applet presenta dos cadenas de procesamiento independientes — TX y RX — en una tira horizontal de bloques de etapas (tiles). Use los botones de alternancia TX y RX para cambiar cuál cadena se muestra y edita. Solo una cadena es visible a la vez; ambas conservan su propio orden de etapas, estados de omisión y configuraciones del editor de forma independiente.

### Cadena TX

La cadena TX se ejecuta de izquierda a derecha a través de hasta siete etapas:

| Etapa | Descripción |
|---|---|
| EQ | Ecualizador paramétrico aplicado al audio saliente |
| COMP | Compresor |
| GATE | Puerta de ruido |
| DESS | Desibilador |
| TUBE | Saturación de tubo |
| PUDU | Procesamiento de voz PooDoo™ |
| VERB | Reverberación |

### Cadena RX

La cadena RX se ejecuta a través de hasta cinco etapas controlables por el usuario, flanqueadas por tres tiles de estado de solo lectura:

| Etapa / Tile | Descripción |
|---|---|
| Tile de estado RADIO | Indica si PC Audio (la transmisión SSB estándar) está habilitado |
| EQ | Ecualizador de recepción |
| GATE | Puerta AGC-T |
| COMP | Compresor AGC-C |
| TUBE | Tubo dinámico |
| PUDU | Procesamiento de recepción PooDoo™ |
| Tile de estado DSP | Refleja el reductor de ruido activo (p. ej., NR2, NR4, BNR); muestra DSP cuando ninguno está activo |
| Tile de estado SPEAK | Indica si la salida de audio de AetherSDR no está silenciada |

Los tiles RADIO, DSP y SPEAK son indicadores no interactivos. Aparecen solo cuando se muestra la cadena RX.

### Interacción con las etapas

Cada tile de etapa admite tres interacciones, resumidas en la línea de ayuda debajo de la cadena:

- **Clic simple** — activa o desactiva la omisión solo de esa etapa.
- **Doble clic** — abre el editor flotante sin marco de la etapa.
- **Arrastrar** — reordena la cadena. Una barra vertical de color cian entre los tiles indica dónde se colocará la etapa antes de soltar. TX y RX usan tipos de arrastre separados, por lo que una etapa TX no puede caer accidentalmente en la cadena RX.

### BYPASS global

BYPASS desactiva todas las etapas de la cadena actualmente visible a la vez. Al marcar BYPASS, AetherSDR guarda un instantáneo de las etapas que estaban habilitadas y las desactiva todas. Desmarcar BYPASS reactiva exactamente esas etapas. Las etapas que se alterne manualmente mientras BYPASS está marcado no se incluyen en el instantáneo. TX y RX mantienen instantáneos de bypass independientes; el estado mostrado refleja el lado que esté visible en ese momento.

### Monitor TX post-PUDU

Dos pequeños botones de icono a la derecha de los botones de alternancia TX/RX permiten grabar y reproducir una captura breve del audio de transmisión tal como sale de la etapa PUDU:

- El botón **⏺** (Record) captura hasta 30 segundos de audio TX post-PUDU. Haga clic de nuevo para detener antes; la reproducción comienza automáticamente. Pulsa en rojo mientras graba. Solo está habilitado cuando la entrada de micrófono está configurada en PC y DAX está desactivado, y la reproducción no está en curso.
- El botón **▶** (Play) reproduce la última captura. Haga clic de nuevo para cancelar. Pulsa en verde mientras reproduce. Solo está habilitado una vez que existe una grabación y la grabación no está activa.

Ambos botones están ocultos cuando se muestra la cadena RX.

### Indicador de actividad TX

Mientras transmite (MOX activo), la tira de la cadena TX pulsa en rojo para confirmar la ruta de transmisión en vivo.

## Qué hace cada control

| Control | Tipo | Predeterminado | Configuración persistida | Notas |
|---|---|---|---|---|
| TX | Botón de alternancia | Marcado | `PooDooAudioActiveTab` | Muestra y edita la cadena TX. Resaltado ámbar cuando está seleccionado. La última pestaña activa persiste como `TX` o `RX`. |
| RX | Botón de alternancia | Desmarcado | `PooDooAudioActiveTab` | Muestra y edita la cadena RX, incluidos los tiles de estado RADIO / DSP / SPEAK. |
| BYPASS | Botón de alternancia | Desmarcado | — | Guarda un instantáneo y desactiva todas las etapas habilitadas en la cadena activa. Desmarcar para restaurarlas. Los instantáneos de TX y RX son independientes. |
| ⏺ (Record) | Botón de alternancia | Desmarcado | — | Graba hasta 30 s de audio TX post-PUDU. Haga clic de nuevo para detener. Pulsa en rojo mientras está activo. Solo TX. |
| ▶ (Play) | Botón de alternancia | Desmarcado | — | Reproduce el audio capturado. Haga clic de nuevo para cancelar. Pulsa en verde mientras está activo. Solo TX. |
| Tiles de etapas de cadena TX / RX | Manejadores de arrastre | — | `ClientCompTxChainStages` / `ClientCompRxChainStages` | Clic simple para omitir, doble clic para editar, arrastrar para reordenar. |
| Tile de estado RADIO | Indicador | — | — | Se pone verde cuando PC Audio está habilitado. Solo en modo RX. |
| Tile de estado DSP | Indicador | — | — | Muestra el nombre corto del reductor de ruido activo (p. ej., NR2, NR4, BNR), o DSP cuando ninguno está activo. Solo en modo RX. |
| Tile de estado SPEAK | Indicador | — | — | Se pone verde cuando la salida de audio de AetherSDR no está silenciada. Solo en modo RX. |

La configuración `Applet_TXDSP` controla si el contenedor de audio Aetherial (que aloja este applet) se muestra en absoluto.

## Consejos

- Los órdenes de las cadenas TX y RX se guardan de forma independiente. Reordenar una cadena no afecta a la otra.
- Puede arrastrar las etapas al orden que desee en cualquiera de las cadenas. El indicador de inserción cian muestra el punto de inserción exacto antes de soltar.
- La grabadora post-PUDU es útil para verificar cómo suena su cadena de procesamiento sin necesitar una segunda estación. Asegúrese de que la fuente de micrófono esté configurada en PC y que DAX esté desactivado antes de grabar, o el botón Record permanecerá deshabilitado.
- BYPASS es por cadena. Marcar BYPASS mientras se visualiza TX no afecta el estado de bypass de la cadena RX.

## Solución de problemas

- **El botón ⏺ (Record) está atenuado** — La entrada de micrófono no está configurada en PC, DAX está habilitado o la reproducción está en curso. Verifique la configuración de entrada de audio y asegúrese de que DAX esté desactivado antes de intentar grabar.
- **Arrastrar una etapa TX no la coloca sobre la tira RX** — Esto es por diseño. Las dos cadenas usan tipos de arrastre incompatibles para evitar caídas accidentales entre cadenas.
- **BYPASS está marcado pero algunas etapas siguen omitidas después de desmarcarlo** — Las etapas que alternó manualmente mientras BYPASS estaba activo no forman parte del instantáneo y no se restaurarán automáticamente. Reactívelas individualmente.

## Relacionados

- [Cambiar entre editar las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Reordenar la cadena DSP de RX (independiente del orden de TX)](reorder-the-rx-dsp-chain-independent-of-tx-order.md)
- [Abrir el editor flotante sin marco de una etapa desde la cadena](open-a-stage-s-frameless-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Ver de un vistazo si PC Audio, el reductor de ruido y la salida de audio están activos (tiles de estado RX)](see-at-a-glance-whether-pc-audio-the-noise-reducer-and-audio-output-are-live-rx-status-tiles.md)
- [Confirmar visualmente cuando TX (MOX) está en vivo](visually-confirm-when-tx-mox-is-live.md)
