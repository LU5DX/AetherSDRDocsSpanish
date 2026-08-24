# Panel de Propagación de HF

El Panel de Propagación de HF ofrece una vista general de las condiciones actuales de propagación en HF/VHF, incluidos los índices solares, un pronóstico de Kp a 3 días con evaluaciones de riesgo de apagones y radiación, condiciones de bandas HF de día/noche, imágenes solares y lunares, y sugerencias sobre propagación por E-esporádica/aurora.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para esta función.
- Se necesita una conexión activa a internet para obtener datos solares en vivo.

## Cómo abrir el panel

1. Haga clic en `View > Propagation Conditions` para abrir el Panel de Propagación de HF.

El título del diálogo y su geometría se conservan entre sesiones mediante la clave de configuración `PropDashboardDialogGeometry`.

## Qué hace cada control

### Tarjetas de Condiciones Actuales

En la parte superior del diálogo se muestran cinco mosaicos de métricas. Pase el cursor sobre cualquier mosaico para leer su información emergente que explica qué mide el índice y qué significa el valor actual para la propagación en HF.

| Control | Qué muestra |
|---|---|
| Mosaico **SFI** | Índice de Flujo Solar. Los valores altos (120 y superiores) favorecen las bandas altas de HF; los valores inferiores a 120 sugieren que las bandas bajas predominarán. |
| Mosaico **SN** | Número de manchas solares. Más manchas solares generalmente implican una ionización más fuerte y un mejor soporte para la propagación en frecuencias HF más altas. |
| Mosaico **K-index** | Alteración geomagnética a corto plazo en una escala de 0–9. Los valores de 5 o superiores indican actividad de tormenta y rutas polares ruidosas. |
| Mosaico **A-index** | Promedio diario de la actividad geomagnética. Los valores elevados significan que las condiciones pueden permanecer inestables incluso si el último valor de K-index parece tranquilo. |
| Mosaico **X-ray** | Última clase de llamarada solar (A/B/C/M/X). Las llamaradas de clase C, M y X pueden provocar apagones de radio diurnos en rutas iluminadas por el sol. |

Ninguno de estos controles tiene claves de configuración persistente; son indicadores de solo lectura que se actualizan con datos en vivo.

### Cuadrícula de Pronóstico a 3 Días

Muestra el pronóstico de Kp para cada período de 3 horas UTC a lo largo de tres días. Debajo de la cuadrícula, las filas de resumen muestran:

- **Max Kp** - Valor de Kp máximo pronosticado por día
- **R1-R2** - Riesgo de apagones de radio menores a moderados
- **R3+** - Riesgo de apagones de radio fuertes a extremos
- **S1+** - Riesgo de tormentas de radiación solar

Etiquetas de resumen adicionales bajo la cuadrícula de pronóstico muestran:
- Estado del **campo geomagnético**
- Condiciones del **viento solar**
- Niveles de **ruido**
- Actividad de **rayos X**

### Panel Solar y Lunar

Muestra una imagen solar en vivo. Haga clic en la imagen para alternar entre las longitudes de onda disponibles. La etiqueta predeterminada muestra **Corona (193A)**. Debajo de la imagen solar, se muestra la fase lunar actual.

### Qué Buscar

En esta sección aparecen notas educativas rotativas en lenguaje sencillo sobre la imagen solar actual.

### Condiciones de Banda HF

Muestra las condiciones de día y noche por fila de banda. Se muestran cuatro filas de bandas con indicadores codificados por color que muestran la calidad de la propagación.

### Condiciones de VHF

Muestra las aperturas de propagación VHF actuales con tres estados por indicador: **Cerrado** o **Abierto**.

| Indicador | Qué muestra |
|---|---|
| **Aurora** | Estado actual de la apertura de propagación auroral |
| **E-Skip NA** | Estado actual de la apertura por E-esporádica para América del Norte |
| **E-Skip EU** | Estado actual de la apertura por E-esporádica para Europa |

### Qué Significan Estos (VHF)

Dos notas educativas explican la diferencia entre los modos de propagación por aurora y por E-esporádica.

### Justificación

Una explicación en lenguaje sencillo del pronóstico de hoy aparece en la parte inferior del panel.

## Consejos

- El color del valor de cada mosaico cambia según la severidad: el verde indica condiciones favorables o tranquilas, el amarillo indica condiciones elevadas o inestables, y el rojo indica actividad de tormenta o llamaradas mayores.
- Si un mosaico no muestra ningún valor, el panel aún está esperando datos de la red.
- El tamaño y la posición de la ventana del panel se recuerdan entre sesiones. Cambie el tamaño o mueva el diálogo y se reabrirá en la misma ubicación.
- Las celdas de Kp en la cuadrícula de pronóstico están codificadas por colores según su nivel de severidad.
- El panel respeta su tema actual. Desde la versión 26.6.1, todos los elementos visuales adaptan sus colores al tema activo para una apariencia coherente.
- Desde la versión 26.8.4, las solicitudes de red utilizadas para obtener datos de clima espacial expiran automáticamente después de 15 segundos si no se recibe respuesta. Si el panel permanece vacío durante más tiempo, verifique su conexión a internet e intente nuevamente.

## Relacionado

- [Verifique el flujo solar actual, el número de manchas solares y el K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Consulte el pronóstico de Kp a 3 días y el riesgo de apagones](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decida qué banda HF está abierta para trabajo de día o de noche](decide-which-hf-band-is-open-for-day-or-night-work.md)
