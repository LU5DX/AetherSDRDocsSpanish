# Configuración de Radio

El diálogo Configuración de Radio es la ventana maestra de configuración por radio. Proporciona acceso a información de la radio, ajustes de red, GPS, configuración de TX, ajustes de Phone/CW, calibración de RX, configuración de audio, nombres de antenas, opciones de filtro, definiciones de transverter, asignaciones de cable USB, conexiones periféricas, muestreo APD, apariencia del tema, integración con KiwiSDR, búsqueda de indicativos y configuración del puerto serie FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Muchos campos se rellenan con datos en vivo de la radio.
- El diálogo recuerda su tamaño y posición entre sesiones. Si el diálogo aparece fuera de pantalla, elimine la entrada `RadioSetupDialogGeometry` de su archivo de configuración.

## Abrir Configuración de Radio

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en su última posición y tamaño utilizados.

# Pestaña Radio

La pestaña Radio muestra información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar soporte.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN**: el número de serie del chasis.
   - **HW Version**: la cadena de versión de hardware reportada por la radio.
   - **Region**: la región regulatoria de la radio (usa `USA` por defecto si la radio no reporta una).
   - **Options**: las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis. Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware. Incluye un botón de copiar al portapapeles junto al valor. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. Incluye un botón de copiar al portapapeles junto al valor. |
| Remote On | Botón pulsador | Habilita el encendido remoto / activación remota. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado habilitado de multiFLEX. |
| Model | Indicador (solo lectura) | Modelo de la radio. Incluye un botón de copiar al portapapeles junto al valor. |
| Nickname | Campo de texto | Apodo amigable de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del sistema operativo si está vacío. Se guarda en AppSettings como `StationName`. |
| License Info | Indicador | Muestra detalles de licencia de la radio (Suscripción, Expiración, ID de Radio, Versión licenciada). Cada campo incluye un botón de copiar al portapapeles. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware. |
| Select Installer... | Botón pulsador | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae el contenido .ssdr y emite el progreso. |
| Upload Firmware | Botón pulsador | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | Botón pulsador | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque termina. Solo está habilitado cuando hay conexión y el backend soporta un reinicio de cliente (p. ej., HL2 es solo RX, así que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. Nuevo en v26.8.4 (#4448). |
| Agent Automation (MCP): | Habilita el puente de automatización en la aplicación para que un asistente de codificación con IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por habilitarlo. | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Pantalla de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se guarda en el almacén secreto del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(loading…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzar activación) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Hace el puente de solo observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede evadirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones sin interfaz/CI. |
| VITA-49 RX buffer: | Control deslizante de ajuste a presets que configura el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; uno más grande absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. | Nuevo en v26.8.4 (#3810). Presets de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: <tamaño>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de buffer que el kernel realmente concedió (vs. el preset solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

Todos los campos de Radio Information son de solo lectura. No se asocian claves de configuración persistidas con ellos.

## Reiniciar la radio

El botón **Reboot Radio** se encuentra en el grupo Radio Information.

1. Haga clic en **Reboot Radio**.
2. Aparece un diálogo de confirmación:
   - En conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente cuando la radio termine de arrancar."
   - En conexiones WAN/SmartLink: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente cuando la radio termine de arrancar."
4. Haga clic en **OK** para confirmar. El diálogo se cierra automáticamente después de confirmar.
5. La radio se reinicia. AetherSDR se desconecta y se reconecta automáticamente en LAN, o espera reconexión manual en WAN.

## Copiar información de la radio

Cada valor en el grupo Radio Information tiene un pequeño botón de copiar a su derecha. Haga clic en el botón de copiar para copiar el valor al portapapeles.

| Destino de copia | Qué se copia |
|---|---|
| Radio SN | La cadena del número de serie del chasis. |
| HW Version | La cadena de versión de hardware (con prefijo `v`). |
| Region | La cadena de la región regulatoria. |
| Options | La cadena de opciones licenciadas. |
| Remote On | El texto de la etiqueta "Remote On". |
| FlexControl | La cadena de estado de FlexControl. |
| multiFLEX | La cadena de estado de multiFLEX. |
| Model | La cadena del modelo de la radio. |
| Nickname | El texto del apodo. |
| Callsign | El texto del indicativo. |
| Station Name | El texto del nombre de estación. |
| License Info | La cadena completa de detalles de licencia. |
| Check for Update | El texto de la etiqueta "Check for Update". |
| Select Installer... | El texto de la ruta de archivo después de navegar. |
| Upload Firmware | El texto de la etiqueta "Upload Firmware". |

El botón de copiar aparece como un ícono pequeño de documento. Solo se puede hacer clic cuando el valor asociado no está vacío y no es un marcador de posición con guión. Al hacer clic, el valor se copia al portapapeles del sistema y aparece un breve aviso "¡Copiado!" cerca del botón.

# Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador (solo lectura) | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |
| Enforce Private IP Connections: | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| Network MTU: | Cuadro de giro | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576-9000 bytes, valor predeterminado 1450. Se guarda en AppSettings como `NetworkMtu`. |
| DHCP / Static | Botón de alternancia | Cambia entre modos DHCP e IP estática. |
| IP Address: / Mask: / Gateway: | Campo de texto | Campos de configuración de IP estática. |
| Apply | Botón pulsador | Envía la configuración de red a la radio. |

# Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **GPS**.

No hay claves de configuración ni controles adicionales más allá de lo que se muestra en la pestaña.

# Pestaña TX

La pestaña TX muestra tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y acceso directo a TX Band Settings.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| TX Band Settings | Botón pulsador | Abre el diálogo dedicado de potencia/sintonía por banda. |
| Timings (en ms) | Cuadro de giro | Tiempos de retención/retardo de TX. |
| Interlocks - TX REQ: RCA / Accessory | Botón de alternancia | Habilita las entradas de enclavamiento RCA y de accesorio. |
| Max Power: | Cuadro de giro | Establece el límite de potencia TX a nivel de radio. Rango 0-100 %. |
| Tune Mode: | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall: | Botón de alternancia | Dibuja la señal TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. Se guarda en AppSettings como `TxFollowsActiveSlice`. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. Se guarda en AppSettings como `ActiveFollowsTxSlice`. |

### Tiempos de TX

| Campo | Unidad de visualización | Unidad de almacenamiento en radio | Comportamiento |
|---|---|---|---|
| ACC TX: | ms | ms | Retardo de TX de accesorio. |
| TX Delay: | ms | ms | Retardo de activación de TX. |
| RCA TX1: | ms | ms | Retardo de RCA TX1. |
| Timeout: | segundos | ms | Tiempo de espera de enclavamiento. Se muestra en segundos completos para legibilidad; la radio espera y almacena milisegundos. |

# Pestaña Phone/CW

La pestaña Phone/CW muestra valores predeterminados de micrófono, manipulador CW y RTTY.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Enable/Disable the Level Meter During Receive | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic: | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | Botón pulsador | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente exclusivo. |
| Swap: | Botón de alternancia | Intercambia dit/dah. |
| Sideband: | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB \| USB). |
| CWX: | Botón de alternancia | Habilita la activación de macros CWX. |
| Decode: RX | Botón de alternancia | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Se guarda en AppSettings como `CwDecoder` (JSON anidado, campo rx). Nuevo en v26.5.3: se dividió del interruptor único CwDecodeOverlay en interruptores independientes RX/TX. |
| Decode: TX | Botón de alternancia | Decodifica la propia clave CW del operador mediante tono lateral del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Se guarda en AppSettings como
