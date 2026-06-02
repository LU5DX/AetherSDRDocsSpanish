# Ver el pronóstico de Kp a 3 días y el riesgo de apagón

El Panel de Propagación de HF incluye una cuadrícula de pronóstico de Kp a 3 días que muestra la actividad geomagnética en períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio y tormenta de radiación de la NOAA para cada día. Utilícelo para planificar sesiones de operación en torno a condiciones perturbadas o aurora.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el diálogo del Panel de Propagación de HF.
2. Desplácese hasta la sección **3-Day Forecast grid**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: verde indica condiciones tranquilas (Kp inferior a 3), amarillo indica condiciones inestables (Kp 3–4) y rojo indica actividad a nivel de tormenta (Kp 5 o superior).
4. Verifique las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio y tormenta de radiación de la NOAA por día.
5. Lea el texto de **Rationale** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Revise las etiquetas de resumen — **Geomagnetic field**, **Solar wind**, **Noise** y **X-ray** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas durante tres días, más el Kp máximo por día. Las celdas están codificadas por colores según la gravedad. |
| Fila **R1-R2** | Riesgo de apagón de radio HF de la NOAA en el nivel R1–R2, mostrado por día. |
| Fila **R3+** | Riesgo de apagón de radio HF de la NOAA en el nivel R3 y superior, mostrado por día. |
| Fila **S1+** | Riesgo de tormenta de radiación solar de la NOAA en el nivel S1 y superior, mostrado por día. |
| **Rationale** | Explicación en lenguaje sencillo del pronóstico de hoy. |
| **Geomagnetic field / Solar wind / Noise / X-ray** | Etiquetas de estado de resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la gravedad. |

## Consejos

- El diálogo guarda y restaura automáticamente su tamaño y posición entre sesiones de AetherSDR. No hay una configuración separada para el modo sin marco.
- Un Kp de 5 o superior indica actividad geomagnética a nivel de tormenta. Las rutas polares y de latitudes altas son las más afectadas. Las bandas de HF más bajas (40m, 80m) tienden a mantenerse mejor que las bandas superiores durante tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certeza. Verifique los colores de las celdas de Kp en los períodos individuales de 3 horas para ver cuándo durante el día el riesgo es más alto.
- Pase el cursor sobre las tarjetas de **Current Conditions** (SFI, SN, A-index, K-index, X-ray) para obtener explicaciones emergentes de cada índice.
- La apariencia del diálogo se adapta al tema actual de AetherSDR. Las líneas separadoras y los fondos utilizan los colores del tema en lugar de valores fijos.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o muestra valores desactualizados** — AetherSDR obtiene los datos del pronóstico de internet. Verifique que su conexión de red esté activa y vuelva a abrir el diálogo.
- **No se recuerda la posición o el tamaño de la ventana** — El diálogo usa `PersistentDialog` para almacenar su geometría bajo la clave `PropDashboardDialogGeometry`. Si el archivo de configuración está dañado, cierre AetherSDR, elimine la entrada `PropDashboardDialogGeometry` de su archivo de configuración y vuelva a abrir el diálogo.

## Relacionado

- [Descripción general del Panel de Propagación de HF](overview.md)
- [Consultar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decidir qué banda de HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Observar aperturas de esporádica-E o aurorales en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
