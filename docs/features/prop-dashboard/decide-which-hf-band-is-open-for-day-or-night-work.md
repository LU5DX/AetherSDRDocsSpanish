# Decida qué banda de HF está abierta para trabajo diurno o nocturno

El Panel de Propagación de HF muestra un resumen del estado por banda, dividido en columnas de día y noche, permitiéndole elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- El panel obtiene datos de servicios de propagación externos; se necesita conexión a internet para datos en vivo.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Desplácese hasta la sección **HF Band Conditions** del diálogo.
3. Lea el estado mostrado para cada una de las cuatro filas de banda bajo las columnas **Day** y **Night**.
4. Elija una banda cuyo estado coincida con su hora actual del día (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Current Conditions cards** | Cinco indicadores métricos (SFI, SN, A-index, K-index, X-ray) con información emergente al pasar el ratón. |
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas para cada uno de los tres días, más las filas de riesgo Max Kp, R1-R2, R3+ y S1+. |
| **Solar And Lunar panel** | Imagen solar en vivo (haga clic para cambiar longitudes de onda) y fase lunar actual. Etiqueta predeterminada 'Corona (193A)'. |
| **What To Look For** | Notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual. |
| **HF Band Conditions** | Muestra una calificación de estado para cada una de las cuatro filas de banda de HF, divididas en columnas de día y noche. |
| Valor de estado de banda | Muestra uno de tres estados: **Good**, **Fair** o **Poor**, codificado con colores verde, ámbar o naranja respectivamente. |
| **VHF Conditions** | Estados de Aurora, E-Skip NA, E-Skip EU. |
| **What These Mean (VHF)** | Dos notas de aprendizaje que explican aurora frente a E esporádica. |

## Consejos

- Las **Current Conditions cards** en la parte superior del diálogo muestran valores de SFI, SN, A-index, K-index y X-ray. Compare estos con las condiciones de banda: un SFI alto (120 o superior) generalmente favorece las bandas altas de HF, mientras que un K-index alto (5 o superior) indica actividad geomagnética de tormenta que degrada muchas trayectorias.
- Pase el ratón sobre cualquier tarjeta métrica para leer una descripción emergente en lenguaje sencillo que explica lo que ese índice significa para la propagación de HF.
- Si el A-index está elevado (15 o superior), las condiciones de banda pueden permanecer inestables incluso si el K-index actual parece tranquilo.
- El **Solar And Lunar panel** le permite recorrer las longitudes de onda solares haciendo clic en la imagen. La vista predeterminada es 'Corona (193A)'.
- La **3-Day Forecast grid** incluye celdas de Kp codificadas por color en períodos UTC, más el riesgo de apagón NOAA (R1-R2, R3+) y tormenta de radiación (S1+) por día.

## Solución de problemas

- **Todos los valores de condición de banda aparecen en blanco o no se actualizan** — el panel no pudo recuperar datos de propagación. Verifique su conexión a internet y vuelva a abrir el diálogo.
- **La ventana del panel no se reposiciona correctamente entre sesiones** — el diálogo guarda y restaura su geometría automáticamente. Si la posición es incorrecta, redimensione o mueva la ventana a una nueva ubicación, luego ciérrela y vuélvala a abrir para guardar la geometría actualizada.

## Relacionado

- [HF Propagation Dashboard overview](overview.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [See the 3-day Kp forecast and blackout risk](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Watch for VHF sporadic-E or auroral openings](watch-for-vhf-sporadic-e-or-auroral-openings.md)
