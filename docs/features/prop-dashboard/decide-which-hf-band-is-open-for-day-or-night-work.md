# Determine qué banda de HF está abierta para trabajo de día o de noche

El Panel de Propagación de HF muestra un resumen de condiciones banda por banda dividido en columnas de día y noche, lo que le permite elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- El panel obtiene datos de servicios externos de propagación; se necesita una conexión a internet para obtener datos en tiempo real.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Desplácese hasta la sección **HF Band Conditions** del cuadro de diálogo.
3. Lea la condición mostrada para cada una de las cuatro filas de bandas bajo las columnas **Day** y **Night**.
4. Elija una banda cuya condición corresponda a su hora actual (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **HF Band Conditions** | Muestra una clasificación de condición para cada una de las cuatro filas de bandas de HF, dividida en columnas de día y noche. |
| Valor de condición de banda | Muestra uno de tres estados: **Good**, **Fair** o **Poor**, codificados en verde, ámbar o naranja, respectivamente. |

## Consejos

- Las tarjetas **Current Conditions** en la parte superior del cuadro de diálogo muestran los valores de SFI, SN, índice A, índice K y rayos X. Compárelos con las condiciones de banda: un SFI alto (120 o más) generalmente favorece las bandas superiores de HF, mientras que un índice K alto (5 o más) indica actividad geomagnética de nivel tormenta que degrada muchos trayectos.
- Pase el cursor sobre cualquier tarjeta de métrica para leer una descripción emergente en lenguaje sencillo que explica qué significa ese índice para la propagación en HF.
- Si el índice A es elevado (15 o más), las condiciones de banda pueden permanecer inestables incluso si el índice K actual parece tranquilo.

## Solución de problemas

- **Todos los valores de condición de banda aparecen en blanco o no se actualizan** — el panel no pudo recuperar los datos de propagación. Verifique su conexión a internet y vuelva a abrir el cuadro de diálogo.

## Relacionados

- [Descripción general del Panel de Propagación de HF](overview.md)
- [Consultar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp para 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Monitorear aperturas esporádicas-E o aurorales en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
