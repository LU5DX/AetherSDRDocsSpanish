# Panel de Propagación HF

El Panel de Propagación HF ofrece una vista rápida de las condiciones actuales de propagación en HF/VHF, incluyendo índices solares, un pronóstico de Kp a 3 días con evaluaciones de riesgo de apagones y radiación, condiciones diurnas/nocturnas de bandas HF, imágenes solares y lunares, e indicios de propagación esporádica-E/aurora.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener datos solares en vivo.

## Abriendo el panel

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.

El título y la geometría del diálogo se conservan entre sesiones mediante la clave de configuración `PropDashboardDialogGeometry`.

## Función de cada control

### Tarjetas de Condiciones Actuales

En la parte superior del diálogo se muestran cinco indicadores métricos. Pase el cursor sobre cualquier indicador para leer su información sobre herramientas, que explica qué mide el índice y qué significa el valor actual para la propagación HF.

| Control | Qué muestra |
|---|---|
| Indicador **SFI** | Índice de Flujo Solar. Valores altos (120 y superiores) favorecen las bandas altas de HF; valores inferiores a 120 sugieren que las bandas bajas serán predominantes. |
| Indicador **SN** | Número de manchas solares. Más manchas solares generalmente significan una ionización más fuerte y un mejor soporte para la propagación HF en frecuencias altas. |
| Indicador **K-index** | Perturbación geomagnética a corto plazo en una escala de 0 a 9. Valores de 5 o superiores indican actividad de tormenta y rutas polares ruidosas. |
| Indicador **A-index** | Promedio diario de la actividad geomagnética. Valores elevados significan que las condiciones pueden permanecer inestables incluso si el último índice K parece tranquilo. |
| Indicador **X-ray** | Clase de llamarada solar más reciente (A/B/C/M/X). Las llamaradas de clase C, M y X pueden desencadenar apagones de radio diurnos en rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistente; son indicadores de solo lectura actualizados con datos en vivo.

### Cuadrícula de Pronóstico a 3 Días

Muestra el pronóstico de Kp para cada período de 3 horas UTC durante tres días. Debajo de la cuadrícula, las filas de resumen muestran:

- **Max Kp** - Valor de Kp máximo previsto por día
- **R1-R2** - Riesgo de apagones de radio menores a moderados
- **R3+** - Riesgo de apagones de radio fuertes a extremos
- **S1+** - Riesgo de tormentas de radiación solar

Etiquetas de resumen adicionales debajo de la cuadrícula de pronóstico muestran:
- Estado del **campo geomagnético**
- Condiciones del **viento solar**
- Niveles de **ruido**
- Actividad de **rayos X**

### Panel Solar y Lunar

Muestra una imagen solar en vivo. Haga clic en la imagen para alternar entre las longitudes de onda disponibles. La etiqueta predeterminada muestra **Corona (193A)**. Debajo de la imagen solar, se muestra la fase lunar actual.

### Qué Buscar

En esta sección aparecen notas de aprendizaje rotativas y en lenguaje sencillo sobre la imagen solar actual.

### Condiciones de Bandas HF

Muestra las condiciones diurnas y nocturnas por fila de banda. Se muestran cuatro filas de bandas con indicadores codificados por color que muestran la calidad de la propagación.

### Condiciones VHF

Muestra las aperturas de propagación VHF actuales con tres estados por indicador: **Cerrado** o **Abierto**.

| Indicador | Qué muestra |
|---|---|
| **Aurora** | Estado actual de apertura de propagación auroral |
| **E-Skip NA** | Estado actual de apertura de propagación esporádica-E para América del Norte |
| **E-Skip EU** | Estado actual de apertura de propagación esporádica-E para Europa |

### Significado de Estos Indicadores (VHF)

Dos notas de aprendizaje explican la diferencia entre los modos de propagación auroral y esporádica-E.

### Fundamento

En la parte inferior del panel aparece una explicación en lenguaje sencillo del pronóstico del día.

## Consejos

- El color del valor de cada indicador cambia según la gravedad: verde indica condiciones favorables o tranquilas; amarillo indica condiciones elevadas o inestables; y rojo indica actividad de tormenta o llamaradas mayores.
- Si un indicador no muestra ningún valor, el panel aún está esperando datos de la red.
- El tamaño y la posición de la ventana del panel se recuerdan entre sesiones. Cambie el tamaño o mueva el diálogo y se volverá a abrir en la misma ubicación.
- Las celdas de Kp en la cuadrícula de pronóstico están codificadas por color según su nivel de gravedad.

## Relacionados

- [Consultar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp a 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decidir qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
