# Decida qué banda de HF está abierta para trabajo diurno o nocturno

El Panel de Propagación de HF muestra un resumen del estado por banda dividido en columnas de día y noche, permitiéndole elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- El panel obtiene datos de servicios externos de propagación; se necesita una conexión a internet para datos en vivo.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Desplácese a la sección **HF Band Conditions** del diálogo.
3. Lea el estado mostrado para cada una de las cuatro filas de banda bajo las columnas **Day** y **Night**.
4. Elija una banda cuyo estado coincida con su hora actual del día (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **HF Band Conditions** | Muestra una calificación de estado para cada una de las cuatro filas de banda de HF, dividida en columnas de día y noche. |
| Valor del estado de la banda | Muestra uno de tres estados: **Good**, **Fair** o **Poor**, codificado con colores verde, ámbar o naranja respectivamente. |

## Consejos

- Las **Current Conditions cards** en la parte superior del diálogo muestran los valores de SFI, SN, índice A, índice K y rayos X. Compare estos con los estados de banda: un SFI alto (120 o superior) generalmente favorece las bandas altas de HF, mientras que un índice K alto (5 o superior) indica actividad geomagnética a nivel de tormenta que degrada muchas rutas.
- Pase el cursor sobre cualquier tarjeta métrica para leer un mensaje emergente en lenguaje sencillo que explica qué significa ese índice para la propagación de HF.
- Si el índice A está elevado (15 o superior), los estados de banda pueden permanecer inestables incluso si el índice K actual parece tranquilo.

## Solución de problemas

- **Todos los valores de estado de banda aparecen en blanco o no se actualizan** — el panel no pudo recuperar datos de propagación. Verifique su conexión a internet y vuelva a abrir el diálogo.

## Relacionado

- [HF Propagation Dashboard overview](overview.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [See the 3-day Kp forecast and blackout risk](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Watch for VHF sporadic-E or auroral openings](watch-for-vhf-sporadic-e-or-auroral-openings.md)
