# Descripción general del applet PooDoo Audio Chain

El applet PooDoo Audio Chain muestra el flujo de señal DSP de TX como una tira horizontal de etapas de procesamiento. Úselo para omitir, reordenar o abrir editores de etapas individuales, y para capturar una breve muestra de audio posterior al procesamiento y auditar su sonido de TX.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para activarlo.
- No se requiere conexión a radio para ver o configurar la cadena. Algunas funciones (grabar, reproducir) requieren que la fuente de entrada del micrófono esté configurada en PC con DAX desactivado.

## Cómo funciona

El applet aparece como la sección superior del contenedor TXDSP. Tiene dos capas: una fila de encabezado con controles y, debajo de ella, la tira de cadena.

**Fila de encabezado**

La fila de encabezado contiene los botones de modo, los botones de monitor y el botón BYPASS, de izquierda a derecha.

- **TX** y **RX** son botones de alternancia exclusivos que seleccionan qué vista de cadena se muestra. TX está seleccionado de forma predeterminada (resaltado en ámbar). Al seleccionar RX se muestra el texto de marcador de posición "Client RX chain — coming in a future phase"; no hay procesamiento de etapas disponible en esa vista.
- El botón **Record** (⏺) y el botón **Play** (▶) son los controles de grabación del monitor post-PUDU, descritos a continuación.
- **BYPASS** se encuentra en el extremo derecho de la fila de encabezado.

**Tira de cadena**

Debajo del encabezado, cada etapa DSP aparece como un mosaico arrastrable en el orden del flujo de señal. El orden predeterminado de las etapas es: Eq, Comp, Gate, DeEss, Tube, Enh (PUDU), Reverb. Una línea de ayuda estática debajo de la tira indica "Click to bypass · Double click to edit · Drag to reorder".

Cada mosaico de etapa responde a tres interacciones:

| Interacción | Resultado |
|---|---|
| Clic simple | Activa o desactiva el bypass solo para esa etapa |
| Doble clic | Abre el editor flotante de esa etapa |
| Arrastrar | Mueve la etapa a una nueva posición en la cadena |

El orden de la cadena y los estados de habilitación de las etapas se guardan en `ClientCompTxChainStages`. Si el contenedor TXDSP se muestra o no, se guarda en `Applet_TXDSP`.

## Qué hace cada control

| Control | Predeterminado | Comportamiento |
|---|---|---|
| **TX** | Seleccionado | Muestra la cadena DSP de TX interactiva. Resaltado en ámbar cuando está activo. |
| **RX** | No seleccionado | Muestra el marcador de posición de RX. BYPASS no tiene efecto en este modo. |
| **BYPASS** | Sin marcar | Cuando se marca: toma una instantánea de las etapas habilitadas en ese momento y las deshabilita todas. Cuando se desmarca: vuelve a habilitar solo las etapas que estaban activas antes de la instantánea. Las etapas alternadas individualmente mientras BYPASS estaba activo no se ven afectadas por la restauración. |
| **Record** (⏺) | Deshabilitado | Captura hasta 30 segundos de audio TX post-PUDU. Haga clic de nuevo para detener antes; la reproducción comienza automáticamente al detenerse la grabación. Se habilita solo cuando la entrada de micrófono está configurada en PC y la reproducción no está activa. Parpadea en rojo mientras graba. |
| **Play** (▶) | Deshabilitado | Reproduce el audio capturado más recientemente. Haga clic de nuevo para cancelar. Se habilita solo cuando existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. |
| **Etapa de cadena (Eq)** | — | Clic simple activa o desactiva el bypass del ecualizador; doble clic abre el editor de EQ; arrastre para reordenar. |
| **Etapa de cadena (Comp)** | — | Clic simple activa o desactiva el bypass del compresor; doble clic abre el editor del compresor; arrastre para reordenar. |
| **Etapa de cadena (Gate)** | — | Clic simple activa o desactiva el bypass del gate; doble clic abre el editor del gate; arrastre para reordenar. |
| **Etapa de cadena (DeEss)** | — | Clic simple activa o desactiva el bypass del de-esser; doble clic abre el editor del de-ess; arrastre para reordenar. |
| **Etapa de cadena (Tube)** | — | Clic simple activa o desactiva el bypass del saturador de tubo; doble clic abre el editor del tubo; arrastre para reordenar. |
| **Etapa de cadena (Enh / PUDU)** | — | Clic simple activa o desactiva el bypass del excitador PUDU; doble clic abre el editor PUDU; arrastre para reordenar. |
| **Etapa de cadena (Reverb)** | — | Clic simple activa o desactiva el bypass del reverb; doble clic abre el editor del reverb; arrastre para reordenar. |

## Consejos

- El indicador de punto final TX parpadea en rojo en la tira de cadena mientras su slice está transmitiendo (MOX activo), lo que le proporciona una confirmación en tiempo real de que TX está activo.
- BYPASS está diseñado para comparaciones A/B rápidas. Dado que toma una instantánea de las etapas habilitadas en el momento en que lo activa, puede alternar etapas individuales de forma segura durante un bypass sin perder su configuración original al restaurar.
- El botón Record requiere que la fuente del micrófono esté configurada en PC y que DAX esté desactivado. Si el botón aparece atenuado, verifique primero esas dos condiciones.

## Relacionados

- [Omitir todas las etapas de TX a la vez](bypass-every-tx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Reordenar la cadena DSP de TX](reorder-the-tx-dsp-chain.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Reproducir el audio PUDU capturado](play-back-the-captured-pudu-audio.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Confirmar visualmente cuando TX (MOX) está activo](visually-confirm-when-tx-mox-is-live.md)
