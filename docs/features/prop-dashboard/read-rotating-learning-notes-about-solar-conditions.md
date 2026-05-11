# Panel de Propagación de HF

El Panel de Propagación de HF ofrece una vista general de las condiciones de propagación en HF y VHF, que incluye los índices solares actuales, un pronóstico de Kp a 3 días con riesgo de apagones y radiación, condiciones de banda HF de día/noche, imágenes solares y lunares, e indicios de propagación E esporádica/auroral.

## Cómo abrir el panel

- Abra el Panel de Propagación de HF mediante `View > Propagation Conditions`.

## Diseño del panel

El panel está organizado en varias secciones que muestran las condiciones actuales, pronósticos y material de aprendizaje.

### Tarjetas de Condiciones Actuales

Cinco mosaicos métricos muestran los índices solares y geomagnéticos actuales. Pase el cursor sobre cualquier mosaico para ver una explicación en lenguaje sencillo del significado del valor.

| Métrica | Descripción |
|---|---|
| SFI | Índice de flujo solar |
| SN | Número de manchas solares |
| A-index | Índice geomagnético A |
| K-index | Índice geomagnético K |
| X-ray | Nivel actual de flujo de rayos X |

### Cuadrícula de Pronóstico a 3 Días

Una cuadrícula codificada por colores que muestra los pronósticos de Kp para cada período de 3 horas UTC durante tres días. Debajo de la cuadrícula, filas de riesgo adicionales muestran:

- Kp máximo por día
- R1-R2: Riesgo de apagón de radio (menor a moderado)
- R3+: Riesgo de apagón de radio (fuerte a extremo)
- S1+: Riesgo de tormenta de radiación solar

En la parte inferior de la sección de pronóstico, las etiquetas de resumen muestran:
- Estado del campo geomagnético
- Condiciones del viento solar
- Niveles de ruido
- Condiciones de rayos X

Una sección "Rationale" proporciona una explicación en lenguaje sencillo del pronóstico del día.

### Panel Solar y Lunar

Muestra una imagen solar en vivo y la fase lunar actual. De forma predeterminada, la imagen solar muestra "Corona (193Å)". Haga clic en la imagen solar para recorrer las longitudes de onda disponibles:

- Corona (193Å)
- Cromosfera (304Å)
- Corona Tranquila (171Å)
- Fulguraciones (94Å)
- Visible (HMI)

### Qué Observar

Debajo o al lado de la imagen solar, notas de aprendizaje rotativas en lenguaje sencillo describen qué observar en la imagen mostrada actualmente. Las notas rotan automáticamente; no se requiere ninguna acción para avanzarlas. Las notas se actualizan para coincidir con la longitud de onda solar seleccionada actualmente.

### Condiciones de Banda HF

Una tabla que muestra las condiciones de día y noche para cada banda de HF. Se muestran cuatro filas de bandas con indicadores de condición tanto para día como para noche.

### Condiciones de VHF

Muestra el estado actual de las aperturas de propagación en VHF:

| Condición | Estados | Significado |
|---|---|---|
| Aurora | Cerrada / Abierta | Propagación auroral actual |
| E-Skip NA | Cerrada / Abierta | Propagación E esporádica sobre Norteamérica |
| E-Skip EU | Cerrada / Abierta | Propagación E esporádica sobre Europa |

### Qué Significan (VHF)

Dos notas de aprendizaje explican la diferencia entre la propagación auroral y la E esporádica, ayudándole a comprender las condiciones actuales de VHF.

## Ajuste de la Apariencia del Diálogo

El Panel de Propagación de HF admite el modo de ventana sin marco. Cuando el modo sin marco está habilitado, el diálogo muestra una barra de título personalizada en lugar de la decoración de ventana del sistema.

Este modo se controla mediante la configuración `FramelessWindow` en los ajustes de la aplicación. Cuando se establece en "True" (el valor predeterminado), el diálogo usa el modo sin marco. Si la configuración es "False", el diálogo usa el marco de ventana del sistema.

Cuando el modo sin marco está activo:
- Se muestra una barra de título personalizada etiquetada como "HF Propagation Dashboard" en la parte superior.
- Se puede cambiar el tamaño del diálogo arrastrando sus bordes.
- Los márgenes del contenido interno se ajustan ligeramente para tener en cuenta la barra de título personalizada.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Tarjetas de Condiciones Actuales | Cinco mosaicos métricos (SFI, SN, A-index, K-index, X-ray) con información emergente al pasar el cursor que proporciona explicaciones en lenguaje sencillo. |
| Cuadrícula de Pronóstico a 3 Días | Kp codificado por colores por período de 3 horas UTC para cada uno de los tres días, más las filas de riesgo Kp máximo, R1-R2, R3+ y S1+. |
| Panel Solar y Lunar | Muestra una imagen solar en vivo (haga clic para recorrer las longitudes de onda) y la fase lunar actual. Etiqueta predeterminada: "Corona (193Å)". |
| Qué Observar | Notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual. Se actualiza automáticamente a medida que la imagen se recorre. |
| Condiciones de Banda HF | Condición de día y noche por fila de banda (4 filas de bandas). |
| Condiciones de VHF | Estados de Aurora, E-Skip NA, E-Skip EU (Cerrada/Abierta). |
| Qué Significan (VHF) | Dos notas de aprendizaje que explican la propagación auroral vs. la E esporádica. |

## Relacionados

- [Cycle solar imagery wavelengths to build intuition](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
