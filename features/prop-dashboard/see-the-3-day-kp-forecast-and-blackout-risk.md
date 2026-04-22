# Ver el pronóstico de Kp de 3 días y el riesgo de apagón

El Panel de Propagación HF incluye una cuadrícula de pronóstico de Kp de 3 días que muestra la actividad geomagnética a lo largo de períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio y tormenta de radiación de la NOAA para cada día. Utilice esto para planificar sesiones de operación en torno a condiciones perturbadas o aurora.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el diálogo del Panel de Propagación HF.
2. Desplácese hasta la sección **3-Day Forecast grid**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: el verde indica condiciones tranquilas (Kp por debajo de 3), el amarillo indica condiciones inestables (Kp 3–4) y el rojo indica actividad de nivel de tormenta (Kp 5 o superior).
4. Revise las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio y tormenta de radiación de la NOAA por día.
5. Lea el texto **Rationale** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Revise las etiquetas de resumen — **Geomagnetic field**, **Solar wind**, **Noise** y **X-ray** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **3-Day Forecast grid** | Muestra el Kp por período UTC de 3 horas a lo largo de tres días, más el Kp máximo por día. Las celdas están codificadas por colores según la severidad. |
| Fila **R1-R2** | Riesgo de apagón de radio HF de la NOAA en el nivel R1–R2, mostrado por día. |
| Fila **R3+** | Riesgo de apagón de radio HF de la NOAA en el nivel R3 y superior, mostrado por día. |
| Fila **S1+** | Riesgo de tormenta de radiación solar de la NOAA en el nivel S1 y superior, mostrado por día. |
| **Rationale** | Explicación en lenguaje sencillo del pronóstico del día. |
| **Geomagnetic field / Solar wind / Noise / X-ray** | Etiquetas de estado de resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la severidad. |

## Consejos

- Un Kp de 5 o superior indica actividad geomagnética de nivel de tormenta. Las rutas polares y de altas latitudes son las más afectadas. Las bandas HF bajas (40m, 80m) tienden a mantenerse mejor que las bandas altas durante las tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certezas. Revise los colores de las celdas de Kp en los períodos individuales de 3 horas para ver en qué momento del día el riesgo es mayor.
- Pase el cursor sobre las tarjetas **Current Conditions cards** (SFI, SN, A-index, K-index, X-ray) para ver explicaciones en globos de ayuda de cada índice.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o muestra valores desactualizados** — AetherSDR obtiene los datos del pronóstico desde internet. Verifique que su conexión de red esté activa y vuelva a abrir el diálogo.

## Relacionado

- [Descripción general del Panel de Propagación HF](overview.md)
- [Verificar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decidir qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Estar atento a aperturas esporádicas-E en VHF o aperturas aurorales](watch-for-vhf-sporadic-e-or-auroral-openings.md)
