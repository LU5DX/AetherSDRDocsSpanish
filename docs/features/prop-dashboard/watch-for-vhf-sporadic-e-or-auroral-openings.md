# Vigilar aperturas esporádicas-E o aurorales en VHF

El Panel de Propagación HF incluye una sección de Condiciones VHF que muestra si los caminos de aurora, E-skip norteamericano o E-skip europeo están actualmente abiertos. Utilícela para decidir si monitorear frecuencias VHF en busca de oportunidades de señal débil o DX en FM.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un radio para usar el panel de propagación.
- Se requiere una conexión a internet activa para que el panel obtenga los datos de propagación actuales.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Desplácese hacia abajo hasta la sección **VHF Conditions**.
3. Lea los indicadores **Aurora**, **E-Skip NA** y **E-Skip EU**. Cada uno muestra **Open** o **Closed**.
4. Lea las notas **What These Mean (VHF)** que aparecen debajo de los indicadores. Estas dos notas en lenguaje sencillo explican qué significan las aperturas aurorales y las esporádicas-E para la operación en VHF.
5. Revise periódicamente — las condiciones pueden cambiar en cuestión de minutos durante períodos activos.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---|---|---|
| **Aurora** | Muestra si la propagación auroral está actualmente activa. | Closed, Open |
| **E-Skip NA** | Muestra si el salto esporádico-E está activo sobre América del Norte. | Closed, Open |
| **E-Skip EU** | Muestra si el salto esporádico-E está activo sobre Europa. | Closed, Open |
| **What These Mean (VHF)** | Dos notas rotativas en lenguaje sencillo que explican la diferencia entre la propagación auroral y la esporádica-E. | — |

## Consejos

- El estado **Open** se muestra en verde; **Closed** se muestra en gris atenuado. Un vistazo rápido al color permite verificar el estado sin leer las etiquetas.
- Las aperturas aurorales tienden a correlacionarse con lecturas elevadas del índice K. Revise la tarjeta **K INDEX** en la sección Current Conditions si el indicador Aurora muestra Open.

## Relacionados

- [Descripción general del Panel de Propagación HF](overview.md)
- [Consultar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
