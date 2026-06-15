# Configuración de la Radio

El cuadro de diálogo Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona acceso a la información de la radio, ajustes de red, GPS, configuración de TX, ajustes de Phone/CW, calibración de RX, configuración de audio, nombres de antenas, opciones de filtro, definiciones de transverter, asignaciones de cable USB, conexiones periféricas, muestreo APD, apariencia del tema y configuración del puerto serie FlexControl.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Muchos campos se completan con datos en vivo de la radio.
- El cuadro de diálogo recuerda su tamaño y posición entre sesiones. Si el cuadro de diálogo aparece fuera de la pantalla, elimine la entrada `RadioSetupDialogGeometry` de su archivo de configuración.

## Abrir Configuración de la Radio

1. Haga clic en `Settings > Radio Setup...`.
2. El cuadro de diálogo se abre en la última posición y tamaño utilizados.

# Pestaña Radio

La pestaña Radio muestra la información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Utilice esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte técnico.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El cuadro de diálogo se abre por defecto en la pestaña **Radio**.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (se muestra `USA` por defecto si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Número de serie del chasis (solo lectura). | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976). |
| HW Version | Cadena de versión de hardware. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Muestra las opciones de radio licenciadas. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| Remote On | Botón pulsador | Habilita el encendido remoto / remote-on. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de habililitación de multiFLEX. |
| Model | Modelo de radio. | Incluye un botón de copia al portapapeles junto al valor (#2976). |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica a este cliente de AetherSDR para otras estaciones multiFLEX. Por defecto, usa el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. |
| License Info | Indicador | Muestra los detalles de licencia de la radio (Suscripción / Vencimiento / ID de radio / Versión licenciada). |
| Check for Update | Botón pulsador | Consulta si hay actualizaciones de firmware disponibles. |
| Upload Firmware | Botón pulsador | Inicia la carga de firmware con barra de progreso y estado. |
| SmartLink (pestaña) | Gestión de certificados TLS SmartLink fijados. Lista cada certificado fijado (host, huella SHA-256, fecha de fijación) con botones por fila Forget y Forget All. Nuevo en v26.5.3 (#2951 Fase 2). | Se construye perezosamente al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de certificado fijado ahora pausa firmemente el handshake con un cuadro de diálogo modal. |
| Pinned SmartLink Certificates (sección) | Encabezado de sección para la tabla de certificados fijados dentro de la pestaña SmartLink. Lista cada host que este cliente ha fijado en la primera conexión (trust-on-first-use). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de fijación migró de cadenas simples a objetos {fp, pinnedAt}. |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (YYYY-MM-DD o '(pre-phase 2)'). | Respaldado por WanCertCache en WanConnection.cpp. |
| Forget selected | Elimina la huella del certificado fijado del host seleccionado, de modo que la próxima conexión lo vuelva a fijar silenciosamente. | |
| Forget all | Limpia todos los certificados fijados (con confirmación). La próxima conexión a cada radio los vuelve a fijar silenciosamente. | Muestra QMessageBox::question antes de borrar. |
| Select Installer... | Abre un cuadro de diálogo para seleccionar un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| Reboot Radio | Botón pulsador | Reinicia la radio conectada. Deshabilitado cuando la radio está desconectada. Muestra un cuadro de diálogo de confirmación antes de reiniciar. Las sesiones LAN se reconectan automáticamente; las sesiones WAN/SmartLink requieren reconexión manual. Nuevo en v26.6.3. |

Todos los campos de Información de la Radio son de solo lectura. No hay claves de configuración persistentes asociadas a ellos.

## Reinicio de la radio

El botón **Reboot Radio** se encuentra en el grupo de Información de la Radio. Solo está habilitado mientras AetherSDR está conectado a la radio.

1. Haga clic en **Reboot Radio**.
2. Aparece un cuadro de diálogo de confirmación:
   - En conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente cuando la radio termine de iniciar."
   - En conexiones WAN/SmartLink: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente cuando la radio termine de iniciar."
3. Haga clic en **OK** para confirmar. El cuadro de diálogo se cierra automáticamente después de la confirmación.
4. La radio se reinicia. AetherSDR se desconecta y reconecta automáticamente en LAN, o espera la reconexión manual en WAN.

## Copia de información de la radio

Cada valor en el grupo de Información de la Radio tiene un pequeño botón de copia a su derecha. Haga clic en el botón de copia para copiar el valor al portapapeles.

| Destino de copia | Qué se copia |
|---|---|
| Radio SN | La cadena del número de serie del chasis. |
| HW Version | La cadena de versión de hardware (con prefijo `v`). |
| Region | La cadena de la región regulatoria. |
| Options | La cadena de opciones licenciadas. |
| Remote On | El texto de la etiqueta "Remote On". |
| FlexControl | La cadena del estado de FlexControl. |
| multiFLEX | La cadena del estado de multiFLEX. |
| Model | La cadena del modelo de radio. |
| Nickname | El texto del apodo. |
| Callsign | El texto del indicativo. |
| Station Name | El texto del nombre de la estación. |
| License Info | La cadena completa de detalles de licencia. |
| Check for Update | El texto de la etiqueta "Check for Update". |
| Browse .ssdr... | La ruta del archivo después de navegar. |
| Upload Firmware | El texto de la etiqueta "Upload Firmware". |

El botón de copia aparece como un icono de documento pequeño. Solo se puede hacer clic cuando el valor asociado no está vacío y no es un marcador de posición de guión. Al hacer clic, el valor se copia al portapapeles del sistema y aparece un breve mensaje emergente "¡Copiado!" cerca del botón.

# Pestaña Red

La pestaña Red muestra la información de red de la radio y opciones avanzadas de red.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. |
| Enforce Private IP Connections: | Botón de alternancia (Habilitado/Deshabilitado) | Rechaza pares que no sean RFC1918. Muestra "Enabled" cuando está marcado. |
| Network MTU: | Spinbox | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se almacena en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| GPS | Pestaña | Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites. |

# Pestaña TX

La pestaña TX muestra temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y un acceso directo a la configuración de banda TX.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el cuadro de diálogo dedicado de potencia/sintonía por banda. |
| Timings (en ms / Timeout (sec)) | Spinbox / Campo de texto | Temporizaciones de retención/retardo de TX. El campo **Timeout** se muestra en segundos; la radio almacena el valor en milisegundos (FlexLib interno). |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y Accessory. |
| Max Power: | Spinbox | Establece el límite máximo de potencia de TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante una operación de Split. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |

### Temporizaciones de TX

Los campos de temporización controlan cuánto tiempo mantiene la radio los estados de activación:

| Campo | Unidad de visualización | Unidad de almacenamiento en la radio | Comportamiento |
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

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iámbico en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. |
| Swap: | Botón de alternancia | Intercambia punto/raya. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB | USB). |
| CWX: | Botón de alternancia | Habilita la activación de macros CWX. |
| Decode: | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. |
| RTTY Mark Default: | Spinbox | Frecuencia predeterminada de marca RTTY. |

# Pestaña RX

La pestaña RX muestra la calibración del offset de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.

## Función de cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb): | Spinbox | Offset de frecuencia manual en ppb. |
| 10 MHz Reference Source: | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto a la selección. |

## Calibración de frecuencia

Los controles de calibración siempre están visibles, independientemente de si hay un GPSDO instalado. El banner de estado en la parte superior del grupo muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido del PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Spinbox | Offset de frecuencia manual en partes por mil millones, aplicado después de que la calibración se completa o se establece directamente para la corrección manual
