# Descripción general del panel de propagación de HF

El panel de propagación de HF le ofrece una vista de un vistazo de las condiciones solares actuales, un pronóstico geomagnético de 3 días, las condiciones de las bandas de HF de día y de noche, imágenes solares y lunares, y sugerencias de propagación de VHF. Úselo para decidir qué bandas probablemente estén abiertas antes de transmitir, o para entender por qué las condiciones se comportan de manera inesperada.

## Antes de comenzar

- No se requiere conexión de radio. El panel obtiene los datos de forma independiente.
- Se necesita una conexión a internet activa para recuperar los índices solares, los datos de pronóstico y las imágenes solares.

## Cómo funciona

Abra el panel desde `View > Propagation Conditions`. El diálogo recupera los datos solares actuales y los presenta en siete áreas distintas que se describen a continuación. El diálogo recuerda su geometría entre sesiones. El panel respeta el tema actual de la aplicación para los colores de fondo y de borde.

El panel aplica un tiempo de espera de transferencia de 15 segundos a todas las consultas de datos de clima espacial. Si una consulta no se completa dentro de ese tiempo, el panel deja de esperarla y continúa mostrando los datos que ya ha recibido. Esto evita que el panel parezca congelado cuando la red es lenta o una fuente de datos no responde.

### Tarjetas de condiciones actuales

Cinco mosaicos de métricas muestran los índices solares y geomagnéticos más importantes de un vistazo: **SFI** (índice de flujo solar), **SN** (número de manchas solares), **índice A**, **índice K** y **clase de rayos X**. Cada tarjeta está codificada por colores para reflejar la calidad de las condiciones: verde indica condiciones favorables, amarillo indica condiciones inestables o moderadas, y rojo indica condiciones de tormenta o degradadas. Pase el cursor sobre cualquier tarjeta para leer una información sobre herramientas en lenguaje sencillo que explica qué significa esa métrica para la propagación de HF.

### Cuadrícula de pronóstico de 3 días

Muestra los valores de Kp para cada período de 3 horas UTC durante tres días — 24 celdas en total. Cada celda está codificada por colores según el nivel de Kp. Debajo de la cuadrícula de Kp, tres filas de riesgo muestran la probabilidad de eventos de apagón de radio y tormenta de radiación de la escala NOAA por día: **R1-R2**, **R3+** y **S1+**. Las etiquetas de resumen para el estado del campo geomagnético, la velocidad del viento solar, el ruido atmosférico y el flujo de rayos X aparecen debajo de la cuadrícula de pronóstico.

### Panel solar y lunar

Muestra una imagen solar en vivo y la fase lunar actual. Al hacer clic en la imagen solar se recorren cinco vistas de longitud de onda:

| Etiqueta | Código |
|---|---|
| Corona (193Å) | 0193 |
| Cromosfera (304Å) | 0304 |
| Corona tranquila (171Å) | 0171 |
| Erupción (94Å) | 0094 |
| Visible (HMI) | HMIIC |

La vista predeterminada es **Corona (193Å)**.

### Qué buscar

Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar actualmente seleccionada. Las notas cambian automáticamente a medida que recorre las longitudes de onda, lo que le ayuda a desarrollar intuición sobre la actividad solar.

### Condiciones de banda de HF

Muestra las condiciones de propagación de día y de noche en cuatro filas de bandas de HF. Cada fila está codificada por colores: **Buena**, **Regular** o **Mala**. Use este panel para identificar qué bandas son más probablemente productivas para su horario y ubicación de operación.

### Condiciones de VHF

Informa el estado actual de tres rutas de propagación de VHF: **Aurora**, **E-Skip NA** (Norteamérica) y **E-Skip EU** (Europa). Cada indicador muestra **Abierto** o **Cerrado**.

### Qué significan estos (VHF)

Dos notas fijas de aprendizaje explican la diferencia entre la propagación auroral y la dispersión esporádica E, proporcionando contexto para los indicadores de condiciones de VHF anteriores.

## Consejos

- El texto **Rationale** debajo de la cuadrícula de pronóstico proporciona una explicación en lenguaje sencillo de por qué el pronóstico de hoy se ve como se ve — léalo para obtener un resumen rápido antes de revisar métricas individuales.
- Pasar el cursor sobre una tarjeta de **Current Conditions** muestra una información sobre herramientas detallada que explica la importancia de la métrica para la propagación de HF, incluyendo qué bandas se ven más afectadas.
- El panel no requiere una radio Flex conectada. Puede consultarlo antes de encender su estación.
- Si el panel parece dejar de actualizarse, espere a que expire el tiempo de espera de transferencia de 15 segundos. El panel continuará con los datos que ya ha recibido en lugar de esperar indefinidamente.

## Relacionado

- [Consulte el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Vea el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decida qué banda de HF está abierta para trabajo de día o de noche](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Esté atento a aperturas de E esporádico o aurora en VHF](watch-for-vhf-sporadic-e-or-auroral-openings.md)
- [Recorra las longitudes de onda de imágenes solares para desarrollar intuición](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Lea notas rotativas de aprendizaje sobre las condiciones solares](read-rotating-learning-notes-about-solar-conditions.md)
