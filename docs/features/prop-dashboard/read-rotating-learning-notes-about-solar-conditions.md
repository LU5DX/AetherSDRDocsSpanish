# Panel de Propagación de HF

El Panel de Propagación de HF ofrece una vista rápida de las condiciones de propagación de HF y VHF, incluidos los índices solares actuales, un pronóstico de Kp a 3 días con riesgo de apagón y radiación, condiciones de bandas de HF día/noche, imágenes solares y lunares, y sugerencias de propagación por esporádica-E y aurora.

## Cómo abrir el panel

- Abra el Panel de Propagación de HF mediante `View > Propagation Conditions`.

## Diseño del panel

El panel está organizado en varias secciones que muestran las condiciones actuales, los pronósticos y el material educativo.

### Tarjetas de condiciones actuales

Cinco tarjetas de métricas muestran los índices solares y geomagnéticos actuales. Pase el cursor sobre cualquier tarjeta para ver una explicación en lenguaje sencillo de lo que significa el valor.

| Métrica | Descripción |
|---|---|
| SFI | Índice de flujo solar |
| SN | Número de manchas solares |
| A-index | Índice geomagnético A |
| K-index | Índice geomagnético K |
| X-ray | Nivel actual de flujo de rayos X |

### Cuadrícula de pronóstico a 3 días

Una cuadrícula con códigos de color que muestra los pronósticos de Kp para cada período de 3 horas UTC a lo largo de tres días. Debajo de la cuadrícula, filas de riesgo adicionales muestran:

- Kp máximo por día
- R1-R2: Riesgo de apagón de radio (menor a moderado)
- R3+: Riesgo de apagón de radio (fuerte a extremo)
- S1+: Riesgo de tormenta de radiación solar

Al final de la sección de pronóstico, las etiquetas de resumen muestran:
- Estado del campo geomagnético
- Condiciones del viento solar
- Niveles de ruido
- Condiciones de rayos X

Una sección "Rationale" proporciona una explicación en lenguaje sencillo del pronóstico de hoy. El campo de rationale utiliza colores de fondo y borde temáticos que respetan el tema actual de la aplicación.

### Panel solar y lunar

Muestra una imagen solar en vivo y la fase lunar actual. De forma predeterminada, la imagen solar muestra "Corona (193Å)". Haga clic en la imagen solar para recorrer las longitudes de onda disponibles:

- Corona (193Å)
- Cromosfera (304Å)
- Corona tranquila (171Å)
- Erupciones (94Å)
- Visible (HMI)

### Qué observar

Debajo o al lado de la imagen solar, notas educativas rotativas en lenguaje sencillo describen qué observar en la imagen mostrada actualmente. Las notas rotan automáticamente; no se requiere ninguna acción para avanzarlas. Las notas se actualizan para coincidir con la longitud de onda solar seleccionada actualmente. El fondo del panel educativo está tematizado para coincidir con el tema actual de la aplicación.

### Condiciones de banda HF

Una tabla que muestra las condiciones de día y noche para cada banda de HF. Se muestran cuatro filas de bandas con indicadores de condición tanto para el día como para la noche.

### Condiciones de VHF

Muestra el estado actual de las aperturas de propagación en VHF:

| Condición | Estados | Significado |
|---|---|---|
| Aurora | Cerrada / Abierta | Propagación auroral actual |
| E-Skip NA | Cerrado / Abierto | Propagación por esporádica-E sobre Norteamérica |
| E-Skip EU | Cerrado / Abierto | Propagación por esporádica-E sobre Europa |

### Qué significan (VHF)

Dos notas educativas explican la diferencia entre la propagación auroral y la esporádica-E, lo que le ayuda a comprender las condiciones actuales de VHF. El fondo del panel educativo está tematizado para coincidir con el tema actual de la aplicación.

## Compatibilidad con temas

El Panel de Propagación es totalmente compatible con el tema activo de la aplicación. Los fondos de los paneles, las líneas separadoras, los colores de los bordes y el campo de rationale utilizan colores temáticos. Cuando cambia el tema de la aplicación, el panel actualiza su apariencia en consecuencia.

## Tiempo de espera de red

El panel aplica un tiempo de espera de red de 15 segundos a todas las descargas de datos de meteorología espacial. Si una descarga no se completa dentro de este intervalo, la solicitud se cancela y el panel no mostrará datos obsoletos o parciales. Los datos se reintentan en el siguiente ciclo de actualización.

## Redimensionamiento y posición

El Panel de Propagación de HF recuerda el tamaño y la posición de su ventana. Redimensione el diálogo arrastrando sus bordes. La próxima vez que abra el panel, se restaurará a su tamaño y ubicación anteriores. La geometría se guarda bajo la clave `PropDashboardDialogGeometry` en la configuración de la aplicación.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tarjetas de condiciones actuales | Cinco tarjetas de métricas (SFI, SN, A-index, K-index, X-ray) con información al pasar el cursor que ofrece explicaciones en lenguaje sencillo. |
| Cuadrícula de pronóstico a 3 días | Kp codificado por colores por período de 3 horas UTC para cada uno de los tres días, más filas de riesgo de Kp máximo, R1-R2, R3+ y S1+. |
| Panel solar y lunar | Muestra una imagen solar en vivo (haga clic para recorrer las longitudes de onda) y la fase lunar actual. Etiqueta predeterminada: "Corona (193Å)". |
| Qué observar | Notas educativas rotativas en lenguaje sencillo sobre la imagen solar actual. Se actualizan automáticamente a medida que la imagen cambia. |
| Condiciones de banda HF | Condición de día y noche por fila de banda (4 filas de bandas). |
| Condiciones de VHF | Estados de Aurora, E-Skip NA, E-Skip EU (Cerrada/Cerrado - Abierta/Abierto). |
| Qué significan (VHF) | Dos notas educativas que explican la propagación auroral frente a la esporádica-E. |

## Relacionado

- [Cicle las longitudes de onda de la imaginería solar para desarrollar intuición](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Consulte el flujo solar, el número de manchas solares y el índice K actuales](check-current-solar-flux-sunspot-number-and-k-index.md)
