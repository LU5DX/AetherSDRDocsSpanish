# Consulte el pronóstico de Kp a 3 días y el riesgo de apagón

El panel de propagación de HF incluye una cuadrícula de pronóstico de Kp a 3 días que muestra la actividad geomagnética en períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio y tormenta de radiación de la NOAA para cada día. Úselo para planificar sesiones de operación en torno a condiciones perturbadas o auroras.

## Antes de comenzar

- AetherSDR debe estar funcionando. No se requiere conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el diálogo del panel de propagación de HF.
2. Desplácese a la sección de la **cuadrícula de pronóstico a 3 días**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: verde indica condiciones tranquilas (Kp por debajo de 3), amarillo indica condiciones inestables (Kp 3–4) y rojo indica actividad de nivel de tormenta (Kp 5 o superior).
4. Revise las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio y tormenta de radiación de la NOAA por día.
5. Lea el texto de **Justificación** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Consulte las etiquetas de resumen — **Campo geomagnético**, **Viento solar**, **Ruido** y **Rayos X** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Función de cada control

| Control | Comportamiento |
|---|---|
| **Cuadrícula de pronóstico a 3 días** | Muestra Kp por período UTC de 3 horas durante tres días, además del Kp máximo por día. Las celdas están codificadas por colores según la severidad. |
| **Fila R1-R2** | Riesgo de apagón de radio HF de la NOAA en el nivel R1–R2, mostrado por día. |
| **Fila R3+** | Riesgo de apagón de radio HF de la NOAA en el nivel R3 y superior, mostrado por día. |
| **Fila S1+** | Riesgo de tormenta de radiación solar de la NOAA en el nivel S1 y superior, mostrado por día. |
| **Justificación** | Explicación en lenguaje sencillo del pronóstico de hoy. |
| **Campo geomagnético / Viento solar / Ruido / Rayos X** | Etiquetas de estado de resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la severidad. |

## Consejos

- El diálogo guarda y restaura automáticamente su tamaño y posición entre sesiones de AetherSDR. No hay una configuración separada para el modo sin marco.
- Un Kp de 5 o superior señala actividad geomagnética de nivel de tormenta. Las rutas polares y de latitudes altas son las más afectadas. Las bandas de HF más bajas (40m, 80m) tienden a mantenerse mejor que las bandas altas durante tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certeza. Revise los colores de las celdas de Kp en períodos individuales de 3 horas para ver cuándo durante el día el riesgo es mayor.
- Pase el cursor sobre las **tarjetas de condiciones actuales** (SFI, SN, índice A, índice K, rayos X) para ver explicaciones en información sobre herramientas de cada índice.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o valores desactualizados** — AetherSDR obtiene datos de pronóstico de internet. Verifique que su conexión de red esté activa y vuelva a abrir el diálogo.
- **No se recuerda la posición o el tamaño de la ventana** — El diálogo usa `PersistentDialog` para almacenar su geometría bajo la clave `PropDashboardDialogGeometry`. Si el archivo de configuración está dañado, cierre AetherSDR, elimine la entrada `PropDashboardDialogGeometry` de su archivo de configuración y vuelva a abrir el diálogo.

## Relacionado

- [Resumen del panel de propagación de HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decida qué banda de HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Esté atento a aperturas de E esporádica o aurorales en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
