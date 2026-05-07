# Resumen del Panel de Propagación HF

El Panel de Propagación HF le ofrece una vista rápida de las condiciones solares actuales, un pronóstico geomagnético de 3 días, las condiciones de las bandas HF durante el día y la noche, imágenes solares y lunares, y sugerencias de propagación VHF. Úselo para decidir qué bandas están probablemente abiertas antes de transmitir, o para entender por qué las condiciones se comportan de manera inesperada.

## Antes de comenzar

- No se requiere conexión de radio. El panel obtiene datos de forma independiente.
- Se necesita una conexión a Internet activa para recuperar los índices solares, los datos de pronóstico y las imágenes solares.

## Cómo funciona

Abra el panel desde `View > Propagation Conditions`. El diálogo recupera los datos solares actuales y los presenta en siete áreas distintas que se describen a continuación.

### Tarjetas de Condiciones Actuales

Cinco mosaicos de métricas muestran los índices solares y geomagnéticos más importantes de un vistazo: **SFI** (Índice de Flujo Solar), **SN** (Número de Manchas Solares), **Índice A**, **Índice K** y clase de **Rayos X**. Cada tarjeta tiene un código de colores que refleja la calidad de las condiciones: verde indica condiciones favorables, amarillo indica condiciones inestables o moderadas, y rojo indica condiciones de tormenta o degradadas. Pase el cursor sobre cualquier tarjeta para leer una descripción emergente en lenguaje sencillo que explica lo que esa métrica significa para la propagación HF.

### Cuadrícula de Pronóstico de 3 Días

Muestra los valores de Kp para cada período UTC de 3 horas a lo largo de tres días: 24 celdas en total. Cada celda tiene un código de colores según el nivel de Kp. Debajo de la cuadrícula de Kp, tres filas de riesgo muestran la probabilidad de eventos de apagón de radio y tormenta de radiación en la escala NOAA por día: **R1-R2**, **R3+** y **S1+**. Las etiquetas de resumen del estado del campo geomagnético, la velocidad del viento solar, el ruido atmosférico y el flujo de rayos X aparecen debajo de la cuadrícula de pronóstico.

### Panel Solar y Lunar

Muestra una imagen solar en vivo y la fase lunar actual. Al hacer clic en la imagen solar, se cicla a través de cinco vistas de longitud de onda:

| Etiqueta | Código |
|---|---|
| Corona (193Å) | 0193 |
| Cromosfera (304Å) | 0304 |
| Corona Tranquila (171Å) | 0171 |
| Fulguraciones (94Å) | 0094 |
| Visible (HMI) | HMIIC |

La vista predeterminada es **Corona (193Å)**.

### Qué Buscar

Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar seleccionada actualmente. Las notas cambian automáticamente a medida que cicla las longitudes de onda, ayudándole a desarrollar intuición sobre la actividad solar.

### Condiciones de las Bandas HF

Muestra las condiciones de propagación diurna y nocturna en cuatro filas de bandas HF. Cada fila tiene un código de colores: **Buena**, **Regular** o **Mala**. Use este panel para identificar qué bandas son probablemente más productivas para su hora y ubicación de operación.

### Condiciones VHF

Informa el estado actual de tres rutas de propagación VHF: **Aurora**, **E-Skip NA** (Norteamérica) y **E-Skip EU** (Europa). Cada indicador muestra **Abierto** o **Cerrado**.

### Qué Significan Estos (VHF)

Dos notas de aprendizaje fijas explican la diferencia entre la propagación auroral y la esporádica-E, proporcionando contexto para los indicadores de Condiciones VHF anteriores.

## Consejos

- El texto **Rationale** debajo de la cuadrícula de pronóstico proporciona una explicación en lenguaje sencillo de por qué el pronóstico de hoy se ve como es — léalo para obtener un resumen rápido antes de verificar métricas individuales.
- Pasar el cursor sobre una tarjeta de **Current Conditions** muestra una descripción emergente detallada que explica la importancia de la métrica para la propagación HF, incluyendo qué bandas se ven más afectadas.
- El panel no requiere una radio Flex conectada. Puede consultarlo antes de encender su estación.

## Relacionado

- [Verifique el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decida qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Esté atento a aperturas VHF por esporádica-E o aurora](watch-for-vhf-sporadic-e-or-auroral-openings.md)
- [Cicle las longitudes de onda de las imágenes solares para desarrollar intuición](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Lea notas de aprendizaje rotativas sobre las condiciones solares](read-rotating-learning-notes-about-solar-conditions.md)
