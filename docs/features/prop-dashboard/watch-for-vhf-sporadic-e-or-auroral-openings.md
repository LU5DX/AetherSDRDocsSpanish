# Observe aperturas de E-esporádico o aurora en VHF

El Panel de Propagación HF incluye una sección de Condiciones VHF que muestra si las rutas de aurora, E-skip de Norteamérica o E-skip de Europa están actualmente abiertas. Use esto para decidir si debe monitorear frecuencias VHF en busca de oportunidades de señales débiles o DX en FM.

## Antes de comenzar

- AetherSDR no necesita estar conectado a una radio para usar el panel de propagación.
- Se requiere una conexión activa a internet para que el panel obtenga los datos de propagación actuales.

## Pasos

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.
2. Desplácese hacia abajo hasta la sección **VHF Conditions**.
3. Lea los indicadores **Aurora**, **E-Skip NA** y **E-Skip EU**. Cada uno muestra **Open** o **Closed**.
4. Lea las notas **What These Mean (VHF)** debajo de los indicadores. Estas dos notas en lenguaje sencillo explican qué significan las aperturas de aurora y E-esporádico para la operación en VHF.
5. Vuelva a consultar periódicamente: las condiciones pueden cambiar en cuestión de minutos durante períodos activos.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---|---|---|
| **Aurora** | Muestra si la propagación auroral está actualmente activa. | Closed, Open |
| **E-Skip NA** | Muestra si el E-skip esporádico está activo sobre Norteamérica. | Closed, Open |
| **E-Skip EU** | Muestra si el E-skip esporádico está activo sobre Europa. | Closed, Open |
| **What These Mean (VHF)** | Dos notas rotativas en lenguaje sencillo que explican la diferencia entre la propagación por aurora y por E-esporádico. | — |

## Consejos

- Un estado **Open** se muestra en verde; **Closed** se muestra en gris apagado. Un vistazo rápido a los colores le permite verificar el estado sin leer las etiquetas.
- Las aperturas por aurora tienden a correlacionarse con lecturas elevadas del índice K. Revise la tarjeta **K INDEX** en la sección Current Conditions si el indicador Aurora muestra Open.
- El panel ahora respeta el tema activo. Su estilo (colores de fondo, líneas separadoras, bordes y paneles de notas de aprendizaje) se adapta automáticamente al cambiar de tema.
- Si el panel parece desactualizado o deja de actualizarse, verifique su conexión a internet. El panel usa un tiempo de espera de red de 15 segundos al obtener datos de propagación; si la obtención no puede completarse dentro de ese plazo, los indicadores afectados podrían no actualizarse hasta el siguiente ciclo de actualización.

## Relacionado

- [Descripción general del Panel de Propagación HF](overview.md)
- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico de Kp a 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
