# Ver el pronóstico de Kp a 3 días y el riesgo de apagón

El Panel de propagación de HF incluye una cuadrícula de pronóstico de Kp a 3 días que muestra la actividad geomagnética en períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio y tormenta de radiación de la NOAA para cada día. Utilícelo para planificar sesiones de operación en torno a condiciones perturbadas o auroras.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el diálogo del Panel de propagación de HF.
2. Desplácese hasta la sección **3-Day Forecast grid**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: verde indica condiciones tranquilas (Kp inferior a 3), amarillo indica condiciones inestables (Kp 3–4) y rojo indica actividad a nivel de tormenta (Kp 5 o superior).
4. Verifique las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio y tormenta de radiación de la NOAA por día.
5. Lea el texto de **Rationale** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Revise las etiquetas de resumen — **Geomagnetic field**, **Solar wind**, **Noise** y **X-ray** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Función de cada control

| Control | Comportamiento |
|---|---|
| **3-Day Forecast grid** | Muestra Kp por período UTC de 3 horas durante tres días, más el Kp máximo por día. Las celdas están codificadas por colores según la severidad. |
| Fila **R1-R2** | Riesgo de apagón de radio de HF de la NOAA a nivel R1–R2, mostrado por día. |
| Fila **R3+** | Riesgo de apagón de radio de HF de la NOAA a nivel R3 y superior, mostrado por día. |
| Fila **S1+** | Riesgo de tormenta de radiación solar de la NOAA a nivel S1 y superior, mostrado por día. |
| **Rationale** | Explicación en lenguaje sencillo del pronóstico del día actual. |
| **Geomagnetic field / Solar wind / Noise / X-ray** | Etiquetas de estado de resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la severidad. |

## Consejos

- Un Kp de 5 o superior indica actividad geomagnética a nivel de tormenta. Las rutas polares y de latitudes altas son las más afectadas. Las bandas bajas de HF (40m, 80m) tienden a resistir mejor que las bandas altas durante las tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certeza. Verifique los colores de las celdas de Kp en períodos individuales de 3 horas para ver cuándo durante el día el riesgo es más alto.
- Pase el cursor sobre las tarjetas de **Current Conditions** (SFI, SN, A-index, K-index, X-ray) para ver explicaciones emergentes de cada índice.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o valores desactualizados** — AetherSDR obtiene los datos del pronóstico desde internet. Verifique que su conexión de red esté activa y vuelva a abrir el diálogo.

## Relacionados

- [HF Propagation Dashboard overview](overview.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decide which HF band is open for day or night work](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Watch for VHF sporadic-E or auroral openings](watch-for-vhf-sporadic-e-or-auroral-openings.md)
