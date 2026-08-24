# Panel VFO

El Panel VFO es un panel de control flotante por segmento (slice) anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por segmento más utilizados — modo, presets de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Se colapsa a una franja compacta de solo frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del segmento objetivo debe estar abierto. Si no lo está, haga clic en la bandera del marcador VFO en la pantalla del espectro para ese segmento.
- Si el panel VFO está colapsado a la franja de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera del marcador VFO en la pantalla del espectro para el segmento que desea configurar.
2. Haga clic en cualquier pestaña dentro del panel VFO para acceder a los controles de esa pestaña.
3. Ajuste los controles según sea necesario. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---------|----------------------|--------------|
| Botón de antena RX | Predeterminado de la radio | Lista de antenas de la radio |
| Botón de antena TX | Predeterminado de la radio | Lista de antenas de la radio (puertos solo RX excluidos) |
| Visualización de frecuencia | Frecuencia actual del segmento | 0.001–50000 MHz |
| Etiqueta de ancho de filtro | Ancho de banda de filtro actual | Presets de filtro por modo |
| Deslizador de ganancia AF (pestaña Audio) | 100 | 0–100 |
| Deslizador de paneo (pestaña Audio) | 50 | 0–100 |
| Botón de silencio (pestaña Audio) | Desactivado | Activado / Desactivado |
| Botón de squelch (pestaña Audio) | Desactivado | Activado / Desactivado |
| Deslizador de squelch (pestaña Audio) | — | 0–100 |
| Combo AGC (pestaña Audio) | FAST | FAST / MED / SLOW / OFF |
| Combo de modo (pestaña Mode) | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY |
| Botones de preset de filtro (pestaña Mode) | — | Por preset guardado |
| Botones RIT / XIT (pestaña X/RIT) | Desactivado | Activado / Desactivado |
| Combo de canal DAX (pestaña DAX) | Desactivado | Desactivado / 1–8 |
| Botón de grosor del marcador | 1 px | Desactivado / 1 px / 3 px |
| Botón de bordes de filtro | Mostrado | Activado / Desactivado |
| Alternancia de colapso | Expandido | Activado / Desactivado |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. | Con estilo similar a un conmutador DSP del lado de la radio pero no marcable. Al hacer clic, eleva y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Alterna la tira de canal de audio Aetherial — la suite DSP unificada de TX/RX. | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú / cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Desactivado | Activado / Desactivado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |

Ni el estado del botón ni la posición del deslizador se conservan como clave AppSettings de AetherSDR — ambos reflejan el estado en vivo de la radio.

## Consejos

- Ajuste el deslizador de squelch justo por encima del piso de ruido para evitar que el audio se corte en señales débiles.
- El umbral de squelch interactúa con el ajuste de AGC. Si cambia el modo AGC usando el **combo AGC**, es posible que deba reajustar el deslizador de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel VFO recibió dos nuevos botones de lanzamiento en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings. Botón no marcable con estilo similar a un conmutador DSP del lado de la radio. |
| Botón AetherVoice | Alterna la tira de canal de audio Aetherial — la suite DSP unificada de TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no marcable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna, y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del deslizador de nivel DSP. Cuando los botones DSP del lado de la radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado de la radio, el deslizador de nivel DSP correspondiente ahora se inserta en la pila de nivel compartida al inicio. Anteriormente, el deslizador de nivel faltaba hasta que el usuario alternaba manualmente el botón DSP. Esto corrige el problema #startup-slider.

### Deslizador de nivel DSP

Una fila compartida de **deslizador de nivel DSP** aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al botón DSP con nivel que se activó más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del deslizador siempre está presente en el diseño. Cuando ningún DSP con nivel está activo — o cuando solo RNN, ANFT o APF están activados — la fila se atenúa y no responde a la interacción. Se vuelve completamente visible nuevamente tan pronto como se habilita un botón DSP compatible.

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

El rango del deslizador es 0–100. El valor de nivel no se conserva como clave AppSettings de AetherSDR — refleja el estado en vivo de la radio.

## Corrección de la etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desfase de 0.1 kHz que anteriormente afectaba las lecturas de filtro en modos SSB y digitales (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la visualización de filtro del applet RX.

## Comportamiento de squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se desactiva cuando el segmento está en modo RTTY. Este cambio aborda el problema #2504, donde el squelch bloqueaba señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el deslizador de squelch se desactivan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para modos digitales y CW.

Si el squelch estaba habilitado al cambiar a modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Cambios en la selección de antena en v26.5.2.1

A partir de v26.5.2.1, los menús de selección de antena RX y TX en el panel VFO se han mejorado:

| Cambio | Descripción |
|---|---|
| Menú de antena RX | Ahora usa `rxAntennaList()` del segmento cuando está disponible, recurriendo a la lista maestra de antenas de la radio. Cada elemento del menú almacena el nombre de la antena como dato, y el texto del elemento se genera con `antennaMenuLabel()` para un formato consistente. |
| Menú de antena TX | Usa el método `txAntennaOptions()` para construir la lista, que excluye automáticamente los puertos de antena solo RX. Las antenas con nombres que comienzan con "RX" se filtran. El auxiliar `likelyTxAntennaFallbackToken()` determina qué antenas son probablemente capaces de TX cuando no hay una lista dedicada de antenas TX disponible. |
| Tooltip y status tip | Cada elemento del menú ahora muestra el nombre crudo de la antena como tooltip y status tip, proporcionando visibilidad completa del nombre cuando la etiqueta formateada se trunca. |

### Lógica de filtrado de antenas TX

El menú de antenas TX usa la siguiente lógica para determinar qué antenas mostrar:

1. Si hay una lista dedicada de antenas TX disponible desde la radio, úsela directamente.
2. De lo contrario, filtre la lista maestra de antenas para excluir puertos que comiencen con "RX".
3. El auxiliar `likelyTxAntennaFallbackToken()` identifica antenas capaces de TX verificando si comienzan con "ANT", "TX" o son iguales a "XVTR".

## Cambios en la entrada de frecuencia en v26.5.2.1

La lógica de entrada de frecuencia para bandas XVTR se ha actualizado en v26.5.2.1:

| Cambio | Descripción |
|---|---|
| Límite máximo de frecuencia | Aumentado de 450 MHz a 50000 MHz para soportar bandas de microondas. |
| Conveniencia de banda de 3 dígitos | La inserción automática de decimales (por ejemplo, 1446 → 144.6) ahora solo se aplica cuando el segmento está en una banda de 100–999 MHz. Para bandas de 23 cm y superiores, un entero simple se interpreta como el valor completo en MHz (por ejemplo, 1296 significa 1296 MHz, no 129.6 MHz). |

### Reglas de entrada de frecuencia para bandas XVTR

Al ingresar frecuencias en bandas XVTR:

- **Banda de 100–999 MHz**: Ingrese un entero simple con al menos 4 dígitos para que el decimal se inserte automáticamente después del 3er dígito (por ejemplo, 144600 → 144.600, 14696 → 146.96).
- **1000 MHz y superiores**: Ingrese el valor completo en MHz directamente (por ejemplo, 1296 para 23 cm significa 1296.000 MHz).
- Siempre puede ingresar un punto decimal manualmente para omitir la inserción automática.

## Cambios en la entrada de frecuencia en v26.5.3

La lógica de entrada de frecuencia se ha actualizado para soportar entrada explícita en MHz en bandas altas:

| Cambio | Descripción |
|---|---|
| Entrada explícita en MHz | Cuando se ingresa un valor de frecuencia mayor que 54.0 con un punto decimal explícito (por ejemplo, "144.200"), ahora se trata como MHz y se acepta para cualquier banda, incluidas bandas no XVTR. Anteriormente, ingresar "144.200" en una banda no XVTR se rechazaba por estar fuera de rango. |
| Análisis normalizado | El texto ahora se normaliza usando `FrequencyEntryParser::normalizedMhzText()` que maneja el formato "14.225.000" eliminando puntos más allá del primero. |
| Validación de rango | El límite máximo de frecuencia de 50000 MHz se aplica a todas las bandas cuando se usa un punto decimal explícito, coincidiendo con el comportamiento existente para bandas XVTR. |

### Reglas de entrada de frecuencia en v26.5.3

Al ingresar frecuencias:

- **Entrada explícita en MHz**: Ingrese una frecuencia con punto decimal (por ejemplo, "14.225", "144.200", "1296.000") para que se trate directamente como MHz. Los valores superiores a 54.0 MHz se aceptan cuando hay un punto decimal explícito presente.

- **Entrada de entero simple (bandas no XVTR, menores o iguales a 54.0 MHz)**: Ingrese un entero simple para que se analice de la siguiente manera:
  - Valores inferiores a 54000: Se tratan como kHz (por ejemplo, 14225 = 14.225 MHz)
  - Valores superiores a 54000: Se tratan como Hz (por ejemplo, 14225000 = 14.225 MHz)

- **Entrada de entero simple (bandas XVTR, superiores a 54.0 MHz)**: Un entero simple se trata directamente como MHz, con la regla de conveniencia de banda de 3 dígitos aplicada para bandas de 100–999 MHz.

## Comportamiento de segmento bloqueado en v26.5.3

A partir de v26.5.3, cuando un segmento está bloqueado, se aplican los siguientes comportamientos:

| Comportamiento | Descripción |
|---|---|
| Notificación de sintonización bloqueada | Cuando intenta desplazar la rueda del ratón sobre un segmento bloqueado, se muestra una superposición visual `LOCKED` en la visualización de frecuencia para indicar que la sintonización está bloqueada. |
| Cancelación de entrada directa | Si comienza una entrada directa de frecuencia (hacer clic en la visualización de frecuencia) en un segmento bloqueado, la entrada se cancela automáticamente y se muestra la superposición `LOCKED`. |
| Botón de bloqueo/desbloqueo | El botón de bloqueo/desbloqueo se actualiza inmediatamente cuando cambia el estado de bloqueo del segmento. Desbloquear elimina la superposición `LOCKED`. |

## Corrección de altura de pestañas del panel VFO en v26.5.3

En v26.5.3, el contenido de las pestañas del panel VFO ahora usa un widget apilado personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un problema de diseño donde el área de contenido de la pestaña podía sobreasignar altura al cambiar entre pestañas de diferentes alturas (por ejemplo, cambiar de la pestaña DSP, que muestra controles adicionales para modos DIGU/DIGL, a la pestaña Mode). El área de contenido de la pestaña ahora se ajusta correctamente al contenido de cada pestaña sin dejar espacios.

## Comportamiento de desplazamiento en v26.5.3

En v26.5.3, el comportamiento de desplazamiento de la rueda del ratón se ha actualizado:

| Cambio | Descripción |
|---|---|
| Manejo de segmento bloqueado | Al desplazarse sobre un segmento bloqueado en modo colapsado, la solicitud de sintonización ahora se bloquea con una notificación visual `LOCKED` en lugar de ignorarse silenciosamente. |
| Modo colapsado consistente | El comportamiento de desplazamiento ahora es consistente entre modos expandido y colapsado. |

## Cambios en v26.6.3

### Mejoras en la barra de pestañas

En v26.6.3, la barra de pestañas del panel VFO se reescribió para usar `QPushButton` en lugar de `QLabel` para las etiquetas de
