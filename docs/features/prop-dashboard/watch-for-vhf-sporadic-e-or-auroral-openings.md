# Monitorización de aperturas VHF por E-esporádica o aurora

El Panel de Propagación de HF incluye una sección de Condiciones VHF que muestra si las rutas de aurora, E-skip de Norteamérica o E-skip de Europa están actualmente abiertas. Úselo para decidir si debe monitorear frecuencias VHF en busca de oportunidades de señales débiles o DX en FM.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para usar el panel de propagación.
- Se requiere una conexión a internet activa para que el panel obtenga los datos de propagación actuales.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Desplace la vista hacia abajo hasta la sección **VHF Conditions**.
3. Lea los indicadores **Aurora**, **E-Skip NA** y **E-Skip EU**. Cada uno muestra **Open** o **Closed**.
4. Lea las notas **What These Mean (VHF)** debajo de los indicadores. Estas dos notas en lenguaje sencillo explican lo que significan las aperturas por aurora y E-esporádica para la operación en VHF.
5. Vuelva a consultar periódicamente — las condiciones pueden cambiar en cuestión de minutos durante períodos activos.

## Función de cada control

| Control | Comportamiento | Estados |
|---|---|---|
| **Aurora** | Muestra si la propagación auroral está actualmente activa. | Closed, Open |
| **E-Skip NA** | Muestra si el salto E-esporádico está activo sobre Norteamérica. | Closed, Open |
| **E-Skip EU** | Muestra si el salto E-esporádico está activo sobre Europa. | Closed, Open |
| **What These Mean (VHF)** | Dos notas rotativas en lenguaje sencillo que explican la diferencia entre la propagación por aurora y la E-esporádica. | — |

## Consejos

- Un estado **Open** se muestra en verde; **Closed** se muestra en gris apagado. Una revisión rápida de colores le permite verificar el estado sin necesidad de leer las etiquetas.
- Las aperturas por aurora tienden a correlacionarse con lecturas elevadas del índice K. Revise la tarjeta **K INDEX** en la sección Current Conditions si el indicador de Aurora muestra Open.

## Relacionados

- [Resumen del Panel de Propagación de HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
