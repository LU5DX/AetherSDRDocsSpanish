# Panel de Propagación HF

El Panel de Propagación HF proporciona una visión general de las condiciones actuales de propagación en HF/VHF, incluyendo índices solares, un pronóstico de Kp a 3 días con evaluaciones de riesgo de apagones y radiación, condiciones de bandas HF día/noche, imágenes solares y lunares, e indicios de E-esporádica/aurora.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión a internet activa para obtener datos solares en vivo.

## Cómo abrir el panel

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación HF.

El título y la geometría del diálogo se conservan entre sesiones mediante la clave de configuración `PropDashboardDialogGeometry`.

## Qué hace cada control

### Tarjetas de condiciones actuales

Cinco mosaicos de métricas se muestran en la parte superior del diálogo. Pase el ratón sobre cualquier mosaico para leer su información sobre herramientas, que explica qué mide el índice y qué significa el valor actual para la propagación HF.

| Control | Qué muestra |
|---|---|
| Mosaico **SFI** | Índice de Flujo Solar. Valores más altos (120 y superiores) favorecen las bandas altas de HF; valores por debajo de 120 sugieren que las bandas bajas serán las mejores. |
| Mosaico **SN** | Número de manchas solares. Más manchas solares generalmente significan una ionización más fuerte y un mejor soporte para la propagación HF en frecuencias más altas. |
| Mosaico **K-index** | Perturbación geomagnética a corto plazo en una escala de 0 a 9. Valores de 5 o superiores indican actividad de tormenta y rutas polares ruidosas. |
| Mosaico **A-index** | Promedio diario de actividad geomagnética. Valores elevados significan que las condiciones pueden permanecer inestables incluso si el último índice K parece tranquilo. |
| Mosaico **X-ray** | Clase de llamarada solar más reciente (A/B/C/M/X). Las llamaradas de clase C, M y X pueden desencadenar apagones de radio diurnos en rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistentes, ya que son indicadores de solo lectura actualizados con datos en vivo.

### Cuadrícula de pronóstico de 3 días

Muestra el pronóstico Kp para cada período UTC de 3 horas durante tres días. Debajo de la cuadrícula, las filas de resumen muestran:

- **Max Kp** - Valor Kp predicho más alto por día
- **R1-R2** - Riesgo de apagones de radio menores a moderados
- **R3+** - Riesgo de apagones de radio fuertes a extremos
- **S1+** - Riesgo de tormentas de radiación solar

Las etiquetas de resumen adicionales debajo de la cuadrícula de pronóstico muestran:
- Estado del **campo geomagnético**
- Condiciones del **viento solar**
- Niveles de **ruido**
- Actividad de **rayos X**

### Panel solar y lunar

Muestra una imagen solar en vivo. Haga clic en la imagen para alternar entre las longitudes de onda disponibles. La etiqueta predeterminada muestra **Corona (193A)**. Debajo de la imagen solar, se muestra la fase lunar actual.

### Qué buscar

En esta sección aparecen notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual.

### Condiciones de bandas HF

Muestra las condiciones de día y noche por fila de banda. Se muestran cuatro filas de banda con indicadores codificados por colores que muestran la calidad de propagación.

### Condiciones de VHF

Muestra las aperturas de propagación VHF actuales con tres estados por indicador: **Closed** (Cerrado) o **Open** (Abierto).

| Indicador | Qué muestra |
|---|---|
| **Aurora** | Estado actual de la apertura de propagación auroral |
| **E-Skip NA** | Estado actual de la apertura de E-esporádica para Norteamérica |
| **E-Skip EU** | Estado actual de la apertura de E-esporádica para Europa |

### Qué significan (VHF)

Dos notas de aprendizaje explican la diferencia entre los modos de propagación de aurora y E-esporádica.

### Fundamentos

Una explicación en lenguaje sencillo del pronóstico de hoy aparece en la parte inferior del panel.

## Consejos

- El color del valor de cada mosaico cambia según la gravedad: verde indica condiciones favorables o tranquilas, amarillo indica condiciones elevadas o inestables, y rojo indica actividad de tormenta o llamarada importante.
- Si un mosaico no muestra ningún valor, el panel aún está esperando datos de la red.
- El tamaño y la posición de la ventana del panel se recuerdan entre sesiones. Redimensione o mueva el diálogo y se volverá a abrir en la misma ubicación.
- Las celdas de Kp en la cuadrícula de pronóstico están codificadas por colores según su nivel de gravedad.
- El panel respeta su tema actual. Desde la versión 26.6.1, todos los elementos visuales adaptan sus colores al tema activo para una apariencia consistente.

## Relacionado

- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [See the 3-day Kp forecast and blackout risk](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decide which HF band is open for day or night work](decide-which-hf-band-is-open-for-day-or-night-work.md)
