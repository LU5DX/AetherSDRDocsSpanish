# Habilitar el squelch desde el panel VFO

El squelch silencia el audio de un slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para eliminar el ruido de fondo en modos FM, AM o digitales cuando no hay señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice objetivo debe estar abierto. Si no lo está, haga clic en la bandera del marcador VFO en la pantalla del espectro de ese slice.
- Si el panel VFO está colapsado a la tira de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera del marcador VFO en la pantalla del espectro del slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Haga clic en el **botón Squelch** para habilitar el squelch. El botón se activa y el squelch se aplica al slice de inmediato.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o derecha para establecer el umbral. El rango válido es 0–100.

Para deshabilitar el squelch, haga clic nuevamente en el **botón Squelch**.

## Qué hace cada control

| Control                      | Predeterminado                                                                                                                         | Rango válido                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Botón Squelch                | Apagado                                                                                                                                | Encendido / Apagado                                                                                                      |
| Control deslizante de squelch | —                                                                                                                                      | 0–100                                                                                                                    |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de conmutador DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Activa o desactiva la tira del canal de audio Aetherial, el conjunto unificado de DSP de TX/RX (v0.9.8).                             | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Ni el estado del botón ni la posición del control deslizante se conservan como una clave de AppSettings de AetherSDR; ambos reflejan el estado en vivo de la radio.

## Consejos

- Ajuste el control deslizante justo por encima del piso de ruido para evitar que el audio se corte y se active con señales débiles.
- El umbral de squelch interactúa con la configuración de AGC. Si cambia el modo AGC usando el **combo AGC**, es posible que deba reajustar el control deslizante de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel VFO recibió dos nuevos botones de lanzamiento en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Botón no marcable con estilo de conmutador DSP del lado de la radio. |
| Botón AetherVoice | Activa o desactiva la tira del canal de audio Aetherial, el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no marcable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del control deslizante de nivel DSP. Cuando los botones DSP del lado de la radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado de la radio, el control deslizante de nivel DSP correspondiente ahora se coloca en la pila de niveles compartida al inicio. Anteriormente, faltaba el control deslizante de nivel hasta que el usuario activaba manualmente el botón DSP. Esto soluciona el problema #startup-slider.

### Control deslizante de nivel DSP

Aparece una fila compartida de **control deslizante de nivel DSP** debajo de la cuadrícula de botones DSP. El control deslizante se dirige al botón DSP con nivel que se haya encendido más recientemente. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del control deslizante siempre está presente en el diseño. Cuando no hay ningún DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila se atenúa y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se habilita un botón DSP compatible.

Objetivos DSP con nivel compatibles con el control deslizante:

| Objetivo | Controlado por |
|---|---|
| NR | `setNrLevel` |
| NB | `setNbLevel` |
| ANF | `setAnfLevel` |
| NRL | `setNrlLevel` |
| NRS | `setNrsLevel` |
| NRF | `setNrfLevel` |
| ANFL | `setAnflLevel` |

El rango del control deslizante es 0–100. El valor de nivel no se conserva como una clave de AppSettings de AetherSDR; refleja el estado en vivo de la radio.

## Corrección de la etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desfase de 0.1 kHz que anteriormente afectaba las lecturas de filtro en modos SSB y digitales (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la visualización del filtro del applet de RX.

## Relacionados

- [Ajustar ganancia AF y paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
