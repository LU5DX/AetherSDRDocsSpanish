# Seleccionar un preajuste de ancho de filtro para el modo actual

Los preajustes de ancho de filtro permiten aplicar un ancho de banda estándar al slice (receptor parcial) activo con un solo clic, adaptado al modo actual. Úselos para cambiar rápidamente entre anchos de filtro amplios y estrechos sin arrastrar los bordes de la banda de paso manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- El applet RX debe estar abierto. Si no es visible, haga clic en el botón RX del panel lateral derecho para mostrarlo.
- Seleccione el slice que desea ajustar usando las pestañas de slice (A..H) en la parte superior del applet RX.

## Pasos

1. Verifique el **Mode combo** para confirmar que el slice está configurado en el modo deseado. Los preajustes de filtro son por modo; cambiar el modo después del paso 2 modificará la forma de los preajustes.
2. Localice la fila de botones de preajuste de ancho de filtro en el applet RX. El ancho de filtro actual se muestra en el indicador **2.7K** de la fila de encabezado.
3. Haga clic en el botón de preajuste correspondiente al ancho de banda que desea. El indicador **2.7K** se actualiza de inmediato para reflejar el ancho aplicado.
4. Para guardar el ancho de filtro actual como preajuste, haga clic derecho sobre cualquier botón de preajuste y elija guardar el ancho actual en esa posición. El valor se almacena bajo `FilterPresets`.

## Qué hace cada control

| Control | Comportamiento | Valores válidos | Clave persistente |
|---|---|---|---|
| Preajustes de ancho de filtro | Haga clic para aplicar un ancho de filtro preajustado al slice activo. Haga clic derecho para guardar el ancho actual como preajuste. | Consulte los rangos por modo a continuación. | `FilterPresets` |
| **2.7K** (indicador de ancho de filtro) | Muestra el ancho de banda de filtro actual en kHz o Hz. Se actualiza al aplicar un preajuste o al arrastrar la banda de paso. | Solo lectura. | — |
| Widget de banda de paso del filtro | Arrastre el borde inferior o superior para establecer un ancho de filtro personalizado fuera de los preajustes. | — | — |

### Valores de preajuste por modo

| Modo | Anchos de preajuste disponibles |
|---|---|
| USB, LSB | 1800, 2100, 2400, 2700, 2900, 3300 Hz |
| AM, SAM | 5600, 6000, 8000, 10000, 12000, 14000 Hz |
| CW | 50, 100, 250, 400 Hz |
| DIGU, DIGL | 100, 300, 600, 1000, 1500, 2000 Hz |
| RTTY | 250, 300, 350, 400, 500, 1000 Hz |
| FM, NFM, DFM | No se muestran botones de preajuste. |

## Consejos

- Los botones de preajuste se ocultan completamente cuando el slice está en modo FM, NFM o DFM. Cambie a un modo no-FM para verlos.
- Para ajustar con precisión más allá de los preajustes, arrastre directamente el borde inferior o superior del widget de banda de paso del filtro.
- La configuración `FilterPresets` se guarda por modo, por lo que personalizar los preajustes de CW no afecta los preajustes de SSB.

## Solución de problemas

- **No se ven botones de preajuste** — El slice está en modo FM, NFM o DFM. Los preajustes de filtro no están disponibles para los modos de la familia FM. Cambie el modo usando el **Mode combo** para ver los preajustes.
- **Al hacer clic en un preajuste no ocurre nada** — Confirme que el slice no está bloqueado. Un ícono de candado cerrado (🔒) en la fila de encabezado indica que el slice ignora los cambios. Haga clic en el ícono del candado para desbloquearlo.

## Relacionado

- [Cambiar el modo (USB, LSB, CW, AM, FM, etc.)](change-mode-usb-lsb-cw-am-fm-etc.md)
- [Bloquear el slice para evitar el resintonizado accidental](lock-the-slice-to-prevent-accidental-retuning.md)
- [Descripción general de los controles RX](overview.md)
