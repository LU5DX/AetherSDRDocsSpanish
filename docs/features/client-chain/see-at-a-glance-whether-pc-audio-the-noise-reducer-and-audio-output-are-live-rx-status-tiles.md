# Consulte de un vistazo si el audio del PC, el reductor de ruido y la salida de audio están activos (indicadores de estado RX)

La vista de la cadena RX en el applet Aetherial Audio Chain incluye tres indicadores de estado no interactivos — RADIO, DSP y SPEAK — que muestran el estado en tiempo real de su ruta de señal de recepción sin necesidad de abrir ningún diálogo.

## Antes de comenzar

- El applet Aetherial Audio Chain debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado `PUDU` en la barra lateral derecha para habilitarlo.
- Debe estar visualizando la cadena RX. Los indicadores de estado solo son visibles cuando RX es la pestaña activa.

## Pasos

1. Haga clic en el botón de bandeja `PUDU` en la barra lateral derecha si el applet Aetherial Audio Chain no está visible todavía.
2. En el encabezado del applet, haga clic en **RX**. La tira de cadena RX reemplaza a la tira de cadena TX y aparecen los tres indicadores de estado a ambos lados de las etapas de procesamiento.
3. Lea los tres indicadores de izquierda a derecha:
   - **RADIO** — se ilumina en verde cuando el audio del PC (el flujo SSB estándar) está habilitado en el radio.
   - **DSP** — refleja qué reductor de ruido del lado del cliente está activo en ese momento. La etiqueta rota al nombre corto del módulo activo (por ejemplo, `NR2`, `NR4` o `BNR`). Cuando no hay ningún reductor de ruido activo, la etiqueta del indicador vuelve a mostrar `DSP`.
   - **SPEAK** — se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada.

No se requiere ninguna interacción adicional. Los indicadores se actualizan automáticamente a medida que cambian las condiciones.

## Qué hace cada control

| Indicador | Tipo | Comportamiento |
|---|---|---|
| **RADIO** | Indicador | Se ilumina en verde cuando el audio del PC está habilitado. |
| **DSP** | Indicador | La etiqueta rota al nombre corto del reductor de ruido activo (`NR2`, `NR4`, `BNR`); muestra `DSP` cuando ninguno está activo. Se ilumina en verde cuando hay un reductor de ruido activo. |
| **SPEAK** | Indicador | Se ilumina en verde cuando la salida de audio de AetherSDR no está silenciada. |
| Etapa de cadena RX (**EQ** / **AGC-T** / **AGC-C** / **TUBE** / **PUDU**) | Controlador de arrastre | Un clic simple activa o desactiva el bypass de la etapa RX; un doble clic abre su editor flotante sin marco en modo RX; arrastrar reordena la cadena RX. Las cinco etapas RX están completamente implementadas. El orden es independiente de la cadena TX. El tipo MIME distinto `application/x-aethersdr-rx-chain-stage` evita colocaciones accidentales entre las dos tiras. |

Ninguno de los tres indicadores es interactivo. El clic simple, el doble clic y el arrastre no tienen efecto sobre ellos.

## Consejos

- La última pestaña activa (TX o RX) se restaura en el próximo inicio mediante la configuración persistida `PooDooAudioActiveTab`. Si desea que los indicadores de estado RX estén visibles de forma predeterminada, deje la pestaña **RX** seleccionada al cerrar AetherSDR.
- El cambio de etiqueta del indicador **DSP** a un nombre específico (como `NR2`) es la forma más rápida de confirmar que un reductor de ruido está realmente activo, sin necesidad de abrir `Settings > AetherDSP Settings...`.
- Las etapas de puerta y compresor en la cadena RX están etiquetadas como **AGC-T** y **AGC-C** respectivamente. Estas corresponden internamente a las etapas Gate y Comp.

## Relacionados

- [Descripción general de Aetherial Audio Chain](overview.md)
- [Cambiar entre la edición de las cadenas TX y RX](switch-between-editing-the-tx-and-rx-chains.md)
- [Desactivar todas las etapas RX a la vez](bypass-every-rx-stage-at-once.md)
