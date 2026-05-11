# Habilitar el squelch desde el panel VFO

El squelch silencia el audio de un slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para silenciar el ruido de fondo en FM, AM o modos digitales cuando no hay señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice objetivo debe estar abierto. Si no lo está, haga clic en la bandera marcadora VFO en la pantalla del espectro para ese slice.
- Si el panel VFO está colapsado en la tira de solo frecuencia, haga clic en él una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera marcadora VFO en la pantalla del espectro del slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Haga clic en el **botón Squelch** para habilitar el squelch. El botón se activa y el squelch se aplica al slice inmediatamente.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o derecha para establecer el umbral. El rango válido es 0–100.

Para deshabilitar el squelch, haga clic en el **botón Squelch** nuevamente.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                                     | Rango válido                                                                                                              |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Botón Squelch                  | Apagado                                                                                                                                  | Encendido / Apagado                                                                                                       |
| Control deslizante de squelch  | —                                                                                                                                        | 0–100                                                                                                                     |
| Botón ADSP (pestaña DSP)       | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene estilo de un conmutador DSP del lado de la radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP)| Activa la barra de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                          | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la barra.            |

Ni el estado del botón ni la posición del control deslizante se conservan como una clave de AppSettings de AetherSDR; ambos reflejan el estado en vivo de la radio.

## Consejos

- Ajuste el control deslizante justo por encima del piso de ruido para evitar que el audio se corte y se active con señales débiles.
- El umbral de squelch interactúa con la configuración del AGC. Si cambia el modo AGC usando el **combo AGC**, es posible que necesite reajustar el control deslizante de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel VFO recibió dos nuevos botones de inicio en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Botón no marcable con estilo de conmutador DSP del lado de la radio. |
| Botón AetherVoice | Activa la barra de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no marcable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del control deslizante de nivel DSP. Cuando los botones DSP del lado de la radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado de la radio, el control deslizante de nivel DSP correspondiente ahora se inserta en la pila de niveles compartida al inicio. Anteriormente, el control deslizante de nivel faltaba hasta que el usuario activaba manualmente el botón DSP. Esto soluciona el problema #startup-slider.

### Control deslizante de nivel DSP

Aparece una fila compartida de **control deslizante de nivel DSP** debajo de la cuadrícula de botones DSP. El control deslizante apunta al último botón DSP con nivel que se encendió. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del control deslizante siempre está presente en el diseño. Cuando ningún DSP con nivel está activo — o solo RNN, ANFT o APF están encendidos — la fila se atenúa y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se habilita un botón DSP compatible.

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

La **etiqueta de ancho de filtro** en el panel VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desfase de 0.1 kHz que antes afectaba las lecturas de filtro en modo SSB y digital (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la visualización del filtro del applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se deshabilita cuando el slice está configurado en modo RTTY. Este cambio soluciona el problema #2504, donde el squelch bloqueaba señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el control deslizante de squelch se deshabilitan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para modos digitales y CW.

Si el squelch estaba habilitado al cambiar al modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Relacionado

- [Ajustar la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
