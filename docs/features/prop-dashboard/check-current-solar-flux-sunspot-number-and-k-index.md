# Verificar el flujo solar actual, el número de manchas solares y el índice K

El Panel de Propagación HF muestra índices solares en tiempo real — Índice de Flujo Solar (SFI), número de manchas solares, índice K, índice A y clase de rayos X — en un conjunto de tarjetas de métricas. Use esta página para obtener una lectura rápida de las condiciones ionosféricas actuales antes de llamar CQ o perseguir DX.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos solares en tiempo real.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Lea las **tarjetas de Condiciones Actuales** en la parte superior del cuadro de diálogo. Se muestran cinco mosaicos de métricas: **SFI**, **SN**, **A-index**, **K-index** y **X-ray**.
3. Pase el cursor sobre cualquier mosaico para leer su información emergente. Cada tooltip explica qué mide el índice y qué significa el valor actual para la propagación HF.

## Qué hace cada control

| Control | Qué muestra |
|---|---|
| Mosaico **SFI** | Índice de Flujo Solar. Valores más altos (120 y superiores) favorecen las bandas HF altas; valores por debajo de 120 sugieren que las bandas bajas serán las principales. |
| Mosaico **SN** | Número de manchas solares. Más manchas generalmente significan una ionización más fuerte y mejor soporte para la propagación HF en frecuencias más altas. |
| Mosaico **K-index** | Perturbación geomagnética a corto plazo en una escala de 0–9. Valores de 5 o superiores indican actividad de nivel de tormenta y caminos polares ruidosos. |
| Mosaico **A-index** | Promedio diario de actividad geomagnética. Valores elevados significan que las condiciones pueden permanecer inestables incluso si el último índice K parece tranquilo. |
| Mosaico **X-ray** | Última clase de erupción solar (A/B/C/M/X). Las erupciones de clase C, M y X pueden provocar apagones de radio diurnos en las rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistentes — son indicadores de solo lectura actualizados con datos en tiempo real.

## Consejos

- El color del valor de cada mosaico cambia según la severidad: el verde indica condiciones favorables o tranquilas, el amarillo indica condiciones elevadas o inestables, y el rojo indica actividad de nivel de tormenta o erupciones importantes.
- Si un mosaico no muestra ningún valor, el panel aún está esperando datos de la red.

## Relacionado

- [Descripción general del Panel de Propagación HF](overview.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decidir qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
