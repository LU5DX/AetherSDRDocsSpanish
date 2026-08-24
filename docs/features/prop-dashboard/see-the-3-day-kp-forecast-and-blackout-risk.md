# Consulte el pronóstico de Kp a 3 días y el riesgo de apagón de radio

El Panel de Propagación de HF incluye una cuadrícula de pronóstico de Kp a 3 días que muestra la actividad geomagnética en períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio y tormenta de radiación de la NOAA para cada día. Úsela para planificar sesiones de operación en torno a condiciones perturbadas o auroras.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión activa a internet para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el diálogo del Panel de Propagación de HF.
2. Desplácese hasta la sección de la **cuadrícula de pronóstico a 3 días**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: verde indica condiciones tranquilas (Kp inferior a 3), amarillo indica condiciones inestables (Kp 3–4) y rojo indica actividad a nivel de tormenta (Kp 5 o superior).
4. Revise las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio y tormenta de radiación de la NOAA por día.
5. Lea el texto de **Rationale** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Consulte las etiquetas de resumen — **Geomagnetic field**, **Solar wind**, **Noise** y **X-ray** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Current Conditions cards** | Cinco mosaicos de métricas (SFI, SN, A-index, K-index, X-ray) que muestran los índices solares/geomagnéticos actuales con información emergente al pasar el cursor. |
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas durante tres días, además del Kp máximo por día. Las celdas están codificadas por colores según la severidad. |
| **Solar And Lunar panel** | Imagen solar en vivo (haga clic para alternar longitudes de onda; etiqueta predeterminada 'Corona (193A)') y fase lunar actual. |
| **What To Look For** | Notas educativas rotativas en lenguaje sencillo sobre la imagen solar actual. |
| **HF Band Conditions** | Condiciones de día y noche por fila de banda (4 filas de banda). |
| **VHF Conditions** | Estados de apertura de aurora, E-Skip NA y E-Skip EU. |
| **What These Mean (VHF)** | Dos notas educativas que explican aurora frente a E esporádica. |
| **R1-R2** row | Riesgo de apagón de radio HF de la NOAA en el nivel R1–R2, mostrado por día. |
| **R3+** row | Riesgo de apagón de radio HF de la NOAA en el nivel R3 y superior, mostrado por día. |
| **S1+** row | Riesgo de tormenta de radiación solar de la NOAA en el nivel S1 y superior, mostrado por día. |
| **Geomagnetic field / Solar wind / Noise / X-ray** | Etiquetas de estado de resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la severidad. |
| **Rationale** | Explicación en lenguaje sencillo del pronóstico de hoy. |

## Consejos

- El diálogo guarda y restaura automáticamente su tamaño y posición entre sesiones de AetherSDR. No hay una configuración separada para el modo sin marco.
- Un Kp de 5 o superior señala actividad geomagnética a nivel de tormenta. Las rutas polares y de latitudes altas son las más afectadas. Las bandas HF más bajas (40 m, 80 m) tienden a mantenerse mejor que las bandas superiores durante tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certeza. Revise los colores de las celdas de Kp en los períodos individuales de 3 horas para ver cuándo durante el día el riesgo es mayor.
- Pase el cursor sobre las **Current Conditions cards** (SFI, SN, A-index, K-index, X-ray) para obtener explicaciones emergentes de cada índice.
- La apariencia del diálogo se adapta a su tema actual de AetherSDR. Las líneas separadoras y los fondos usan colores del tema en lugar de valores fijos.
- Si los datos del pronóstico no se cargan en 15 segundos, el panel detiene la descarga y puede reintentar cerrando y volviendo a abrir el diálogo.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o muestra valores desactualizados** — AetherSDR obtiene los datos del pronóstico de internet. Verifique que su conexión de red esté activa y vuelva a abrir el diálogo. Las descargas expiran después de 15 segundos si el servidor no responde.
- **No se recuerda la posición o el tamaño de la ventana** — El diálogo usa `PersistentDialog` para almacenar su geometría bajo la clave `PropDashboardDialogGeometry`. Si el archivo de configuración está dañado, cierre AetherSDR, elimine la entrada `PropDashboardDialogGeometry` de su archivo de configuración y vuelva a abrir el diálogo.

## Relacionado

- [Descripción general del Panel de Propagación de HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decida qué banda HF está abierta para trabajo de día o de noche](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Esté atento a aperturas de E esporádica o auroras en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
