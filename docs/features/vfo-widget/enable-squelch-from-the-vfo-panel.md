# Habilitar el squelch desde el panel VFO

El squelch silencia el audio de un slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para eliminar el ruido de fondo en modos FM, AM o digitales cuando no hay señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El panel VFO del slice objetivo debe estar abierto. Si no lo está, haga clic en la bandera marcadora VFO en la visualización del espectro de ese slice.
- Si el panel VFO está colapsado a la tira de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera marcadora VFO en la visualización del espectro del slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Haga clic en el **botón Squelch** para habilitar el squelch. El botón se activa y el squelch se aplica al slice de inmediato.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o derecha para establecer el umbral. El rango válido es 0–100.

Para deshabilitar el squelch, haga clic en el **botón Squelch** nuevamente.

## Qué hace cada control

| Control                        | Predeterminado                                                                                                                             | Rango válido                                                                                                              |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Botón antena RX                | Predeterminado del radio                                                                                                                  | Lista de antenas del radio                                                                                                |
| Botón antena TX                | Predeterminado del radio                                                                                                                  | Lista de antenas del radio (puertos solo RX excluidos)                                                                    |
| Visualización de frecuencia    | Frecuencia actual del slice                                                                                                               | 0.001–50000 MHz                                                                                                           |
| Etiqueta de ancho de filtro    | Ancho de banda de filtro actual                                                                                                           | Preajustes de filtro por modo                                                                                             |
| Deslizador AF Gain (pestaña Audio) | 100                                                                                                                                 | 0–100                                                                                                                     |
| Deslizador Pan (pestaña Audio) | 50                                                                                                                                      | 0–100                                                                                                                     |
| Botón Mute (pestaña Audio)     | Off                                                                                                                                     | On / Off                                                                                                                  |
| Botón Squelch (pestaña Audio)  | Off                                                                                                                                     | On / Off                                                                                                                  |
| Deslizador Squelch (pestaña Audio) | —                                                                                                                                     | 0–100                                                                                                                     |
| Combo AGC (pestaña Audio)      | FAST                                                                                                                                     | FAST / MED / SLOW / OFF                                                                                                   |
| Combo Mode (pestaña Mode)      | USB                                                                                                                                     | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY                                                     |
| Botones de preajuste de filtro (pestaña Mode) | —                                                                                                                                | Por preajuste guardado                                                                                                    |
| Botones RIT / XIT (pestaña X/RIT) | Off                                                                                                                                     | On / Off                                                                                                                  |
| Combo canal DAX (pestaña DAX)  | Off                                                                                                                                     | Off / 1–8                                                                                                                 |
| Botón de grosor del marcador   | 1 px                                                                                                                                   | Off / 1 px / 3 px                                                                                                         |
| Botón de bordes de filtro      | Mostrado                                                                                                                                | On / Off                                                                                                                  |
| Alternar colapso               | Expandido                                                                                                                               | On / Off                                                                                                                  |
| Botón ADSP (pestaña DSP)       | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Estilizado como un botón de DSP del lado del radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo AetherDSP Settings no modal. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canales de audio Aetherial: el conjunto unificado de DSP TX/RX (v0.9.8).                                             | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Ni el estado del botón ni la posición del deslizador se persisten como una clave de AppSettings de AetherSDR; ambos reflejan el estado en vivo del radio.

## Consejos

- Ajuste el deslizador justo por encima del piso de ruido para evitar que el audio se corte y se restablezca en señales débiles.
- El umbral de squelch interactúa con la configuración de AGC. Si cambia el modo AGC usando el **combo AGC**, es posible que necesite reajustar el deslizador de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel VFO recibió dos nuevos botones de lanzamiento en v0.9.8:

| Nuevo botón    | Comportamiento                                                                                                                                                      |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Botón ADSP     | Abre el diálogo AetherDSP Settings (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado cliente). Mismo punto de entrada que el menú Settings. Botón no seleccionable estilizado como un botón de DSP del lado del radio. |
| Botón AetherVoice | Alterna la tira de canales de audio Aetherial: el conjunto unificado de DSP TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no seleccionable.     |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna, y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del deslizador de nivel DSP. Cuando los botones DSP del lado del radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado del radio, el deslizador de nivel DSP correspondiente ahora se empuja a la pila de niveles compartida al inicio. Anteriormente, el deslizador de nivel faltaba hasta que el usuario alternaba manualmente el botón DSP. Esto corrige el problema #startup-slider.

### Deslizador de nivel DSP

Aparece una fila **deslizador de nivel DSP** compartida debajo de la cuadrícula de botones DSP. El deslizador apunta al botón DSP con nivel que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del deslizador siempre está presente en el diseño. Cuando no hay DSP con nivel activo, o cuando solo RNN, ANFT o APF están encendidos, la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se habilita un botón DSP compatible.

Objetivos DSP con nivel compatibles con el deslizador:

| Objetivo | Controlado por |
|---|---|
| NR | `setNrLevel` |
| NB | `setNbLevel` |
| ANF | `setAnfLevel` |
| NRL | `setNrlLevel` |
| NRS | `setNrsLevel` |
| NRF | `setNrfLevel` |
| ANFL | `setAnflLevel` |

El rango del deslizador es 0–100. El valor de nivel no se persiste como una clave de AppSettings de AetherSDR; refleja el estado en vivo del radio.

## Corrección de etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que anteriormente afectaba las lecturas de filtro en modo SSB y digitales (problemas #794, #1225, #2197). La etiqueta ahora permanece sincronizada con la visualización del filtro del applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se deshabilita cuando el slice está en modo RTTY. Este cambio aborda el problema #2504, donde el squelch estaba bloqueando señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el deslizador de squelch se deshabilitan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para modos digitales y CW.

Si el squelch estaba habilitado al cambiar al modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Cambios en la selección de antena en v26.5.2.1

A partir de v26.5.2.1, los menús de selección de antena RX y TX en el panel VFO se han mejorado:

| Cambio | Descripción |
|---|---|
| Menú de antena RX | Ahora usa `rxAntennaList()` del slice cuando está disponible, recurriendo a la lista maestra de antenas del radio. Cada elemento del menú almacena el nombre de la antena como datos, y el texto del elemento se genera mediante `antennaMenuLabel()` para un formato consistente. |
| Menú de antena TX | Usa el método `txAntennaOptions()` para construir la lista, que excluye automáticamente los puertos de antena solo RX. Las antenas con nombres que comienzan con "RX" se filtran. El ayudante `likelyTxAntennaFallbackToken()` determina qué antenas son probablemente capaces de TX cuando no hay disponible una lista de antenas TX dedicada. |
| Tooltip y status tip | Cada elemento del menú ahora muestra el nombre de la antena en bruto como tooltip y status tip, proporcionando visibilidad del nombre completo cuando la etiqueta formateada está truncada. |

### Lógica de filtrado de antena TX

El menú de antena TX utiliza la siguiente lógica para determinar qué antenas mostrar:

1. Si hay una lista de antenas TX dedicada disponible del radio, úsela directamente.
2. De lo contrario, filtre la lista maestra de antenas para excluir puertos que comiencen con "RX".
3. El ayudante `likelyTxAntennaFallbackToken()` identifica las antenas capaces de TX verificando si comienzan con "ANT", "TX", o son iguales a "XVTR".

## Cambios en la entrada de frecuencia en v26.5.2.1

La lógica de entrada de frecuencia para bandas XVTR se ha actualizado en v26.5.2.1:

| Cambio | Descripción |
|---|---|
| Límite máximo de frecuencia | Aumentado de 450 MHz a 50000 MHz para soportar bandas de microondas. |
| Comodidad de banda de 3 dígitos | La inserción automática de decimales (por ejemplo, 1446 → 144.6) ahora solo se aplica cuando el slice está en una banda de 100–999 MHz. Para bandas de 23 cm y superiores, un número entero se interpreta como el valor completo en MHz (por ejemplo, 1296 significa 1296 MHz, no 129.6 MHz). |

### Reglas de entrada de frecuencia para bandas XVTR

Al ingresar frecuencias en bandas XVTR:

- **Banda de 100–999 MHz**: Ingrese un número entero con al menos 4 dígitos para que el decimal se inserte automáticamente después del 3er dígito (por ejemplo, 144600 → 144.600, 14696 → 146.96).
- **1000 MHz y superior**: Ingrese el valor completo en MHz directamente (por ejemplo, 1296 para 23 cm significa 1296.000 MHz).
- Siempre puede ingresar un punto decimal manualmente para evitar la inserción automática.

## Relacionado

- [Ajustar ganancia AF y paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar audio para un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
