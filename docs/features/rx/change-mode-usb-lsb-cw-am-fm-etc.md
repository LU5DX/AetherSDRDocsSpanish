# Cambiar el modo (USB, LSB, CW, AM, FM, etc.)

Esta página explica cómo cambiar el modo de demodulación de un slice. Al cambiar el modo, los preajustes de filtro y los tamaños de paso de sintonía se adaptan automáticamente al nuevo modo.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet RX Controls requiere una conexión activa con el equipo.
- Abra el applet RX Controls si no está visible. Haga clic en el botón RX del área de notificación en la barra lateral derecha, o confirme que el panel de applets esté visible mediante `View > Applet Panel`.

## Pasos

1. Si tiene más de un slice, haga clic en la pestaña correcta (de A hasta H) en la parte superior del applet RX Controls para seleccionar el slice que desea modificar.
2. Localice el **Mode combo** en el applet RX Controls. Muestra el modo actual (predeterminado: **USB**).
3. Haga clic en el **Mode combo** para abrir la lista de modos.
4. Seleccione el modo deseado de la lista.

El modo del slice cambia de inmediato. Los botones de preajuste de filtro se actualizan para mostrar anchos apropiados para el nuevo modo, y la lista de pasos de sintonía se restablece a los valores predeterminados de cada modo.

## Qué hace cada control

| Control | Predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|
| Mode combo | USB | USB, LSB, CW, AM, SAM, FM, NFM, DFM, DIGU, DIGL, RTTY | Establece el modo de demodulación del slice. Adapta los preajustes de filtro y los tamaños de paso al modo seleccionado. |
| Preajustes de ancho de filtro | — | USB/LSB: 1800/2100/2400/2700/2900/3300 Hz; AM/SAM: 5600–14000 Hz; CW: 50/100/250/400 Hz; DIGU/DIGL: 100–2000 Hz; RTTY: 250–1000 Hz | Los botones de preajuste se actualizan automáticamente al cambiar el modo. No se muestran para FM, NFM ni DFM. Se guardan como `FilterPresets`. |
| STEP | 100 Hz (índice 2) | SSB: 1/10/50/100/500/1000/2000/3000 Hz; CW: 1/5/10/50/100/200/400 Hz; FM: 50/250/500/2500/3000/5000/10000/12500 Hz (otros varían) | La lista de pasos se restablece a los valores por modo al cambiar el modo. Use los botones **<** / **>** o la rueda del ratón para recorrer los pasos. |

## Consejos

- Los modos de la familia FM (FM, NFM, DFM) no muestran botones de preajuste de filtro. En su lugar, aparecen los controles de tono CTCSS y desplazamiento de repetidor cuando se selecciona uno de estos modos.
- Los controles de modo AGC se ocultan en los modos de la familia FM.
- Después de cambiar a CW, verifique el indicador QSK. Se ilumina en ámbar cuando el break-in de CW está activo, reflejando el estado configurado en el applet CW.

## Solución de problemas

- **El modo RADE no aparece en la lista** — RADE requiere una versión especial de AetherSDR. La versión instalada no lo incluye.
- **Los botones de preajuste de filtro no aparecen después de cambiar el modo** — Esto es normal para FM, NFM y DFM. Esos modos no utilizan preajustes de filtro variables.
- **Los tamaños de paso no son correctos después de un cambio de modo** — El control STEP se restablece a los valores predeterminados por modo al cambiar el modo. Use los botones **<** / **>** para seleccionar el tamaño de paso deseado.

## Relacionado

- [Seleccionar un preajuste de ancho de filtro para el modo actual](pick-a-filter-width-preset-for-the-current-mode.md)
- [Trabajar un repetidor FM con tono CTCSS y desplazamiento +/-](work-an-fm-repeater-with-ctcss-tone-and-offset.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Descripción general de RX Controls](overview.md)
