# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a la información de la radio, configuración de red, GPS, configuración de TX, ajustes de Phone/CW, calibración de RX, configuración de audio, nombres de antena, opciones de filtro, definiciones de transvertidores, asignaciones de cable USB, conexiones de periféricos, muestreo APD, apariencia del tema y configuración del puerto serie FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Muchos campos se completan con datos en vivo de la radio.
- El diálogo recuerda su tamaño y posición entre sesiones. Si el diálogo aparece fuera de la pantalla, elimine la entrada `RadioSetupDialogGeometry` de su archivo de configuración.

## Abrir Configuración de la Radio

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en su última posición y tamaño utilizados.

# Pestaña Radio

La pestaña Radio muestra información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte técnico.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (por defecto `USA` si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reportado por la radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. |
| Remote On | Botón pulsador | Activa el encendido remoto / remote-on. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Model | Indicador | Modelo de la radio. |
| Nickname | Campo de texto | Apodo de la radio fácil de usar. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre de host del sistema operativo si está vacío. Se almacena en AppSettings como `StationName`. |
| License Info | Indicador | Muestra los detalles de la licencia de la radio (Suscripción / Vencimiento / ID de Radio / Versión licenciada). |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Browse .ssdr... | Botón pulsador | Selecciona un archivo de imagen de firmware. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| SmartLink (pestaña) | Gestión de certificados TLS de SmartLink anclados. Enumera cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones Olvidar por fila y Olvidar todo. Nuevo en v26.5.3 (#2951 Fase 2). | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: una discrepancia de certificado ahora pausa el handshake de forma forzosa con un diálogo modal. |
| Pinned SmartLink Certificates (sección) | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Enumera cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}. |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)'). | Respaldado por WanCertCache en WanConnection.cpp. |
| Forget selected | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión vuelva a anclar en silencio. | |
| Forget all | Borra todos los certificados anclados (con confirmación). La próxima conexión a cada radio vuelve a anclar en silencio. | Muestra QMessageBox::question antes de borrar. |

Todos los campos de Radio Information son de solo lectura. No hay claves de configuración persistentes asociadas a ellos.

## Copiar información de la radio

Cada valor en el grupo Radio Information tiene un pequeño botón de copiar a su derecha. Haga clic en el botón de copiar para copiar el valor al portapapeles.

| Destino de copia | Qué se copia |
|---|---|
| Radio SN | La cadena del número de serie del chasis. |
| HW Version | La cadena de versión de hardware (con prefijo `v`). |
| Region | La cadena de región regulatoria. |
| Options | La cadena de opciones licenciadas. |
| Remote On | El texto de la etiqueta "Remote On". |
| FlexControl | La cadena de estado de FlexControl. |
| multiFLEX | La cadena de estado de multiFLEX. |
| Model | La cadena del modelo de la radio. |
| Nickname | El texto del apodo. |
| Callsign | El texto del indicativo. |
| Station Name | El texto del nombre de la estación. |
| License Info | La cadena completa de detalles de la licencia. |
| Check for Update | El texto de la etiqueta "Check for Update". |
| Browse .ssdr... | La ruta del archivo después de navegar. |
| Upload Firmware | El texto de la etiqueta "Upload Firmware". |

El botón de copiar aparece como un pequeño icono de documento. Solo se puede hacer clic cuando el valor asociado no está vacío y no es un marcador de posición de guión. Al hacer clic, el valor se copia al portapapeles del sistema y aparece un breve mensaje emergente "¡Copiado!" cerca del botón.

# Pestaña Red

La pestaña Red muestra información de red de la radio y opciones de red avanzadas.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| Network MTU: | Spinbox | Establece el tamaño máximo del paquete VITA-49 UDP de salida en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se almacena en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Aplica la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| GPS | Pestaña | Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites. |

# Pestaña TX

La pestaña TX muestra tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y acceso directo a Configuración de Banda TX.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (in ms / Timeout (sec)) | Spinbox / Campo de texto | Tiempos de retención/retardo de TX. El campo **Timeout** se muestra en segundos; la radio almacena el valor en milisegundos (interno de FlexLib). |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power: | Spinbox | Establece el límite máximo de potencia de TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Combo box | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |

### Tiempos de TX

Los campos de tiempo controlan cuánto tiempo la radio mantiene ciertos estados:

| Campo | Unidad mostrada | Unidad de almacenamiento en radio | Comportamiento |
|---|---|---|---|
| ACC TX: | ms | ms | Retardo de TX del accesorio. |
| TX Delay: | ms | ms | Retardo de activación de TX. |
| RCA TX1: | ms | ms | Retardo de RCA TX1. |
| Timeout: | segundos | ms | Tiempo de espera de enclavamiento. Se muestra en segundos enteros para facilitar la lectura; la radio espera y almacena milisegundos. |

# Pestaña Phone/CW

La pestaña Phone/CW muestra el micrófono, el manipulador CW y los valores predeterminados de RTTY.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Combo box | Selecciona la banda lateral del tono CW (LSB | USB). |
| CWX: | Botón de alternancia | Habilita la activación de macros CWX. |
| Decode: | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | Frecuencia de marca RTTY predeterminada. |

# Pestaña RX

La pestaña RX muestra la calibración del desvío de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | Desvío de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Combo box | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto a ella. |

## Calibración de frecuencia

Los controles de calibración siempre son visibles independientemente de si hay un GPSDO instalado. El banner de estado en la parte superior del grupo muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido del PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Spinbox | Desvío de frecuencia manual en partes por mil millones, aplicado después de que la calibración se completa o configurado directamente para corrección manual. |

Aparece una etiqueta de estado a la derecha del botón Start que se actualiza durante la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Gris-azul |
| En progreso | Se actualiza según el estado del PLL reportado por la radio | Gris-azul |

El botón Start se vuelve a habilitar y su etiqueta vuelve a **Start** cuando la secuencia de calibración se completa o falla.

## Fuente de referencia de 10 MHz

El combo box **10 MHz Reference Source:** y su etiqueta de estado de bloqueo adjunta se actualizaron para manejar una gama más amplia de estados del oscilador reportados por la radio.

**Población del combo box:** La lista de fuentes disponibles se construye dinámicamente cada vez que se abre la pestaña o cambia el estado del oscilador de la radio. Las fuentes aparecen en el combo solo si la radio reporta que el hardware relevante está presente, si la configuración actual o el estado activo usa esa fuente, o si se ha recibido el estado del oscilador (en cuyo caso TCXO y External 10 MHz siempre se incluyen como opciones).

| Valor de fuente | Etiqueta mostrada en el combo |
|---|---|
| `auto` | Auto |
| `tcxo` | TCXO |
| `gpsdo` | GPSDO |
| `external` / `ext` | External 10 MHz |

**Etiqueta de estado de bloqueo:** La etiqueta a la derecha del combo muestra información de estado más completa:

| Condición | Texto mostrado | Color |
|---|---|---|
| Aún no se ha recibido el estado del oscilador | "Waiting for oscillator status" | Gris-azul |
| Fuente bloqueada | `<source> Locked` | Verde (`#00c040`) |
| Fuente desbloqueada |
