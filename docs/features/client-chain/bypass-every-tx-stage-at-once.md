# Omitir todas las etapas de TX a la vez

El botón BYPASS desactiva todas las etapas activas en la cadena DSP de TX con un solo clic y las restaura con la misma rapidez. Úselo cuando necesite una ruta de señal limpia y sin procesamiento, sin modificar la configuración individual de cada etapa.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para mostrarlo.
- El botón de modo **TX** debe estar seleccionado (está seleccionado de forma predeterminada). BYPASS no tiene efecto en el modo RX.

## Pasos

1. Ubique la fila de encabezado del applet PooDoo Audio Chain. Contiene los botones **TX**, **RX** y **BYPASS**.
2. Haga clic en **BYPASS**.
   - El botón se resalta con un borde y relleno ámbar, lo que confirma que está activo.
   - AetherSDR toma una instantánea de las etapas que estaban habilitadas en ese momento y las desactiva todas.
3. Para restaurar la cadena, haga clic en **BYPASS** nuevamente.
   - Cada etapa que estaba habilitada antes de activar BYPASS se vuelve a habilitar.
   - Las etapas que activó o desactivó manualmente mientras BYPASS estaba activo no se ven afectadas por la restauración.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| **TX** | Botón de alternancia | Activado | Muestra la cadena DSP de TX; requerido para que BYPASS tenga efecto. | — |
| **RX** | Botón de alternancia | Desactivado | Cambia al marcador de posición de la cadena RX. BYPASS no tiene efecto en este modo. | — |
| **BYPASS** | Botón de alternancia | Desactivado | Activado: toma una instantánea de las etapas habilitadas en ese momento y las desactiva todas. Desactivado: vuelve a habilitar exactamente las etapas que estaban activas antes de la instantánea. | `ClientCompTxChainStages` |

La clave `Applet_TXDSP` conserva el estado de visibilidad del contenedor PooDoo Audio.

## Consejos

- Si activa o desactiva manualmente una etapa mientras BYPASS está activo, ese cambio se conserva al desactivar BYPASS. Solo se restaura la instantánea original, no sus ajustes manuales.
- La información emergente del botón BYPASS indica: "Disable every stage in the selected chain. Click again to restore the stages that were on before."

## Solución de problemas

- **BYPASS parece no hacer nada** — Confirme que el botón **TX** esté seleccionado. BYPASS no tiene efecto cuando **RX** está activo.
- **Algunas etapas no se volvieron a habilitar tras desactivar BYPASS** — Es probable que esas etapas se hayan activado o desactivado manualmente mientras BYPASS estaba activo. Su nuevo estado se conserva por diseño. Vuelva a habilitarlas individualmente haciendo clic en cada etapa de la cadena.

## Temas relacionados

- [Volver a habilitar una etapa específica después de un bypass global](re-enable-a-specific-stage-after-a-global-bypass.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Cambiar entre la vista de cadena TX y el marcador de posición RX](switch-between-tx-chain-view-and-rx-placeholder.md)
