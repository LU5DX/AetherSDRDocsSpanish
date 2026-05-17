# Panel de Propagación en HF

El Panel de Propagación en HF proporciona una vista rápida de las condiciones de propagación en HF y VHF, incluyendo índices solares actuales, un pronóstico de Kp a 3 días con riesgo de apagones y radiación, condiciones de bandas HF día/noche, imágenes solares y lunares, e indicios de E-esporádica/aurora.

## Abrir el Panel

- Abra el Panel de Propagación en HF mediante `View > Propagation Conditions`.

## Diseño del Panel

El panel está organizado en varias secciones que muestran las condiciones actuales, pronósticos y material didáctico.

### Tarjetas de Condiciones Actuales

Cinco tarjetas muestran los índices solares y geomagnéticos actuales. Pase el cursor sobre cualquier tarjeta para ver una explicación en lenguaje sencillo de lo que significa el valor.

| Métrica | Descripción |
|---|---|
| SFI | Índice de Flujo Solar |
| SN | Número de Manchas Solares |
| A-index | Índice Geomagnético A |
| K-index | Índice Geomagnético K |
| X-ray | Nivel actual de flujo de rayos X |

### Cuadrícula de Pronóstico a 3 Días

Una cuadrícula codificada por colores que muestra los pronósticos de Kp para cada período de 3 horas UTC durante tres días. Debajo de la cuadrícula, filas de riesgo adicionales muestran:

- Kp máximo por día
- R1-R2: Riesgo de apagón de radio (leve a moderado)
- R3+: Riesgo de apagón de radio (fuerte a extremo)
- S1+: Riesgo de tormenta de radiación solar

Al final de la sección de pronóstico, etiquetas de resumen muestran:
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

Debajo o al lado de la imagen solar, notas didácticas rotativas en lenguaje sencillo describen qué observar en la imagen mostrada actualmente. Las notas rotan automáticamente; no se requiere ninguna acción para avanzarlas. Las notas se actualizan para coincidir con la longitud de onda solar seleccionada.

### Condiciones de Bandas HF

Una tabla que muestra las condiciones de día y noche para cada banda de HF. Se muestran cuatro filas de bandas con indicadores de condición tanto para día como para noche.

### Condiciones de VHF

Muestra el estado actual de las aperturas de propagación en VHF:

| Condición | Estados | Significado |
|---|---|---|
| Aurora | Cerrada / Abierta | Propagación auroral actual |
| E-Skip NA | Cerrada / Abierta | Propagación E-esporádica sobre Norteamérica |
| E-Skip EU | Cerrada / Abierta | Propagación E-esporádica sobre Europa |

### Qué Significan (VHF)

Dos notas didácticas explican la diferencia entre la propagación auroral y la E-esporádica, ayudándole a comprender las condiciones actuales de VHF.

## Redimensionamiento y Posición

El Panel de Propagación en HF recuerda el tamaño y la posición de su ventana. Redimensione el diálogo arrastrando sus bordes. La próxima vez que abra el panel, se restaurará a su tamaño y ubicación anteriores. La geometría se guarda bajo la clave `PropDashboardDialogGeometry` en la configuración de la aplicación.

## Control de cada elemento

| Control | Comportamiento |
|---|---|
| Tarjetas de Condiciones Actuales | Cinco tarjetas (SFI, SN, A-index, K-index, X-ray) con información emergente al pasar el cursor que proporciona explicaciones en lenguaje sencillo. |
| Cuadrícula de Pronóstico a 3 Días | Kp codificado por colores por período de 3 horas UTC para cada uno de los tres días, más filas de riesgo Max Kp, R1-R2, R3+ y S1+. |
| Panel Solar y Lunar | Muestra imagen solar en vivo (haga clic para recorrer longitudes de onda) y fase lunar actual. Etiqueta predeterminada: "Corona (193Å)". |
| Qué Observar | Notas didácticas rotativas en lenguaje sencillo sobre la imagen solar actual. Se actualiza automáticamente al cambiar la imagen. |
| Condiciones de Bandas HF | Condición de día y noche por fila de banda (4 filas de banda). |
| Condiciones de VHF | Estados de Aurora, E-Skip NA, E-Skip EU (Cerrada/Abierta). |
| Qué Significan (VHF) | Dos notas didácticas que explican la propagación auroral versus la E-esporádica. |

## Relacionados

- [Cycle solar imagery wavelengths to build intuition](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Check current solar flux, sunspot number and K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
