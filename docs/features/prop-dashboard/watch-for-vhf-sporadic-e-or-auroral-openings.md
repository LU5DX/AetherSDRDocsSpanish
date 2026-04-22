# Monitorear aperturas esporádicas-E o aurorarles en VHF

El Panel de Propagación HF incluye una sección de Condiciones VHF que muestra si las rutas de aurora, E-skip norteamericano o E-skip europeo están actualmente abiertas. Use esto para decidir si conviene monitorear frecuencias VHF en busca de oportunidades de señal débil o DX en FM.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un radio para usar el panel de propagación.
- Se requiere una conexión a internet activa para que el panel obtenga los datos de propagación actuales.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Desplácese hacia abajo hasta la sección **VHF Conditions**.
3. Lea los indicadores **Aurora**, **E-Skip NA** y **E-Skip EU**. Cada uno muestra **Open** o **Closed**.
4. Lea las notas **What These Mean (VHF)** que aparecen debajo de los indicadores. Estas dos notas en lenguaje sencillo explican qué significan las aperturas de aurora y esporádica-E para la operación en VHF.
5. Consulte el panel periódicamente — las condiciones pueden cambiar en minutos durante períodos activos.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---|---|---|
| **Aurora** | Indica si la propagación auroral está actualmente activa. | Closed, Open |
| **E-Skip NA** | Indica si el salto esporádico-E está activo sobre América del Norte. | Closed, Open |
| **E-Skip EU** | Indica si el salto esporádico-E está activo sobre Europa. | Closed, Open |
| **What These Mean (VHF)** | Dos notas rotativas en lenguaje sencillo que explican la diferencia entre la propagación por aurora y la esporádica-E. | — |

## Consejos

- El estado **Open** se muestra en verde; **Closed** se muestra en gris apagado. Un vistazo rápido al color permite verificar el estado sin leer las etiquetas.
- Las aperturas de aurora tienden a correlacionarse con lecturas elevadas del índice K. Consulte la tarjeta **K INDEX** en la sección Current Conditions si el indicador Aurora muestra Open.

## Relacionados

- [Descripción general del Panel de Propagación HF](overview.md)
- [Verificar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp a 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
