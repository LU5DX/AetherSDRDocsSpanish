# Panel de Propagación de HF

El Panel de Propagación de HF ofrece una vista rápida de las condiciones actuales de propagación en HF/VHF, que incluye índices solares, un pronóstico de Kp a 3 días con evaluaciones de riesgo de apagones y radiación, condiciones de banda HF día/noche, imágenes solares y lunares, e indicios de E-Esporádica/aurora.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener datos solares en vivo.

## Abriendo el panel

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.

## Función de cada control

### Tarjetas de Condiciones Actuales

En la parte superior del diálogo se muestran cinco métricas en mosaicos. Pase el cursor sobre cualquier mosaico para leer su información sobre herramientas, que explica qué mide el índice y qué significa el valor actual para la propagación en HF.

| Control | Qué muestra |
|---|---|
| Mosaico **SFI** | Índice de Flujo Solar. Valores superiores (120 o más) favorecen las bandas altas de HF; valores inferiores a 120 sugieren que las bandas bajas liderarán. |
| Mosaico **SN** | Número de manchas solares. Más manchas solares generalmente significan una ionización más fuerte y un mejor soporte para la propagación en frecuencias HF más altas. |
| Mosaico **K-index** | Perturbación geomagnética a corto plazo en una escala de 0 a 9. Valores de 5 o superiores indican actividad de tormenta y rutas polares ruidosas. |
| Mosaico **A-index** | Promedio diario de actividad geomagnética. Valores elevados significan que las condiciones pueden permanecer inestables incluso si el último K-index parece tranquilo. |
| Mosaico **X-ray** | Clase de la última fulguración solar (A/B/C/M/X). Las fulguraciones de clase C, M y X pueden desencadenar apagones de radio diurnos en rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistentes; son indicadores de solo lectura que se actualizan con datos en vivo.

### Cuadrícula de Pronóstico a 3 Días

Muestra el pronóstico de Kp para cada período de 3 horas UTC durante tres días. Debajo de la cuadrícula, las filas de resumen muestran:

- **Max Kp** - Valor de Kp máximo pronosticado por día
- **R1-R2** - Riesgo de apagones de radio menores a moderados
- **R3+** - Riesgo de apagones de radio fuertes a extremos
- **S1+** - Riesgo de tormentas de radiación solar

Etiquetas de resumen adicionales debajo de la cuadrícula de pronóstico muestran:
- Estado del **campo geomagnético**
- Condiciones del **viento solar**
- Niveles de **ruido**
- Actividad de **rayos X**

### Panel Solar y Lunar

Muestra una imagen solar en vivo. Haga clic en la imagen para cambiar entre las longitudes de onda disponibles. La etiqueta predeterminada muestra **Corona (193A)**. Debajo de la imagen solar, se muestra la fase lunar actual.

### Qué Buscar

En esta sección aparecen notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual.

### Condiciones de Banda HF

Muestra las condiciones diurnas y nocturnas por fila de banda. Se muestran cuatro filas de banda con indicadores codificados por colores que señalan la calidad de la propagación.

### Condiciones de VHF

Muestra las aperturas de propagación VHF actuales con tres estados por indicador: **Cerrado** o **Abierto**.

| Indicador | Qué muestra |
|---|---|
| **Aurora** | Estado actual de apertura de propagación auroral |
| **E-Skip NA** | Estado actual de apertura de E-Esporádica para Norteamérica |
| **E-Skip EU** | Estado actual de apertura de E-Esporádica para Europa |

### Qué Significan (VHF)

Dos notas de aprendizaje explican la diferencia entre los modos de propagación por aurora y E-Esporádica.

### Justificación

En la parte inferior del panel aparece una explicación en lenguaje sencillo del pronóstico del día.

## Consejos

- El color del valor de cada mosaico cambia según la gravedad: el verde indica condiciones favorables o tranquilas, el amarillo indica condiciones elevadas o inestables, y el rojo indica actividad de tormenta o fulguraciones mayores.
- Si un mosaico no muestra ningún valor, el panel aún está esperando datos de la red.
- El panel admite el modo de ventana sin marco. Cuando está habilitado, se muestra una barra de título personalizada con el título de ventana "HF Propagation Dashboard". Este modo respeta la configuración `FramelessWindow` de la aplicación.
- Las celdas de Kp en la cuadrícula de pronóstico están codificadas por colores según su nivel de gravedad.

## Relacionado

- [Consultar el flujo solar, número de manchas solares e índice K actuales](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp a 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decidir qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
