# Ver el flujo solar actual, número de manchas solares e índice K

El Panel de Propagación de HF muestra índices solares en vivo — Índice de Flujo Solar (SFI), número de manchas solares, índice K, índice A y clase de rayos X — en un conjunto de tarjetas métricas. Use esta página para obtener una lectura rápida de las condiciones ionosféricas actuales antes de llamar CQ o buscar DX.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener datos solares en vivo.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Lea las **tarjetas de Condiciones Actuales** en la parte superior del diálogo. Se muestran cinco mosaicos métricos: **SFI**, **SN**, **Índice A**, **Índice K** y **Rayos X**.
3. Pase el cursor sobre cualquier mosaico para leer su información emergente. Cada información emergente explica qué mide el índice y qué significa el valor actual para la propagación de HF.

## Qué hace cada control

| Control | Qué muestra |
|---|---|
| Mosaico **SFI** | Índice de Flujo Solar. Los valores altos (120 y superiores) favorecen las bandas altas de HF; los valores por debajo de 120 sugieren que las bandas bajas liderarán. |
| Mosaico **SN** | Número de manchas solares. Más manchas solares generalmente significan una ionización más fuerte y un mejor soporte para la propagación de HF en frecuencias más altas. |
| Mosaico **Índice K** | Perturbación geomagnética a corto plazo en una escala de 0 a 9. Los valores de 5 o superiores indican actividad de nivel de tormenta y rutas polares ruidosas. |
| Mosaico **Índice A** | Promedio diario de actividad geomagnética. Los valores elevados significan que las condiciones pueden permanecer inestables incluso si el último índice K parece tranquilo. |
| Mosaico **Rayos X** | Última clase de llamarada solar (A/B/C/M/X). Las llamaradas de clase C, M y X pueden provocar apagones de radio diurnos en rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistentes; son indicadores de solo lectura actualizados con datos en vivo.

## Consejos

- El color del valor de cada mosaico cambia según la gravedad: el verde indica condiciones favorables o tranquilas, el amarillo indica condiciones elevadas o inestables, y el rojo indica actividad de nivel de tormenta o llamarada importante.
- Si un mosaico no muestra ningún valor, el panel aún está esperando datos de la red.

## Relacionados

- [Descripción general del Panel de Propagación de HF](overview.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decidir qué banda de HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
