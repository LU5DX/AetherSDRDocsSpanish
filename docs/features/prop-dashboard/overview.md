# Descripción general del panel de propagación HF

El panel de propagación HF le ofrece una vista rápida de las condiciones solares actuales, un pronóstico geomagnético de 3 días, las condiciones de las bandas HF de día y de noche, imágenes solares y lunares, y sugerencias para propagación VHF. Úselo para decidir qué bandas probablemente están abiertas antes de transmitir, o para entender por qué las condiciones se comportan de manera inesperada.

## Antes de comenzar

- No se requiere conexión de radio. El panel obtiene datos de forma independiente.
- Se necesita una conexión a Internet activa para recuperar índices solares, datos de pronóstico e imágenes solares.

## Cómo funciona

Abra el panel desde `View > Propagation Conditions`. El diálogo recupera los datos solares actuales y los presenta en siete áreas distintas, descritas a continuación.

### Tarjetas de condiciones actuales

Cinco mosaicos de métricas muestran los índices solares y geomagnéticos más importantes de un vistazo: **SFI** (Índice de flujo solar), **SN** (Número de manchas solares), **índice A**, **índice K** y **clase de rayos X**. Cada tarjeta tiene un código de colores que refleja la calidad de las condiciones: verde indica condiciones favorables, amarillo indica condiciones inestables o moderadas, y rojo indica condiciones de tormenta o degradadas. Pase el cursor sobre cualquier tarjeta para leer una descripción emergente en lenguaje sencillo que explica lo que significa esa métrica para la propagación HF.

### Cuadrícula de pronóstico de 3 días

Muestra los valores de Kp para cada período de 3 horas UTC durante tres días: 24 celdas en total. Cada celda tiene un código de colores según el nivel de Kp. Debajo de la cuadrícula de Kp, tres filas de riesgo muestran la probabilidad de eventos de apagón de radio y tormenta de radiación a escala NOAA por día: **R1-R2**, **R3+** y **S1+**. Las etiquetas de resumen del estado del campo geomagnético, la velocidad del viento solar, el ruido atmosférico y el flujo de rayos X aparecen debajo de la cuadrícula de pronóstico.

### Panel solar y lunar

Muestra una imagen solar en vivo y la fase lunar actual. Al hacer clic en la imagen solar, se cicla a través de cinco vistas de longitud de onda:

| Etiqueta | Código |
|---|---|
| Corona (193Å) | 0193 |
| Cromosfera (304Å) | 0304 |
| Corona en calma (171Å) | 0171 |
| Erupción (94Å) | 0094 |
| Visible (HMI) | HMIIC |

La vista predeterminada es **Corona (193Å)**.

### Qué buscar

Muestra notas rotativas en lenguaje sencillo que explican qué observar en la imagen solar seleccionada actualmente. Las notas cambian automáticamente al ciclar longitudes de onda, ayudándole a desarrollar intuición sobre la actividad solar.

### Condiciones de las bandas HF

Muestra las condiciones de propagación diurnas y nocturnas en cuatro filas de bandas HF. Cada fila tiene un código de colores: **Buena**, **Regular** o **Mala**. Use este panel para identificar qué bandas son probablemente más productivas para su horario y ubicación de operación.

### Condiciones VHF

Informa el estado actual de tres rutas de propagación VHF: **Aurora**, **E-Skip NA** (Norteamérica) y **E-Skip EU** (Europa). Cada indicador muestra **Abierta** o **Cerrada**.

### Qué significan (VHF)

Dos notas de aprendizaje fijas explican la diferencia entre la propagación auroral y la E esporádica, proporcionando contexto para los indicadores de condiciones VHF anteriores.

## Consejos

- El texto **Justificación** debajo de la cuadrícula de pronóstico proporciona una explicación en lenguaje sencillo de por qué el pronóstico de hoy se ve como se ve — léalo para obtener un resumen rápido antes de revisar métricas individuales.
- Pasar el cursor sobre una tarjeta de **condiciones actuales** muestra una descripción emergente detallada que explica la importancia de la métrica para la propagación HF, incluyendo qué bandas se ven más afectadas.
- El panel no requiere una radio Flex conectada. Puede consultarlo antes de encender su estación.

## Modo sin marco

El panel de propagación admite el modo de ventana sin marco. Cuando el modo sin marco está habilitado, se muestra una barra de título personalizada en la parte superior del diálogo. El diálogo respeta automáticamente la configuración global `FramelessWindow` en las preferencias de la aplicación. Para alternar este comportamiento, establezca `FramelessWindow` en `True` o `False` en `Settings > General > Frameless Window`. Al cambiar entre modos, el diálogo conserva su geometría y estado de visibilidad.

## Relacionados

- [Consultar el flujo solar actual, el número de manchas solares y el índice K](check-current-solar-flux-sunspot-number-and-k-index.md)
- [Ver el pronóstico de Kp de 3 días y el riesgo de apagón](see-the-3-day-kp-forecast-and-blackout-risk.md)
- [Decidir qué banda HF está abierta para trabajo diurno o nocturno](decide-which-hf-band-is-open-for-day-or-night-work.md)
- [Observar aperturas VHF por E esporádica o aurora](watch-for-vhf-sporadic-e-or-auroral-openings.md)
- [Ciclar longitudes de onda de imágenes solares para desarrollar intuición](cycle-solar-imagery-wavelengths-to-build-intuition.md)
- [Leer notas de aprendizaje rotativas sobre condiciones solares](read-rotating-learning-notes-about-solar-conditions.md)
