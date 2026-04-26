# Omitir todas las etapas de TX a la vez

Use el control BYPASS para silenciar toda la cadena DSP de TX en un solo clic — útil cuando desea una señal seca y sin procesar para una comparación rápida o para diagnosticar una etapa de procesamiento.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrar el contenedor "Aetherial Audio".
- La cadena TX debe ser el lado activo. Si actualmente se muestra RX, haga clic en TX en el encabezado del applet para cambiar.

## Pasos

1. Abra el applet Aetherial Audio Chain haciendo clic en el botón PUDU de la bandeja en la barra lateral derecha si el applet no está visible todavía.
2. Haga clic en TX en el encabezado del applet para activar la cadena TX. TX usa resaltado ámbar cuando está seleccionado.
3. Haga clic en BYPASS.

   Todas las etapas de la cadena TX (EQ, COMP, GATE, DESS, TUBE, PUDU, VERB) se deshabilitan a la vez. BYPASS permanece marcado con un borde ámbar para indicar que la cadena está omitida.

4. Para restaurar el procesamiento, haga clic en BYPASS nuevamente.

   Solo las etapas que estaban habilitadas antes de activar BYPASS se vuelven a habilitar. Cualquier etapa que haya activado o desactivado manualmente mientras BYPASS estaba activo no se incluye en la restauración.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Ajuste persistente |
|---------|---------|----------|-------------------|
| TX | Marcado | Muestra y edita la cadena DSP de TX. Resaltado ámbar cuando está activo. | `PooDooAudioActiveTab` |
| RX | Sin marcar | Muestra y edita la cadena DSP de RX. TX y RX mantienen instantáneas de BYPASS independientes. | `PooDooAudioActiveTab` |
| BYPASS | Sin marcar | Marcado: toma una instantánea de las etapas TX habilitadas en ese momento y las deshabilita todas. Sin marcar: vuelve a habilitar solo las etapas que estaban activas antes. | — (no persistente) |

## Sugerencias

- BYPASS actúa únicamente sobre el lado que se muestra en ese momento. Activar BYPASS mientras se muestra TX no tiene ningún efecto sobre la cadena RX, y viceversa.
- Si activa o desactiva etapas individuales mientras BYPASS está marcado, esos cambios manuales se conservan fuera de la instantánea y no se revertirán al desmarcar BYPASS.
- El orden de las etapas de la cadena TX (y el estado habilitado de cada etapa) persiste mediante `ClientCompTxChainStages`.

## Solución de problemas

- **BYPASS está marcado pero aún se escucha procesamiento** — Confirme que TX sea la pestaña activa. Si RX está seleccionado, BYPASS se aplica a la cadena RX, no a TX. Haga clic en TX y verifique el estado de BYPASS nuevamente.
- **Después de desmarcar BYPASS, hay menos etapas activas de las esperadas** — Una etapa que ya estaba deshabilitada antes de activar BYPASS no será restaurada por BYPASS, ya que no formaba parte de la instantánea.

## Temas relacionados

- [Omitir todas las etapas de RX a la vez](bypass-every-rx-stage-at-once.md)
- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Descripción general de Aetherial Audio Chain](overview.md)
