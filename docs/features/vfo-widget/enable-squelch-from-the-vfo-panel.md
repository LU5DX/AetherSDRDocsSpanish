# Habilitar el squelch desde el panel del VFO

El squelch silencia el audio de un slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para silenciar el ruido de fondo en FM, AM o modos digitales cuando no hay señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El panel del VFO para el slice objetivo debe estar abierto. Si no lo está, haga clic en la bandera marcadora del VFO en la pantalla del espectro para ese slice.
- Si el panel del VFO está colapsado a la tira de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel del VFO haciendo clic en la bandera marcadora del VFO en la pantalla del espectro para el slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel del VFO.
3. Haga clic en el **botón Squelch** para habilitar el squelch. El botón se activa y el squelch se aplica al slice de inmediato.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o derecha para establecer el umbral. El rango válido es 0–100.

Para deshabilitar el squelch, haga clic en el **botón Squelch** nuevamente.

## Qué hace cada control

| Control                          | Valor predeterminado                                                                                                                 | Rango válido                                                                                                               |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Predeterminado del radio                                                                                                             | Lista de antenas del radio                                                                                                 |
| Botón de antena TX               | Predeterminado del radio                                                                                                             | Lista de antenas del radio (puertos solo RX excluidos)                                                                     |
| Visualización de frecuencia      | Frecuencia actual del slice                                                                                                          | 0.001–50000 MHz                                                                                                            |
| Etiqueta de ancho de filtro      | Ancho de banda del filtro actual                                                                                                     | Preajustes de filtro por modo                                                                                              |
| Control deslizante AF Gain (pestaña Audio) | 100                                                                                                                                  | 0–100                                                                                                                      |
| Control deslizante Pan (pestaña Audio)     | 50                                                                                                                                   | 0–100                                                                                                                      |
| Botón Mute (pestaña Audio)       | Apagado                                                                                                                              | Encendido / Apagado                                                                                                        |
| Botón Squelch (pestaña Audio)    | Apagado                                                                                                                              | Encendido / Apagado                                                                                                        |
| Control deslizante Squelch (pestaña Audio) | —                                                                                                                                    | 0–100                                                                                                                      |
| Combo AGC (pestaña Audio)        | FAST                                                                                                                                 | FAST / MED / SLOW / OFF                                                                                                    |
| Combo Mode (pestaña Mode)        | USB                                                                                                                                  | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY                                                       |
| Botones de preajuste de filtro (pestaña Mode) | —                                                                                                                                    | Por preajuste guardado                                                                                                     |
| Botones RIT / XIT (pestaña X/RIT) | Apagado                                                                                                                              | Encendido / Apagado                                                                                                        |
| Combo de canal DAX (pestaña DAX) | Apagado                                                                                                                              | Apagado / 1–8                                                                                                              |
| Botón de grosor del marcador     | 1 px                                                                                                                                 | Apagado / 1 px / 3 px                                                                                                     |
| Botón de bordes del filtro       | Mostrado                                                                                                                             | Encendido / Apagado                                                                                                        |
| Alternar colapso                 | Expandido                                                                                                                            | Encendido / Apagado                                                                                                        |
| Botón ADSP (pestaña DSP)         | Abre el diálogo de configuración AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de un botón de alternancia DSP del lado del radio pero no es marcable. Al hacer clic, abre y enfoca el diálogo no modal AetherDSP Settings. |
| Botón AetherVoice (pestaña DSP)  | Alterna la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                                      | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Ni el estado del botón ni la posición del control deslizante se persisten como una clave de AppSettings de AetherSDR — ambos reflejan el estado en vivo del radio.

## Consejos

- Ajuste el control deslizante justo por encima del piso de ruido para evitar que el audio entre y salga en señales débiles.
- El umbral de squelch interactúa con la configuración de AGC. Si cambia el modo AGC usando el **combo AGC**, es posible que necesite reajustar el control deslizante de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel del VFO recibió dos nuevos botones de lanzamiento en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo de configuración AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Botón no marcable con estilo de alternancia DSP del lado del radio. |
| Botón AetherVoice | Alterna la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no marcable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del control deslizante de nivel DSP. Cuando los botones DSP del lado del radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado del radio, el control deslizante de nivel DSP correspondiente ahora se empuja a la pila de niveles compartida al inicio. Anteriormente, el control deslizante de nivel faltaba hasta que el usuario alternaba manualmente el botón DSP. Esto corrige el problema #startup-slider.

### Control deslizante de nivel DSP

Aparece una fila de **control deslizante de nivel DSP** compartida debajo de la cuadrícula de botones DSP. El control deslizante se dirige al botón DSP de nivel que se encendió más recientemente. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del control deslizante siempre está presente en el diseño. Cuando ningún DSP de nivel está activo — o solo RNN, ANFT o APF está encendido — la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se habilita un botón DSP compatible.

Objetivos DSP de nivel compatibles con el control deslizante:

| Objetivo | Controlado por |
|---|---|
| NR | `setNrLevel` |
| NB | `setNbLevel` |
| ANF | `setAnfLevel` |
| NRL | `setNrlLevel` |
| NRS | `setNrsLevel` |
| NRF | `setNrfLevel` |
| ANFL | `setAnflLevel` |

El rango del control deslizante es 0–100. El valor de nivel no se persiste como una clave de AppSettings de AetherSDR — refleja el estado en vivo del radio.

## Corrección de la etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel del VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas de filtro en modos SSB y digitales (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la visualización del filtro del applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se deshabilita cuando el slice está configurado en modo RTTY. Este cambio aborda el problema #2504, donde el squelch estaba bloqueando señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el control deslizante de squelch se deshabilitan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para modos digitales y CW.

Si el squelch estaba habilitado al cambiar al modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Cambios en la selección de antena en v26.5.2.1

A partir de v26.5.2.1, los menús de selección de antena RX y TX en el panel del VFO se han mejorado:

| Cambio | Descripción |
|---|---|
| Menú de antena RX | Ahora usa `rxAntennaList()` del slice cuando está disponible, recurriendo a la lista maestra de antenas del radio. Cada elemento del menú almacena el nombre de la antena como dato, y el texto del elemento se genera mediante `antennaMenuLabel()` para un formato consistente. |
| Menú de antena TX | Usa el método `txAntennaOptions()` para construir la lista, que excluye automáticamente los puertos de antena solo RX. Las antenas con nombres que comienzan con "RX" se filtran. El ayudante `likelyTxAntennaFallbackToken()` determina qué antenas son probablemente capaces de TX cuando no hay una lista de antenas TX dedicada disponible. |
| Tooltip y sugerencia de estado | Cada elemento del menú ahora muestra el nombre de antena sin procesar como tooltip y sugerencia de estado, proporcionando visibilidad del nombre completo cuando la etiqueta formateada está truncada. |

### Lógica de filtrado de antena TX

El menú de antena TX usa la siguiente lógica para determinar qué antenas mostrar:

1. Si hay una lista de antenas TX dedicada disponible del radio, úsela directamente.
2. De lo contrario, filtre la lista maestra de antenas para excluir puertos que comiencen con "RX".
3. El ayudante `likelyTxAntennaFallbackToken()` identifica antenas capaces de TX verificando si comienzan con "ANT", "TX" o son igual a "XVTR".

## Cambios en la entrada de frecuencia en v26.5.2.1

La lógica de entrada de frecuencia para bandas XVTR se ha actualizado en v26.5.2.1:

| Cambio | Descripción |
|---|---|
| Límite máximo de frecuencia | Aumentado de 450 MHz a 50000 MHz para soportar bandas de microondas. |
| Conveniencia de banda de 3 dígitos | La inserción automática de decimal (por ejemplo, 1446 → 144.6) ahora solo se aplica cuando el slice está en una banda de 100–999 MHz. Para bandas de 23cm y superiores, un entero simple se interpreta como el valor completo en MHz (por ejemplo, 1296 significa 1296 MHz, no 129.6 MHz). |

### Reglas de entrada de frecuencia para bandas XVTR

Al ingresar frecuencias en bandas XVTR:

- **Banda de 100–999 MHz**: Ingrese un entero simple con al menos 4 dígitos para que el decimal se inserte automáticamente después del 3er dígito (por ejemplo, 144600 → 144.600, 14696 → 146.96).
- **1000 MHz y superior**: Ingrese el valor completo en MHz directamente (por ejemplo, 1296 para 23cm significa 1296.000 MHz).
- Siempre puede ingresar un punto decimal manualmente para omitir la inserción automática.

## Cambios en la entrada de frecuencia en v26.5.3

La lógica de entrada de frecuencia se ha actualizado para admitir la entrada explícita en MHz en bandas altas:

| Cambio | Descripción |
|---|---|
| Entrada explícita en MHz | Cuando se ingresa un valor de frecuencia mayor a 54.0 con un punto decimal explícito (por ejemplo, "144.200"), ahora se trata como MHz y se acepta para cualquier banda, incluyendo bandas no XVTR. Anteriormente, ingresar "144.200" en una banda no XVTR sería rechazado por estar fuera de rango. |
| Análisis normalizado | El texto ahora se normaliza usando `FrequencyEntryParser::normalizedMhzText()` que maneja el formato "14.225.000" eliminando puntos más allá del primero. |
| Validación de rango | El límite máximo de frecuencia de 50000 MHz se aplica a todas las bandas cuando se usa un punto decimal explícito, coincidiendo con el comportamiento existente para bandas XVTR. |

### Reglas de entrada de frecuencia en v26.5.3

Al ingresar frecuencias:

- **Entrada explícita en MHz**: Ingrese una frecuencia con un punto decimal (por ejemplo, "14.225", "144.200", "1296.000") para que se trate como MHz directamente. Los valores superiores a 54.0 MHz se aceptan cuando hay un punto decimal explícito presente.

- **Entrada de entero simple (bandas no XVTR, igual o inferior a 54.0 MHz)**: Ingrese un entero simple para que se analice de la siguiente manera:
  - Valores por debajo de 54000: Tratados como kHz (por ejemplo, 14225 = 14.225 MHz)
  - Valores por encima de 54000: Tratados como Hz (por ejemplo, 14225000 = 14.225 MHz)

- **Entrada de entero simple (bandas XVTR, superiores a 54.0 MHz)**: Un entero simple se trata como MHz directamente, con la regla de conveniencia de banda de 3 dígitos aplicada para bandas de 100–999 MHz.

## Comportamiento del slice bloqueado en v26.5.3

A partir de v26.5.3, cuando un slice está bloqueado, se aplican los siguientes comportamientos:

| Comportamiento | Descripción |
|---|---|
| Notificación de sintonía bloqueada | Cuando intenta desplazar la rueda del ratón sobre un slice bloqueado, se muestra una superposición visual `LOCKED` en la visualización de frecuencia para indicar que la sintonía está bloqueada. |
| Cancelación de entrada directa | Si comienza la entrada de frecuencia directa (haga clic en la visualización de frecuencia) en un slice bloqueado, la entrada se cancela automáticamente y se muestra la superposición `LOCKED`. |
| Botón de bloquear/desbloquear | El botón de bloquear/desbloquear se actualiza inmediatamente cuando cambia el estado de bloqueo del slice. Desbloquear elimina la superposición `LOCKED`. |

## Corrección de altura de pestaña del panel VFO en v26.5.3

En v26.5.3, el contenido de la pestaña del panel VFO ahora utiliza un widget apilado personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un problema de diseño donde el área de contenido de la pestaña podría asignar demasiada altura al cambiar entre pestañas de diferentes alturas (por ejemplo, al cambiar de la pestaña DSP, que muestra controles adicionales para modos DIGU/DIGL, a la pestaña Mode). El área de contenido de la pestaña ahora se ajusta correctamente al contenido de cada pestaña sin dejar espacios.

## Comportamiento de desplazamiento en v26.5.3

En v26.5.3, el comportamiento de desplazamiento con la rueda del ratón se ha actualizado:

| Cambio | Descripción |
|---|---|
| Manejo de slice bloqueado | Al desplazarse sobre un slice bloqueado en modo contraído, la solicitud de sintonía ahora se bloquea con una notificación visual `LOCKED` en lugar de ignorarse silenciosamente. |
| Modo contraído consistente | El comportamiento de desplazamiento para sintonizar en modo contraído ahora usa la misma verificación de bloqueo que el modo expandido, asegurando
