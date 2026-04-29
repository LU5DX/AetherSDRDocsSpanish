# Determinar qué banda HF está abierta para trabajo diurno o nocturno

El Panel de Propagación HF muestra un resumen de condiciones banda por banda, dividido en columnas de día y noche, lo que permite elegir la mejor banda antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio para esta función.
- El panel obtiene datos de servicios externos de propagación; se necesita conexión a internet para datos en tiempo real.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Desplácese hasta la sección **HF Band Conditions** del cuadro de diálogo.
3. Lea la condición mostrada para cada una de las cuatro filas de banda bajo las columnas **Day** y **Night**.
4. Elija una banda cuya condición corresponda a su momento del día (día o noche en su ubicación).

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **HF Band Conditions** | Muestra una calificación de condición para cada una de las cuatro filas de banda HF, dividida en columnas de día y noche. |
| Valor de condición de banda | Indica uno de tres estados: **Good**, **Fair** o **Poor**, codificados en color verde, ámbar o naranja, respectivamente. |

## Consejos

- Las tarjetas **Current Conditions** en la parte superior del cuadro de diálogo muestran los valores de SFI, SN, A-index, K-index y rayos X. Compárelos con las condiciones de banda: un SFI alto (120 o más) generalmente favorece las bandas HF superiores, mientras que un K-index alto (5 o más) indica actividad geomagnética de nivel de tormenta que degrada muchos circuitos.
- Coloque el cursor sobre cualquier tarjeta de métrica para leer un tooltip en lenguaje sencillo que explica qué significa ese índice para la propagación HF.
- Si el A-index está elevado (15 o más), las condiciones de banda pueden permanecer inestables aunque el K-index actual parezca tranquilo.

## Solución de problemas

- **Todos los valores de condición de banda aparecen en blanco o no se actualizan** — el panel no pudo recuperar datos de propagación. Verifique su conexión a internet y vuelva a abrir el cuadro de diálogo.

## Relacionados

- [Descripción general del Panel de Propagación HF](overview.md)
- [Verificar el flujo solar actual, el número de manchas solares y el K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Detectar aperturas esporádicas-E o auroréales en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
