# Panel VFO

El Panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes más usados por slice — modo, preajustes de filtro, selección de antena, ganancia AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Se colapsa a una tira compacta de solo frecuencia.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO para el slice deseado debe estar abierto. Si no lo está, haga clic en la bandera del marcador VFO en la pantalla del espectro para ese slice.
- Si el panel VFO está colapsado a la tira de solo frecuencia, haga clic en él una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera del marcador VFO en la pantalla del espectro para el slice que desea configurar.
2. Haga clic en cualquier pestaña dentro del panel VFO para acceder a los controles de esa pestaña.
3. Ajuste los controles según sea necesario. Los cambios surten efecto de inmediato.

## Función de cada control

| Control | Valor predeterminado | Rango válido |
|---------|---------------------|--------------|
| Botón de antena RX | Predeterminado de la radio | Lista de antenas de la radio |
| Botón de antena TX | Predeterminado de la radio | Lista de antenas de la radio (puertos solo RX excluidos) |
| Visualización de frecuencia | Frecuencia actual del slice | 0.001–50000 MHz |
| Etiqueta de ancho de filtro | Ancho de banda actual del filtro | Preajustes de filtro por modo |
| Deslizador de ganancia AF (pestaña Audio) | 100 | 0–100 |
| Deslizador de paneo (pestaña Audio) | 50 | 0–100 |
| Botón de silencio (pestaña Audio) | Apagado | Encendido / Apagado |
| Botón de squelch (pestaña Audio) | Apagado | Encendido / Apagado |
| Deslizador de squelch (pestaña Audio) | — | 0–100 |
| Combinación AGC (pestaña Audio) | RÁPIDO | RÁPIDO / MED / LENTO / APAGADO |
| Combinación de modo (pestaña Modo) | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY |
| Botones de preajuste de filtro (pestaña Modo) | — | Por preajuste guardado |
| Botones RIT / XIT (pestaña X/RIT) | Apagado | Encendido / Apagado |
| Combinación de canal DAX (pestaña DAX) | Apagado | Apagado / 1–8 |
| Botón de grosor de marcador | 1 px | Apagado / 1 px / 3 px |
| Botón de bordes de filtro | Mostrado | Encendido / Apagado |
| Alternancia de colapso | Expandido | Encendido / Apagado |
| Botón ADSP (pestaña DSP) | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú de Configuración. | Con estilo de alternancia DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo de configuración de AetherDSP no modal. |
| Botón AetherVoice (pestaña DSP) | Alterna la Tira de Canal de Audio Aetherial — el conjunto DSP unificado TX/RX. | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botones NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF (pestaña DSP) | Apagado | Encendido / Apagado. Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de configuración de AetherDSP para ese algoritmo. |

Ni el estado del botón ni la posición del deslizador se conservan como clave de AppSettings de AetherSDR — ambos reflejan el estado en vivo de la radio.

## Consejos

- Ajuste el deslizador de squelch justo por encima del piso de ruido para evitar que el audio se corte en señales débiles.
- El umbral de squelch interactúa con el ajuste de AGC. Si cambia el modo AGC usando el **combinación AGC**, es posible que deba reajustar el deslizador de squelch.

## Cambios en la pestaña DSP en v0.9.8

La **pestaña DSP** del panel VFO recibió dos nuevos botones de inicio en v0.9.8:

| Nuevo botón | Comportamiento |
|---|---|
| Botón ADSP | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú de Configuración. Botón no seleccionable con estilo de alternancia DSP del lado de la radio. |
| Botón AetherVoice | Alterna la Tira de Canal de Audio Aetherial — el conjunto DSP unificado TX/RX. Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Botón no seleccionable. |

Ambos botones se colocan al final de la cuadrícula de botones DSP. ADSP ocupa 1 columna, y AetherVoice ocupa las 2 columnas adyacentes.

### Sincronización del nivel DSP al inicio

En v0.9.8, se mejoró la sincronización del deslizador de nivel DSP. Cuando los botones DSP del lado de la radio (NR, NB, ANF, NRL, NRS, NRF, ANFL) están habilitados en el perfil guardado de la radio, el deslizador de nivel DSP correspondiente ahora se empuja a la pila de nivel compartida al inicio. Anteriormente, el deslizador de nivel faltaba hasta que el usuario alternaba manualmente el botón DSP. Esto soluciona el problema #startup-slider.

### Deslizador de nivel DSP

Una fila de **deslizador de nivel DSP** compartida aparece debajo de la cuadrícula de botones DSP. El deslizador apunta al botón DSP con nivel que se encendió más recientemente. La etiqueta a la izquierda del deslizador muestra el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha.

La fila del deslizador siempre está presente en el diseño. Cuando ningún DSP con nivel está activo — o cuando solo RNN, ANFT o APF está encendido — la fila se atenúa y no responde a la interacción. Se vuelve completamente visible tan pronto como se habilita un botón DSP compatible.

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

El rango del deslizador es 0–100. El valor de nivel no se conserva como clave de AppSettings de AetherSDR — refleja el estado en vivo de la radio.

## Corrección de la etiqueta de ancho de filtro en v0.9.8

La **etiqueta de ancho de filtro** en el panel VFO ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desfase de 0.1 kHz que antes afectaba las lecturas del filtro en modo SSB y digital (problemas #794, #1225, #2197). La etiqueta ahora se mantiene sincronizada con la visualización del filtro del applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

A partir de v26.5.1, el squelch también se deshabilita cuando el slice está en modo RTTY. Este cambio aborda el problema #2504, donde el squelch bloqueaba las señales FSK débiles utilizadas por decodificadores externos a través de DAX. El botón y el deslizador de squelch se deshabilitan automáticamente cuando el modo RTTY está activo, coincidiendo con el comportamiento existente para modos digitales y CW.

Si el squelch estaba habilitado al cambiar al modo RTTY, AetherSDR guarda el estado del squelch y lo restaura cuando vuelve a un modo de voz o FM.

## Cambios en la selección de antena en v26.5.2.1

A partir de v26.5.2.1, los menús de selección de antena RX y TX en el panel VFO se han mejorado:

| Cambio | Descripción |
|---|---|
| Menú de antena RX | Ahora usa `rxAntennaList()` del slice cuando está disponible, recurriendo a la lista maestra de antenas de la radio. Cada elemento del menú almacena el nombre de la antena como dato, y el texto del elemento se genera mediante `antennaMenuLabel()` para un formato consistente. |
| Menú de antena TX | Usa el método `txAntennaOptions()` para construir la lista, que excluye automáticamente los puertos de antena solo RX. Las antenas con nombres que comienzan con "RX" se filtran. El ayudante `likelyTxAntennaFallbackToken()` determina qué antenas probablemente tienen capacidad TX cuando no hay una lista de antenas TX dedicada disponible. |
| Tooltip y sugerencia de estado | Cada elemento del menú ahora muestra el nombre de antena sin procesar como tooltip y sugerencia de estado, proporcionando visibilidad completa del nombre cuando la etiqueta formateada está truncada. |

### Lógica de filtrado de antena TX

El menú de antena TX utiliza la siguiente lógica para determinar qué antenas mostrar:

1. Si hay una lista de antenas TX dedicada disponible desde la radio, úsela directamente.
2. De lo contrario, filtre la lista maestra de antenas para excluir los puertos que comienzan con "RX".
3. El ayudante `likelyTxAntennaFallbackToken()` identifica antenas con capacidad TX verificando si comienzan con "ANT", "TX", o son iguales a "XVTR".

## Cambios en la entrada de frecuencia en v26.5.2.1

La lógica de entrada de frecuencia para bandas XVTR se ha actualizado en v26.5.2.1:

| Cambio | Descripción |
|---|---|
| Límite máximo de frecuencia | Aumentado de 450 MHz a 50000 MHz para soportar bandas de microondas. |
| Comodidad de banda de 3 dígitos | La inserción automática de decimal (ej., 1446 → 144.6) ahora solo se aplica cuando el slice está en una banda de 100–999 MHz. Para bandas de 23cm y superiores, un entero simple se interpreta como el valor completo en MHz (ej., 1296 significa 1296 MHz, no 129.6 MHz). |

### Reglas de entrada de frecuencia para bandas XVTR

Al ingresar frecuencias en bandas XVTR:

- **Banda de 100–999 MHz**: Ingrese un entero simple con al menos 4 dígitos para que el decimal se inserte automáticamente después del 3er dígito (ej., 144600 → 144.600, 14696 → 146.96).
- **1000 MHz y superior**: Ingrese el valor completo en MHz directamente (ej., 1296 para 23cm significa 1296.000 MHz).
- Siempre puede ingresar un punto decimal manualmente para evitar la inserción automática.

## Cambios en la entrada de frecuencia en v26.5.3

La lógica de entrada de frecuencia se ha actualizado para soportar la entrada explícita de MHz en bandas altas:

| Cambio | Descripción |
|---|---|
| Entrada explícita de MHz | Cuando se ingresa un valor de frecuencia superior a 54.0 con un punto decimal explícito (ej., "144.200"), ahora se trata como MHz y se acepta para cualquier banda, incluidas las bandas no XVTR. Anteriormente, ingresar "144.200" en una banda no XVTR sería rechazado por estar fuera de rango. |
| Análisis normalizado | El texto ahora se normaliza usando `FrequencyEntryParser::normalizedMhzText()` que maneja el formato "14.225.000" eliminando los puntos más allá del primero. |
| Validación de rango | El límite máximo de frecuencia de 50000 MHz se aplica a todas las bandas cuando se usa un punto decimal explícito, coincidiendo con el comportamiento existente para bandas XVTR. |

### Reglas de entrada de frecuencia en v26.5.3

Al ingresar frecuencias:

- **Entrada explícita de MHz**: Ingrese una frecuencia con un punto decimal (ej., "14.225", "144.200", "1296.000") para que se trate directamente como MHz. Los valores superiores a 54.0 MHz se aceptan cuando hay un punto decimal explícito presente.

- **Entrada de entero simple (bandas no XVTR, por debajo o igual a 54.0 MHz)**: Ingrese un entero simple para que se analice de la siguiente manera:
  - Valores por debajo de 54000: Se tratan como kHz (ej., 14225 = 14.225 MHz)
  - Valores por encima de 54000: Se tratan como Hz (ej., 14225000 = 14.225 MHz)

- **Entrada de entero simple (bandas XVTR, por encima de 54.0 MHz)**: Un entero simple se trata directamente como MHz, con la regla de comodidad de banda de 3 dígitos aplicada para bandas de 100–999 MHz.

## Comportamiento del slice bloqueado en v26.5.3

A partir de v26.5.3, cuando un slice está bloqueado, se aplican los siguientes comportamientos:

| Comportamiento | Descripción |
|---|---|
| Notificación de sintonía bloqueada | Cuando intenta desplazar la rueda del ratón sobre un slice bloqueado, se muestra una superposición visual `BLOQUEADO` en la visualización de frecuencia para indicar que la sintonía está bloqueada. |
| Cancelación de entrada directa | Si comienza la entrada directa de frecuencia (haga clic en la visualización de frecuencia) en un slice bloqueado, la entrada se cancela automáticamente y se muestra la superposición `BLOQUEADO`. |
| Botón de bloquear/desbloquear | El botón de bloquear/desbloquear se actualiza inmediatamente cuando cambia el estado de bloqueo del slice. Desbloquear elimina la superposición `BLOQUEADO`. |

## Corrección de altura de pestaña del panel VFO en v26.5.3

En v26.5.3, el contenido de la pestaña del panel VFO ahora usa un widget apilado personalizado que informa solo el tamaño preferido de la pestaña actual. Esto corrige un problema de diseño donde el área de contenido de la pestaña podía sobreasignar altura al cambiar entre pestañas de diferentes alturas (ej., al cambiar de la pestaña DSP, que muestra controles adicionales para modos DIGU/DIGL, a la pestaña Modo). El área de contenido de la pestaña ahora se ajusta correctamente al contenido de cada pestaña sin dejar espacios.

## Comportamiento de desplazamiento en v26.5.3

En v26.5.3, el comportamiento de desplazamiento con la rueda del ratón se ha actualizado:

| Cambio | Descripción |
|---|---|
| Manejo de slice bloqueado | Al desplazarse sobre un slice bloqueado en modo colapsado, la solicitud de sintonía ahora se bloquea con una notificación visual `BLOQUEADO` en lugar de ignorarse silenciosamente. |
| Modo colapsado consistente | El comportamiento de desplazamiento ahora es consistente entre los modos expandido y colapsado. |

## Cambios en v26.6.3

### Mejoras en la barra de pestañas

En v26.6.3, la barra de pestañas del panel VFO se reescrib
