# Panel de Propagación de HF

El Panel de Propagación de HF ofrece una vista rápida de las condiciones de propagación en HF y VHF, incluyendo índices solares actuales, un pronóstico de Kp a 3 días con riesgo de apagones y radiación, condiciones de banda HF día/noche, imágenes solares y lunares, e indicios de E-esporádica/aurora.

## Abrir el Panel

- Abra el Panel de Propagación de HF mediante `View > Propagation Conditions`.

## Diseño del Panel

El panel está organizado en varias secciones que muestran condiciones actuales, pronósticos y material de aprendizaje.

### Tarjetas de Condiciones Actuales

Cinco mosaicos de métricas muestran los índices solares y geomagnéticos actuales. Pase el cursor sobre cualquier mosaico para ver una explicación en lenguaje sencillo de lo que significa el valor.

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

En la parte inferior de la sección de pronóstico, etiquetas de resumen muestran:
- Estado del campo geomagnético
- Condiciones del viento solar
- Niveles de ruido
- Condiciones de rayos X

Una sección "Rationale" proporciona una explicación en lenguaje sencillo del pronóstico del día. El campo rationale utiliza colores de fondo y borde temáticos que respetan el tema actual de la aplicación.

### Panel Solar y Lunar

Muestra una imagen solar en vivo y la fase lunar actual. De forma predeterminada, la imagen solar muestra "Corona (193Å)". Haga clic en la imagen solar para recorrer las longitudes de onda disponibles:

- Corona (193Å)
- Cromosfera (304Å)
- Corona Tranquila (171Å)
- Fulguraciones (94Å)
- Visible (HMI)

### Qué Buscar

Debajo o al lado de la imagen solar, notas de aprendizaje rotativas en lenguaje sencillo describen qué observar en la imagen mostrada actualmente. Las notas rotan automáticamente; no se requiere ninguna acción para avanzarlas. Las notas se actualizan para coincidir con la longitud de onda solar seleccionada actualmente. El fondo del panel de aprendizaje está tematizado para coincidir con el tema actual de la aplicación.

### Condiciones de Banda HF

Una tabla que muestra las condiciones de día y noche para cada banda de HF. Se muestran cuatro filas de bandas con indicadores de condición tanto para el día como para la noche.

### Condiciones de VHF

Muestra el estado actual de las aperturas de propagación en VHF:

| Condición | Estados | Significado |
|---|---|---|
| Aurora | Cerrada / Abierta | Propagación auroral actual |
| E-Skip NA | Cerrada / Abierta | Propagación E-esporádica sobre Norteamérica |
| E-Skip EU | Cerrada / Abierta | Propagación E-esporádica sobre Europa |

### Qué Significan (VHF)

Dos notas de aprendizaje explican la diferencia entre la propagación auroral y la E-esporádica, ayudándole a comprender las condiciones actuales de VHF. El fondo del panel de aprendizaje está tematizado para coincidir con el tema actual de la aplicación.

## Soporte de Temas

El Panel de Propagación es compatible con el tema activo de la aplicación. Los fondos de los paneles, las líneas separadoras, los colores de los bordes y el campo de rationale utilizan colores temáticos. Cuando cambie el tema de la aplicación, el panel actualizará su apariencia en consecuencia.

## Redimensionamiento y Posicionamiento

El Panel de Propagación de HF recuerda el tamaño y la posición de su ventana. Redimensione el cuadro de diálogo arrastrando sus bordes. La próxima vez que abra el panel, se restaurará a su tamaño y ubicación anteriores. La geometría se guarda bajo la clave `PropDashboardDialogGeometry` en la configuración de la aplicación.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Tarjetas de Condiciones Actuales | Cinco mosaicos de métricas (SFI, SN, A-index, K-index, X-ray) con información emergente al pasar el cursor que proporciona explicaciones en lenguaje sencillo. |
| Cuadrícula de Pronóstico a 3 Días | Kp codificado por colores por período de 3 horas UTC para cada uno de los tres días, más filas de riesgo de Kp máximo, R1-R2, R3+ y S1+. |
| Panel Solar y Lunar | Muestra una imagen solar en vivo (haga clic para recorrer longitudes de onda) y la fase lunar actual. Etiqueta predeterminada: "Corona (193Å)". |
| Qué Buscar | Notas de aprendizaje rotativas en lenguaje sencillo sobre la imagen solar actual. Se actualiza automáticamente a medida que la imagen cambia. |
| Condiciones de Banda HF | Condición de día y noche por fila de banda (4 filas de bandas). |
| Condiciones de VHF | Estados de Aurora, E-Skip NA, E-Skip EU (Cerrada/Abierta). |
| Qué Significan (VHF) | Dos notas de aprendizaje que explican la propagación auroral versus la E-esporádica. |

## Relacionados

- [Cycle solar imagery wavelengths to build intuition](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
