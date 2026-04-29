# Consultar el flujo solar actual, el número de manchas solares y el índice K

El Panel de Propagación HF muestra índices solares en tiempo real — Solar Flux Index (SFI), número de manchas solares, índice K, índice A y clase de rayos X — en un conjunto de tarjetas de métricas. Use esta página para obtener una lectura rápida de las condiciones ionosféricas actuales antes de llamar en CQ o perseguir DX.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio para esta función.
- Se necesita una conexión a internet activa para obtener los datos solares en tiempo real.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Lea las **tarjetas de Condiciones Actuales** en la parte superior del diálogo. Se muestran cinco fichas de métricas: **SFI**, **SN**, **A-index**, **K-index** y **X-ray**.
3. Pase el cursor sobre cualquier ficha para leer su información emergente. Cada información emergente explica qué mide el índice y qué significa el valor actual para la propagación HF.

## Qué hace cada control

| Control | Qué muestra |
|---|---|
| Ficha **SFI** | Solar Flux Index. Valores más altos (120 y superiores) favorecen las bandas HF altas; valores por debajo de 120 sugieren que las bandas bajas serán las protagonistas. |
| Ficha **SN** | Número de manchas solares. Más manchas generalmente significan mayor ionización y mejor soporte para la propagación HF en frecuencias más altas. |
| Ficha **K-index** | Perturbación geomagnética a corto plazo en una escala de 0–9. Valores de 5 o superiores indican actividad de nivel de tormenta y ruido en las rutas polares. |
| Ficha **A-index** | Promedio diario de la actividad geomagnética. Valores elevados significan que las condiciones pueden mantenerse inestables incluso si el último K-index parece tranquilo. |
| Ficha **X-ray** | Última clase de erupción solar (A/B/C/M/X). Las erupciones de clase C, M y X pueden provocar apagones de radio durante el día en las rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistentes — son indicadores de solo lectura actualizados con datos en tiempo real.

## Consejos

- El color del valor de cada ficha cambia según la severidad: el verde indica condiciones favorables o tranquilas, el amarillo indica condiciones elevadas o inestables, y el rojo indica actividad de nivel de tormenta o erupción solar importante.
- Si una ficha no muestra ningún valor, el panel aún está esperando datos de la red.

## Relacionados

- [Descripción general del Panel de Propagación HF](overview.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Determinar qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
