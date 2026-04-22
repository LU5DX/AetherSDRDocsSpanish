# Omitir todas las etapas de TX a la vez

El botón BYPASS desactiva todas las etapas activas de la cadena DSP de TX en un solo clic y las restaura con otro clic. Úselo para comparar el audio de TX procesado y sin procesar sin necesidad de alternar cada etapa manualmente.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- TX debe estar seleccionado en el applet de cadena. El selector TX está marcado de forma predeterminada; si en cambio está seleccionado RX, BYPASS no tiene ningún efecto.

## Pasos

1. Confirme que el selector TX está marcado en la fila de encabezado del applet PooDoo Audio Chain. El botón se ilumina en ámbar cuando está activo.
2. Haga clic en BYPASS.
3. AetherSDR toma una instantánea de las etapas actualmente habilitadas y las desactiva todas. El botón BYPASS se ilumina en ámbar para indicar que el bypass está activo.
4. Haga clic en BYPASS nuevamente para restaurar las etapas que estaban habilitadas antes de activar el bypass.

## Qué hace cada control

| Control | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|
| TX | Marcado | Muestra y edita la cadena DSP de TX. BYPASS opera únicamente sobre esta cadena. | — |
| RX | Desmarcado | Cambia a la vista de marcador de posición de RX. BYPASS no tiene efecto en este modo. | — |
| BYPASS | Desmarcado | Marcado: toma una instantánea de las etapas habilitadas y las desactiva todas. Desmarcado: reactiva únicamente las etapas que estaban activas antes. | `ClientCompTxChainStages` |

## Consejos

- Las etapas que se alternan individualmente mientras BYPASS está activo no forman parte de la instantánea. Al desmarcar BYPASS, solo se restauran las etapas que estaban activas en el momento en que se activó el bypass.
- El botón PUDU de la bandeja controla la visibilidad del contenedor PooDoo Audio completo, que se guarda en `Applet_TXDSP`.

## Solución de problemas

- **Hacer clic en BYPASS no tiene efecto** — Verifique que TX esté seleccionado y no RX. En modo RX, BYPASS no hace nada, ya que la cadena RX aún no está implementada.
- **BYPASS restaura menos etapas de las esperadas** — Cualquier etapa que se haya desactivado manualmente mientras BYPASS estaba activo fue eliminada de la instantánea y no se restaurará automáticamente. Vuelva a habilitarla haciendo clic directamente en esa etapa.

## Relacionados

- [Reactivar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
