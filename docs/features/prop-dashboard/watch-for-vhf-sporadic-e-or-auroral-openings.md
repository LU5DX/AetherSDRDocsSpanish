# Observe aperturas de E-esporádico o auroral en VHF

El Panel de Propagación de HF incluye una sección de Condiciones de VHF que muestra si las rutas de aurora, E-skip de Norteamérica o E-skip de Europa están actualmente abiertas. Utilícelo para decidir si debe monitorear frecuencias de VHF en busca de oportunidades de señales débiles o DX en FM.

## Antes de comenzar

- AetherSDR no necesita estar conectado a un radio para usar el panel de propagación.
- Se requiere una conexión a internet activa para que el panel obtenga los datos de propagación actuales.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.
2. Desplácese hacia abajo hasta la sección **VHF Conditions**.
3. Lea los indicadores **Aurora**, **E-Skip NA** y **E-Skip EU**. Cada uno muestra **Open** o **Closed**.
4. Lea las notas **What These Mean (VHF)** debajo de los indicadores. Estas dos notas en lenguaje sencillo explican lo que significan las aperturas aurorales y de E-esporádico para la operación en VHF.
5. Vuelva a consultar periódicamente: las condiciones pueden cambiar en cuestión de minutos durante periodos activos.

## Función de cada control

| Control | Comportamiento | Estados |
|---|---|---|
| **Aurora** | Muestra si la propagación auroral está actualmente activa. | Closed, Open |
| **E-Skip NA** | Muestra si el salto E-esporádico está activo sobre Norteamérica. | Closed, Open |
| **E-Skip EU** | Muestra si el salto E-esporádico está activo sobre Europa. | Closed, Open |
| **What These Mean (VHF)** | Dos notas rotativas en lenguaje sencillo que explican la diferencia entre propagación auroral y E-esporádico. | — |

## Consejos

- Un estado **Open** se muestra en verde; **Closed** se muestra en gris apagado. Un vistazo rápido al color le permite verificar el estado sin leer las etiquetas.
- Las aperturas aurorales tienden a correlacionarse con lecturas elevadas del índice K. Consulte la tarjeta **K INDEX** en la sección de Condiciones Actuales si el indicador Aurora muestra Open.

## Relacionados

- [Resumen del Panel de Propagación de HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico de Kp a 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
