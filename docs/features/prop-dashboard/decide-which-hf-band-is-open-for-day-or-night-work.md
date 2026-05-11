# Decida qué banda de HF está abierta para trabajo diurno o nocturno

El Panel de propagación de HF muestra un resumen del estado de cada banda dividido en columnas de día y noche, permitiéndole elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- El panel obtiene datos de servicios externos de propagación; se necesita conexión a internet para datos en vivo.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de propagación de HF.
2. Desplácese hasta la sección **HF Band Conditions** del diálogo.
3. Lea el estado que se muestra para cada una de las cuatro filas de bandas bajo las columnas **Day** y **Night**.
4. Elija una banda cuyo estado coincida con su hora actual del día (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Current Conditions cards** | Cinco tarjetas de métricas (SFI, SN, A-index, K-index, X-ray) con información en tooltip al pasar el ratón. |
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas para cada uno de los tres días, más filas de riesgo Max Kp, R1-R2, R3+ y S1+. |
| **Solar And Lunar panel** | Imagen solar en vivo (haga clic para cambiar longitudes de onda) y fase lunar actual. Etiqueta predeterminada 'Corona (193A)'. |
| **What To Look For** | Notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual. |
| **HF Band Conditions** | Muestra una calificación de estado para cada una de las cuatro filas de bandas de HF, dividida en columnas de día y noche. |
| Valor del estado de la banda | Muestra uno de tres estados: **Good**, **Fair** o **Poor**, codificados con colores verde, ámbar o naranja respectivamente. |
| **VHF Conditions** | Estados de Aurora, E-Skip NA, E-Skip EU. |
| **What These Mean (VHF)** | Dos notas de aprendizaje que explican aurora vs esporádica-E. |

## Consejos

- Las **Current Conditions cards** en la parte superior del diálogo muestran valores de SFI, SN, A-index, K-index y X-ray. Compare estos con las condiciones de la banda: un SFI alto (120 o superior) generalmente favorece las bandas altas de HF, mientras que un K-index alto (5 o superior) indica actividad geomagnética de tormenta que degrada muchos trayectos.
- Pase el ratón sobre cualquier tarjeta de métrica para leer un tooltip en lenguaje sencillo que explica qué significa ese índice para la propagación de HF.
- Si el A-index está elevado (15 o superior), las condiciones de la banda pueden permanecer inestables incluso si el K-index actual parece tranquilo.
- El **Solar And Lunar panel** permite cambiar entre longitudes de onda solares haciendo clic en la imagen. La vista predeterminada es 'Corona (193A)'.
- La **3-Day Forecast grid** incluye celdas Kp con código de colores en períodos UTC, más riesgos de apagón NOAA (R1-R2, R3+) y tormenta de radiación (S1+) por día.

## Solución de problemas

- **Todos los valores de estado de la banda aparecen en blanco o no se actualizan** — el panel no pudo obtener datos de propagación. Verifique su conexión a internet y vuelva a abrir el diálogo.
- **La ventana del panel no aparece con una barra de título o no se puede mover** — En algunas plataformas, el diálogo usa un estilo de ventana sin marco. Haga clic y arrastre en cualquier lugar del área del cuerpo (excepto controles interactivos) para reposicionar la ventana.

## Relacionados

- [HF Propagation Dashboard overview](overview.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [See the 3-day Kp forecast and blackout risk](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Watch for VHF sporadic-E or auroral openings](watch-for-vhf-sporadic-e-or-auroral-openings.md)
