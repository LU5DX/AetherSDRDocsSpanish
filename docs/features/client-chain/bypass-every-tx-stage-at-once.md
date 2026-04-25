# Omitir todas las etapas de TX a la vez

El botón BYPASS desactiva todas las etapas activas de DSP de TX en un solo clic y las restaura con la misma rapidez. Úselo cuando desee comparar el audio procesado y sin procesar sin tener que activar o desactivar cada etapa manualmente.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja PUDU en la barra lateral derecha para mostrarlo.
- Asegúrese de que TX sea el modo activo. El botón de alternancia TX debe estar marcado (color ámbar). BYPASS no tiene efecto en el modo RX.

## Pasos

1. Localice la fila de encabezado del applet PooDoo Audio Chain. Verá los botones TX, RX y BYPASS.
2. Haga clic en BYPASS.
   - BYPASS queda marcado (borde y relleno de color ámbar).
   - Cada etapa que estaba habilitada se deshabilita. Las etapas de la cadena muestran su estado de omisión.
3. Para restaurar todas las etapas, haga clic en BYPASS nuevamente.
   - BYPASS vuelve al estado no marcado.
   - Solo se vuelven a habilitar las etapas que estaban habilitadas antes de hacer clic en BYPASS. Las etapas que ya habían sido omitidas individualmente antes de activar BYPASS permanecen omitidas.

## Qué hace cada control

| Control | Predeterminado | Comportamiento | Configuración persistente |
|---|---|---|---|
| TX | Marcado | Muestra y edita la cadena DSP de TX. BYPASS está activo en este modo. | — |
| RX | No marcado | Cambia al marcador de posición de la cadena RX. BYPASS no tiene efecto en este modo. | — |
| BYPASS | No marcado | Marcado: toma una instantánea de las etapas habilitadas en ese momento y las deshabilita todas. No marcado: vuelve a habilitar solo las etapas que estaban activas antes. | — |
| Etapa de cadena (Eq) | — | Un solo clic alterna la omisión de la etapa de EQ individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (Comp) | — | Un solo clic alterna la omisión del compresor individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (Gate) | — | Un solo clic alterna la omisión del gate individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (DeEss) | — | Un solo clic alterna la omisión del de-esser individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (Tube) | — | Un solo clic alterna la omisión del saturador de tubo individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (Enh / PUDU) | — | Un solo clic alterna la omisión del excitador PUDU individualmente. | `ClientCompTxChainStages` |
| Etapa de cadena (Reverb) | — | Un solo clic alterna la omisión del reverb individualmente. | `ClientCompTxChainStages` |

La visibilidad del contenedor TXDSP se persiste bajo `Applet_TXDSP`.

## Consejos

- Si alterna manualmente una etapa mientras BYPASS está marcado, el nuevo estado de esa etapa se conserva fuera de la instantánea. Desmarcar BYPASS no anulará una etapa que haya cambiado durante la omisión.
- BYPASS solo funciona en modo TX. Si RX está seleccionado, hacer clic en BYPASS no tiene efecto en ninguna etapa de DSP.

## Resolución de problemas

- **BYPASS está marcado pero las etapas no aparecen como omitidas** — Confirme que TX sea el modo activo y no RX. Haga clic en TX si es necesario y luego haga clic en BYPASS nuevamente.
- **Las etapas no se restauran después de desmarcar BYPASS** — Cualquier etapa que ya estuviera omitida individualmente antes de activar BYPASS no será restaurada; BYPASS solo restaura las etapas que estaban habilitadas en el momento en que se marcó.

## Relacionado

- [Volver a habilitar una etapa específica después de una omisión global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
- [Abrir el editor flotante de una etapa desde la cadena](open-a-stage-s-floating-editor-from-the-chain.md)
