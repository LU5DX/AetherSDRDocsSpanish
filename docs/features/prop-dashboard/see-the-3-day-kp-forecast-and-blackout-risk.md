# Ver el pronóstico de Kp a 3 días y el riesgo de apagón

El Panel de Propagación de HF incluye una cuadrícula de pronóstico de Kp a 3 días que muestra la actividad geomagnética en períodos UTC de 3 horas, junto con filas de riesgo de apagón de radio NOAA y de tormenta de radiación para cada día. Úselo para planificar sesiones de operación en torno a condiciones perturbadas o auroras.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos del pronóstico.

## Pasos

1. Haga clic en `View > Propagation Conditions` en la barra de menú. Esto abre el cuadro de diálogo del Panel de Propagación de HF.
2. Desplácese hasta la sección de la **Cuadrícula de pronóstico a 3 días**.
3. Lea los valores de Kp en las 8 columnas de períodos UTC de 3 horas para cada uno de los tres días. Las celdas están codificadas por colores: verde indica condiciones tranquilas (Kp inferior a 3), amarillo indica condiciones inestables (Kp 3–4) y rojo indica actividad de nivel de tormenta (Kp 5 o superior).
4. Verifique las filas **R1-R2**, **R3+** y **S1+** debajo de las celdas de Kp. Estas muestran la probabilidad de riesgo de apagón de radio NOAA y de tormenta de radiación por día.
5. Lea el texto de **Justificación** debajo de la cuadrícula para obtener una explicación en lenguaje sencillo del pronóstico actual.
6. Revise las etiquetas resumen — **Campo geomagnético**, **Viento solar**, **Ruido** y **Rayos X** — para obtener contexto adicional debajo de la cuadrícula de pronóstico.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Cuadrícula de pronóstico a 3 días** | Muestra Kp por período UTC de 3 horas durante tres días, más el Kp máximo por día. Las celdas están codificadas por colores según la gravedad. |
| Fila **R1-R2** | Riesgo de apagón de radio HF de NOAA en el nivel R1–R2, mostrado por día. |
| Fila **R3+** | Riesgo de apagón de radio HF de NOAA en el nivel R3 y superior, mostrado por día. |
| Fila **S1+** | Riesgo de tormenta de radiación solar de NOAA en el nivel S1 y superior, mostrado por día. |
| **Justificación** | Explicación en lenguaje sencillo del pronóstico de hoy. |
| **Campo geomagnético / Viento solar / Ruido / Rayos X** | Etiquetas de estado resumen debajo de la cuadrícula de pronóstico. Codificadas por colores según la gravedad. |

## Consejos

- El cuadro de diálogo admite el modo sin marco. Para habilitar o deshabilitar el modo sin marco, establezca la configuración `FramelessWindow` en `True` o `False` en su archivo de configuración de AetherSDR.
- Un Kp de 5 o superior indica actividad geomagnética de nivel de tormenta. Las rutas polares y de alta latitud son las más afectadas. Las bandas de HF más bajas (40m, 80m) tienden a mantenerse mejor que las bandas altas durante las tormentas geomagnéticas.
- Las filas R1-R2 y R3+ reflejan estimaciones de probabilidad por día, no certezas. Verifique los colores de las celdas de Kp en los períodos individuales de 3 horas para ver cuándo durante el día el riesgo es mayor.
- Pase el cursor sobre las **Tarjetas de condiciones actuales** (SFI, SN, A-index, K-index, X-ray) para obtener explicaciones emergentes de cada índice.

## Solución de problemas

- **La cuadrícula de pronóstico no muestra datos o muestra valores desactualizados** — AetherSDR obtiene los datos del pronóstico de internet. Verifique que su conexión de red esté activa y vuelva a abrir el cuadro de diálogo.
- **La decoración de la ventana aparece o desaparece inesperadamente** — La configuración del modo sin marco controla si el cuadro de diálogo tiene un marco de ventana nativo. Cambie la configuración `FramelessWindow` y vuelva a abrir el cuadro de diálogo.

## Relacionado

- [Descripción general del Panel de Propagación de HF](overview.md)
- [Ver el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Decidir qué banda de HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Observar aperturas de VHF por esporádica-E o auroras](watch-for-vhf-sporadic-e-or-auroral-openings.md)
