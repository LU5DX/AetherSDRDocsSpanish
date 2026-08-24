# Decida qué banda de HF está abierta para trabajo diurno o nocturno

El Panel de propagación de HF muestra un resumen de condiciones por banda dividido en columnas de día y noche, permitiéndole elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- El panel obtiene datos de servicios de propagación externos; se necesita una conexión a internet para datos en vivo.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de propagación de HF.
2. Desplácese hasta la sección **HF Band Conditions** del diálogo.
3. Lea la condición mostrada para cada una de las cuatro filas de bandas bajo las columnas **Day** y **Night**.
4. Elija una banda cuya condición coincida con su hora actual del día (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Current Conditions cards** | Cinco mosaicos de métricas (SFI, SN, índice A, índice K, rayos X) con información emergente al pasar el cursor. |
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas para cada uno de los tres días, además de filas de riesgo Max Kp, R1-R2, R3+ y S1+. |
| **Solar And Lunar panel** | Imagen solar en vivo (haga clic para alternar longitudes de onda) y fase lunar actual. Etiqueta predeterminada 'Corona (193A)'. |
| **What To Look For** | Notas educativas rotativas en lenguaje sencillo sobre la imagen solar actual. |
| **HF Band Conditions** | Muestra una calificación de condición para cada una de las cuatro filas de bandas de HF, dividida en columnas de día y noche. |
| Valor de condición de banda | Muestra uno de tres estados: **Good**, **Fair** o **Poor**, codificados con colores verde, ámbar o naranja respectivamente. |
| **VHF Conditions** | Estados de Aurora, E-Skip NA, E-Skip EU. |
| **What These Mean (VHF)** | Dos notas educativas que explican aurora frente a esporádica-E. |

## Consejos

- Las **Current Conditions cards** en la parte superior del diálogo muestran valores de SFI, SN, índice A, índice K y rayos X. Compare estos con las condiciones de banda: un SFI alto (120 o superior) generalmente favorece las bandas altas de HF, mientras que un índice K alto (5 o superior) indica actividad geomagnética a nivel de tormenta que degrada muchas rutas.
- Pase el cursor sobre cualquier tarjeta de métrica para leer una información emergente en lenguaje sencillo que explica qué significa ese índice para la propagación de HF.
- Si el índice A está elevado (15 o superior), las condiciones de banda pueden permanecer inestables incluso si el índice K actual parece tranquilo.
- El **Solar And Lunar panel** le permite alternar entre longitudes de onda solares haciendo clic en la imagen. La vista predeterminada es 'Corona (193A)'.
- El **3-Day Forecast grid** incluye celdas Kp codificadas por color en períodos UTC, además de riesgos de apagón NOAA (R1-R2, R3+) y tormenta de radiación (S1+) por día.

## Solución de problemas

- **Todos los valores de condición de banda aparecen en blanco o no se actualizan** — el panel no pudo recuperar datos de propagación. Verifique su conexión a internet y vuelva a abrir el diálogo.
- **La ventana del panel no se reposiciona correctamente entre sesiones** — el diálogo guarda y restaura su geometría automáticamente. Si la posición es incorrecta, redimensione o mueva la ventana a una nueva ubicación, luego ciérrela y vuelva a abrirla para guardar la geometría actualizada.
- **Los datos del panel dejan de actualizarse o parecen desactualizados** — el panel utiliza un tiempo de espera de red de 15 segundos para las recuperaciones de clima espacial. Si el servicio de propagación es lento o inaccesible, los paneles afectados pueden permanecer en blanco. Verifique su conexión a internet y vuelva a abrir el diálogo para reintentar.

## Relacionados

- [Descripción general del Panel de propagación de HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Esté atento a aperturas de esporádica-E o aurora en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
