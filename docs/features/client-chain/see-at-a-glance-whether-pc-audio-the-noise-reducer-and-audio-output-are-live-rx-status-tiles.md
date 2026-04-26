# Vea de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)

La vista de la cadena RX incluye tres indicadores de estado no interactivos — RADIO, DSP y SPEAK — que muestran de un vistazo si la ruta de audio entrante está completamente activa. Úselos para confirmar que PC Audio está en funcionamiento, que hay un reductor de ruido activado y que la salida de audio no está silenciada, sin necesidad de abrir ningún diálogo de configuración.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón PUDU de la bandeja en la barra lateral derecha para mostrarlo.
- Debe estar viendo la cadena RX. Los tres indicadores de estado solo son visibles en modo RX.

## Pasos

1. Haga clic en el botón PUDU de la bandeja en la barra lateral derecha para abrir el contenedor Aetherial Audio si aún no está visible.
2. Haga clic en **RX** en el encabezado del applet. La tira de la cadena RX reemplaza la tira TX y los tres indicadores de estado aparecen en los extremos de la cadena.
3. Lea los tres indicadores:
   - **RADIO** — se ilumina en verde cuando PC Audio (la transmisión SSB estándar) está habilitado en la radio.
   - **DSP** — muestra el nombre abreviado del reductor de ruido activo (por ejemplo, `NR2`, `NR4` o `BNR`). Muestra `DSP` cuando no hay ningún reductor de ruido activado.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

## Qué hace cada control

| Indicador | Tipo | Visible | Comportamiento | Ajuste persistente |
|-----------|------|---------|----------------|--------------------|
| RADIO | Indicador | Solo en modo RX | Se ilumina en verde cuando PC Audio está habilitado | — |
| DSP | Indicador | Solo en modo RX | La etiqueta rota al nombre abreviado del reductor de ruido activo (p. ej., `NR2`, `NR4`, `BNR`); vuelve a `DSP` cuando ninguno está activo | — |
| SPEAK | Indicador | Solo en modo RX | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada | — |

Ninguno de los tres indicadores es interactivo. No es posible hacer clic en ellos para cambiar su estado.

## Consejos

- Si RADIO no está iluminado, PC Audio no está habilitado en el lado de la radio. Verifique la configuración de audio de su slice.
- Si DSP muestra `DSP` en lugar del nombre de un módulo, no hay ningún reductor de ruido del lado del cliente activo en este momento. Abra `Settings > AetherDSP Settings...` para configurar uno.
- Si SPEAK no está iluminado, la salida de audio de AetherSDR está silenciada. Reactive la salida de audio para restaurar el audio recibido.
- El ajuste `PooDooAudioActiveTab` conserva cuál cadena se mostró por última vez. Si AetherSDR se reabre en el lado TX, haga clic en **RX** una vez para volver a los indicadores de estado.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
