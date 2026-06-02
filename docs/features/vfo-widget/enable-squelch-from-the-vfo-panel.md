# Habilitar el squelch desde el panel del VFO

El squelch silencia el audio de una slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para silenciar el ruido de fondo en FM, AM o modos digitales cuando no haya señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El panel del VFO para la slice de destino debe estar abierto. Si no lo está, haga clic en la bandera marcadora del VFO en la pantalla del espectro para esa slice.
- Si el panel del VFO está colapsado a la tira de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel del VFO haciendo clic en la bandera marcadora del VFO en la pantalla del espectro para la slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel del VFO.
3. Haga clic en el **botón Squelch** para habilitar el squelch. El botón se activa y el squelch se aplica a la slice de inmediato.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o derecha para establecer el umbral. El rango válido es 0–100.

Para deshabilitar el squelch, haga clic nuevamente en el **botón Squelch**.

## Qué hace cada control

| Control                          | Valor predeterminado                                                                                                                 | Rango válido                                                                                                             |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Botón de antena RX               | Predeterminado del radio                                                                                                             | Lista de antenas del radio                                                                                               |
| Botón de antena TX               | Predeterminado del radio                                                                                                             | Lista de antenas del radio (puertos solo RX excluidos)                                                                   |
| Pantalla de frecuencia           | Frecuencia actual de la slice                                                                                                        | 0,001–50000 MHz                                                                                                          |
| Etiqueta de ancho de filtro      | Ancho de banda del filtro actual                                                                                                     | Preajustes de filtro por modo                                                                                            |
| Control deslizante de AF Gain (pestaña Audio) | 100                                                                                                                            | 0–100                                                                                                                    |
| Control deslizante de Pan (pestaña Audio)     | 50                                                                                                                             | 0–100                                                                                                                    |
| Botón Mute (pestaña Audio)       | Desactivado                                                                                                                          | Activado / Desactivado                                                                                                   |
| Botón Squelch (pestaña Audio)    | Desactivado                                                                                                                          | Activado / Desactivado                                                                                                   |
| Control deslizante de Squelch (pestaña Audio) | —                                                                                                                            | 0–100                                                                                                                    |
| Combinación AGC (pestaña Audio)  | FAST                                                                                                                                 | FAST / MED / SLOW / OFF                                                                                                  |
| Combinación Mode (pestaña Mode)  | USB                                                                                                                                  | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY                                                    |
| Botones de preajuste de filtro (pestaña Mode) | —                                                                                                                             | Por preajuste guardado                                                                                                   |
| Botones RIT / XIT (pestaña X/RIT) | Desactivado                                                                                                                          | Activado / Desactivado                                                                                                   |
| Combinación de canal DAX (pestaña DAX) | Desactivado                                                                                                                    | Desactivado / 1–8                                                                                                        |
| Botón de grosor del marcador     | 1 px                                                                                                                                 | Desactivado / 1 px / 3 px                                                                                                |
| Botón de bordes del filtro       | Mostrado                                                                                                                             | Activado / Desactivado                                                                                                   |
| Alternancia de colapso            | Expandido                                                                                                                            | Activado / Desactivado                                                                                                   |
| Botón ADSP (pestaña DSP)         | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. | Estilizado como una alternancia de DSP del lado del radio pero no marcable. Al hacer clic, muestra y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP)  | Alterna la tira de canal de audio Aetherial — el conjunto unificado de DSP de TX/RX.                                             | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Desactivado | Activado / Desactivado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |

Ni el estado del botón ni la posición del control deslizante se conservan como una clave de AppSettings de AetherSDR; ambos reflejan el estado en vivo del radio.

## Consejos

- Ajuste el control deslizante justo por encima del piso de ruido para evitar que el audio se entrecorte en señales débiles.
- El umbral de squelch interactúa con la configuración de AGC. Si cambia el modo AGC usando la **combinación AGC**, es posible que necesite reajustar el control deslizante de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel del VFO recibió dos nuevos botones de lanzamiento en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Botón no marcable estilizado como una alternancia de DSP del lado del radio. |
| Botón AetherVoice | Alterna la tira de canal de audio Aetherial — el conjunto unificado de DSP de TX/RX. Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Botón no marcable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel del control deslizante DSP al inicio

En v0.9.8, se mejoró la sincronización del control deslizante de nivel DSP. Cuando los botones DSP del lado del radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado del radio, el control deslizante de nivel DSP correspondiente ahora se inserta en la pila de niveles compartida al inicio. Anteriormente, el control deslizante de nivel faltaba hasta que el usuario alternaba manualmente el botón DSP. Esto corrige el problema #startup-slider.

### Control deslizante de nivel DSP

Una fila de **control deslizante de nivel DSP** compartida aparece debajo de la cuadrícula de botones DSP. El control deslizante apunta al botón DSP con nivel que se haya activado más recientemente. La etiqueta a la izquierda del control deslizante muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del control deslizante siempre está presente en el diseño. Cuando ningún DSP con nivel está activo, o cuando solo RNN, ANFT o APF están activados, la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se habilita un botón DSP compatible.

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

El rango del control deslizante es 0–100. El valor de nivel no se conserva como una clave de AppSettings de AetherSDR; refleja el estado en vivo del radio.

## Corrección de la etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel del VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0,1 kHz que afectaba anteriormente las lecturas del filtro en modo SSB y digital (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la pantalla del filtro del applet de RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se deshabilita cuando la slice está configurada en modo RTTY. Este cambio aborda el problema #2504, donde el squelch estaba bloqueando señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el control deslizante de squelch se deshabilitan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para los modos digital y CW.

Si el squelch estaba habilitado al cambiar al modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Cambios en la selección de antena en v26.5.2.1

A partir de v26.5.2.1, los menús de selección de antena RX y TX en el panel del VFO se han mejorado:

| Cambio | Descripción |
|---|---|
| Menú de antena RX | Ahora usa `rxAntennaList()` de la slice cuando está disponible, recurriendo a la lista maestra de antenas del radio. Cada elemento del menú almacena el nombre de la antena como dato, y el texto del elemento se genera mediante `antennaMenuLabel()` para un formato consistente. |
| Menú de antena TX | Usa el método `txAntennaOptions()` para construir la lista, que excluye automáticamente los puertos de antena solo RX. Las antenas con nombres que comienzan con "RX" se filtran. El helper `likelyTxAntennaFallbackToken()` determina qué antenas son probablemente capaces de TX cuando no hay disponible una lista de antenas TX dedicada. |
| Tooltip y status tip | Cada elemento del menú ahora muestra el nombre bruto de la antena como tooltip y status tip, proporcionando visibilidad del nombre completo cuando la etiqueta formateada está truncada. |

### Lógica de filtrado de antena TX

El menú de antena TX usa la siguiente lógica para determinar qué antenas mostrar:

1. Si hay una lista de antenas TX dedicada disponible desde el radio, úsela directamente.
2. De lo contrario, filtre la lista maestra de antenas para excluir puertos que comiencen con "RX".
3. El helper `likelyTxAntennaFallbackToken()` identifica antenas capaces de TX verificando si comienzan con "ANT", "TX" o son iguales a "XVTR".

## Cambios en la entrada de frecuencia en v26.5.2.1

La lógica de entrada de frecuencia para bandas XVTR se ha actualizado en v26.5.2.1:

| Cambio | Descripción |
|---|---|
| Límite máximo de frecuencia | Aumentado de 450 MHz a 50000 MHz para soportar bandas de microondas. |
| Conveniencia de banda de 3 dígitos | La inserción automática del decimal (p. ej., 1446 → 144,6) ahora solo se aplica cuando la slice está en una banda de 100–999 MHz. Para bandas de 23cm y superiores, un entero simple se interpreta como el valor completo en MHz (p. ej., 1296 significa 1296 MHz, no 129,6 MHz). |

### Reglas de entrada de frecuencia para bandas XVTR

Al ingresar frecuencias en bandas XVTR:

- **Banda de 100–999 MHz**: Ingrese un entero simple con al menos 4 dígitos para que el decimal se inserte automáticamente después del 3er dígito (p. ej., 144600 → 144,600, 14696 → 146,96).
- **1000 MHz y superior**: Ingrese el valor completo en MHz directamente (p. ej., 1296 para 23cm significa 1296,000 MHz).
- Siempre puede ingresar un punto decimal manualmente para evitar la inserción automática.

## Cambios en la entrada de frecuencia en v26.5.3

La lógica de entrada de frecuencia se ha actualizado para soportar la entrada explícita en MHz en bandas altas:

| Cambio | Descripción |
|---|---|
| Entrada explícita en MHz | Cuando se ingresa un valor de frecuencia mayor a 54,0 con un punto decimal explícito (p. ej., "144.200"), ahora se trata como MHz y se acepta para cualquier banda, incluyendo bandas que no son XVTR. Anteriormente, ingresar "144.200" en una banda que no era XVTR sería rechazado por estar fuera de rango. |
| Análisis normalizado | El texto ahora se normaliza usando `FrequencyEntryParser::normalizedMhzText()` que maneja el formato "14.225.000" eliminando los puntos más allá del primero. |
| Validación de rango | El límite máximo de frecuencia de 50000 MHz se aplica a todas las bandas cuando se usa un punto decimal explícito, coincidiendo con el comportamiento existente para bandas XVTR. |

### Reglas de entrada de frecuencia en v26.5.3

Al ingresar frecuencias:

- **Entrada explícita en MHz**: Ingrese una frecuencia con un punto decimal (p. ej., "14.225", "144.200", "1296.000") para que se trate directamente como MHz. Los valores superiores a 54,0 MHz se aceptan cuando hay un punto decimal explícito.

- **Entrada de entero simple (bandas no XVTR, por debajo o igual a 54,0 MHz)**: Ingrese un entero simple para analizarlo de la siguiente manera:
  - Valores por debajo de 54000: Se tratan como kHz (p. ej., 14225 = 14,225 MHz)
  - Valores por encima de 54000: Se tratan como Hz (p. ej., 14225000 = 14,225 MHz)

- **Entrada de entero simple (bandas XVTR, por encima de 54,0 MHz)**: Un entero simple se trata directamente como MHz, con la regla de conveniencia de banda de 3 dígitos aplicada para bandas de 100–999 MHz.

## Comportamiento de slice bloqueada en v26.5.3

A partir de v26.5.3, cuando una slice está bloqueada, se aplican los siguientes comportamientos:

| Comportamiento | Descripción |
|---|---|
| Notificación de sintonía bloqueada | Cuando intenta desplazar la rueda del ratón sobre una slice bloqueada, se muestra una superposición visual `LOCKED` en la pantalla de frecuencia para indicar que la sintonía está bloqueada. |
| Cancelación de entrada directa | Si comienza la entrada de frecuencia directa (haga clic en la pantalla de frecuencia) en una slice bloqueada, la entrada se cancela automáticamente y se muestra la superposición `LOCKED`. |
| Botón de bloqueo/desbloqueo | El botón de bloqueo/desbloqueo se actualiza inmediatamente cuando cambia el estado de bloqueo de la slice. Desbloquear elimina la superposición `LOCKED`. |

## Corrección de altura de pestaña del panel VFO en v26.5.3

En v26.5.3, el contenido de la pestaña del panel VFO ahora usa un widget apilado personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un problema de diseño donde el área de contenido de la pestaña podía sobre-asignar altura al cambiar entre pestañas de diferentes alturas (p. ej., al cambiar de la pestaña DSP, que muestra controles adicionales para modos DIGU/DIGL, a la pestaña Mode). El área de contenido de la pestaña ahora se ajusta correctamente al contenido de cada pestaña sin dejar espacios.

## Comportamiento de desplazamiento en v26.5.3

En v26.5.3, el comportamiento de desplazamiento con la rueda del ratón se ha actualizado:

| Cambio | Descripción |
|---|---|
| Manejo
