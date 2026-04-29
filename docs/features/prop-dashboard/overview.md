# Descripción general del Panel de Propagación HF

El Panel de Propagación HF le ofrece una vista rápida de las condiciones solares actuales, un pronóstico geomagnético de 3 días, condiciones de bandas HF de día y de noche, imágenes solares y lunares, y sugerencias de propagación VHF. Úselo para determinar qué bandas probablemente estén abiertas antes de transmitir, o para entender por qué las condiciones se comportan de manera inesperada.

## Antes de comenzar

- No se requiere conexión a radio. El panel obtiene los datos de forma independiente.
- Se necesita una conexión a internet activa para recuperar índices solares, datos de pronóstico e imágenes solares.

## Cómo funciona

Abra el panel desde `View > Propagation Conditions`. El diálogo recupera los datos solares actuales y los presenta en siete áreas distintas que se describen a continuación.

### Tarjetas de Current Conditions

Cinco indicadores de métricas muestran los índices solares y geomagnéticos más importantes de un vistazo: **SFI** (Índice de Flujo Solar), **SN** (Número de Manchas Solares), **A-index**, **K-index** y clase **X-ray**. Cada tarjeta tiene un código de colores que refleja la calidad de las condiciones: el verde indica condiciones favorables, el amarillo indica condiciones inestables o moderadas, y el rojo indica condiciones de tormenta o degradadas. Pase el cursor sobre cualquier tarjeta para leer una descripción en lenguaje sencillo que explica qué significa esa métrica para la propagación HF.

### Cuadrícula de 3-Day Forecast

Muestra los valores Kp para cada período UTC de 3 horas a lo largo de tres días, 24 celdas en total. Cada celda tiene un código de colores según el nivel Kp. Debajo de la cuadrícula Kp, tres filas de riesgo muestran la probabilidad de apagón de radio según la escala NOAA y eventos de tormenta de radiación por día: **R1-R2**, **R3+** y **S1+**. Debajo de la cuadrícula de pronóstico aparecen etiquetas de resumen para el estado del campo geomagnético, la velocidad del viento solar, el ruido atmosférico y el flujo de rayos X.

### Panel Solar And Lunar

Muestra una imagen solar en vivo y la fase actual de la Luna. Al hacer clic en la imagen solar se puede recorrer cinco vistas de longitud de onda:

| Etiqueta | Código |
|---|---|
| Corona (193Å) | 0193 |
| Chromosphere (304Å) | 0304 |
| Quiet Corona (171Å) | 0171 |
| Flaring (94Å) | 0094 |
| Visible (HMI) | HMIIC |

La vista predeterminada es **Corona (193Å)**.

### What To Look For

Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar seleccionada en ese momento. Las notas cambian automáticamente al recorrer las longitudes de onda, ayudándole a desarrollar intuición sobre la actividad solar.

### HF Band Conditions

Muestra las condiciones de propagación de día y de noche en cuatro filas de bandas HF. Cada fila tiene un código de colores: **Good**, **Fair** o **Poor**. Use este panel para identificar qué bandas son más probablemente productivas según su horario de operación y ubicación.

### VHF Conditions

Informa el estado actual de tres trayectos de propagación VHF: **Aurora**, **E-Skip NA** (Norteamérica) y **E-Skip EU** (Europa). Cada indicador muestra **Open** o **Closed**.

### What These Mean (VHF)

Dos notas de aprendizaje fijas explican la diferencia entre la propagación auroral y la esporádica-E, dando contexto a los indicadores de VHF Conditions anteriores.

## Consejos

- El texto de **Rationale** debajo de la cuadrícula de pronóstico ofrece una explicación en lenguaje sencillo de por qué el pronóstico de hoy tiene el aspecto que tiene; léalo para obtener un resumen rápido antes de revisar las métricas individuales.
- Al pasar el cursor sobre una tarjeta de **Current Conditions** se muestra una descripción detallada que explica la importancia de esa métrica para la propagación HF, incluyendo qué bandas se ven más afectadas.
- El panel no requiere un radio Flex conectado. Puede consultarlo antes de encender su estación.

## Relacionados

- [Consultar el flujo solar actual, el número de manchas solares y el K-index](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Determinar qué banda HF está abierta para trabajo de día o de noche](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Estar atento a aperturas esporádicas-E o aurorales en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
- [Recorrer las longitudes de onda de imágenes solares para desarrollar intuición](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Leer las notas de aprendizaje rotativas sobre condiciones solares](read-rotating-learning-notes-about-solar-conditions.md)
