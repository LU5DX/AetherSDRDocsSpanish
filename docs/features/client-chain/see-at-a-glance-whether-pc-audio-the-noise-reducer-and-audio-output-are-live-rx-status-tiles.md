# Ver de un vistazo si el audio de PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)

La vista de la cadena RX en el applet Aetherial Audio Chain incluye tres indicadores de estado no interactivos — RADIO, DSP y SPEAK — que muestran el estado en tiempo real de la ruta de recepción de señal sin necesidad de abrir ningún cuadro de diálogo.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para habilitarlo.
- Debe estar visualizando la cadena RX. Los indicadores de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Aetherial Audio Chain no está visible.
2. En el encabezado del applet, haga clic en **RX**. La tira de la cadena RX reemplaza a la tira de la cadena TX, y los tres indicadores de estado aparecen a ambos lados de las etapas de procesamiento.
3. Lea los tres indicadores de izquierda a derecha:
   - **RADIO** — se ilumina en verde cuando el audio de PC (la transmisión SSB estándar) está habilitado en la radio.
   - **DSP** — refleja cuál reductor de ruido del lado del cliente está activo en ese momento. La etiqueta rota al nombre abreviado del módulo activo (por ejemplo, `NR2`, `NR4` o `BNR`). Cuando ningún reductor de ruido está activado, la etiqueta del indicador vuelve a mostrar `DSP`.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

No se requiere ninguna acción adicional. Los indicadores se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Indicador | Tipo | Comportamiento | Visible |
|-----------|------|----------------|---------|
| **RADIO** | Indicador | Se ilumina en verde cuando el audio de PC está habilitado. | Solo en modo RX |
| **DSP** | Indicador | La etiqueta rota al nombre abreviado del reductor de ruido activo (`NR2`, `NR4`, `BNR`); muestra `DSP` cuando ninguno está activo. Se ilumina en verde cuando hay un reductor de ruido activado. | Solo en modo RX |
| **SPEAK** | Indicador | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. | Solo en modo RX |

Ninguno de los tres indicadores es interactivo. El clic simple, el doble clic y el arrastre no tienen ningún efecto sobre ellos.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el siguiente inicio mediante la configuración guardada `PooDooAudioActiveTab`. Si desea que los indicadores de estado RX estén visibles de forma predeterminada, deje la pestaña **RX** seleccionada al cerrar AetherSDR.
- El cambio de la etiqueta del indicador **DSP** a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activado, sin necesidad de abrir `Settings > AetherDSP Settings...`.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Alternar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Omitir todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
