# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información del radio, configuración de red, GPS, configuración de TX, Phone/CW, calibración de RX, audio, nombres de antenas, filtros, calibración, transverters, cables USB, periféricos, puertos serie, APD, temas, gestión de certificados fijados SmartLink y receptores KiwiSDR.

## Abrir el diálogo de Configuración de Radio

- Seleccione `Settings > Radio Setup...` desde el menú principal.

## Pestaña Radio

La pestaña Radio muestra la identificación del radio, información de licencia y controles de actualización de firmware.

### Información del radio (solo lectura)

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copiar junto al valor para copiar el número de serie al portapapeles. |
| **Region** | Región regulatoria (EE. UU. por defecto). |
| **HW Version** | Cadena de versión de hardware. |
| **Options** | Opciones licenciadas del radio. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado habilitado de multiFLEX. |
| **Model** | Modelo del radio. |

Cada campo de valor de solo lectura tiene un botón de copiar. Haga clic en el icono de portapapeles para copiar el valor al portapapeles del sistema. Una breve ventana emergente "Copied" confirma la acción. Los botones de copiar se atenúan visualmente cuando el valor está vacío o no disponible.

### Campos configurables por el usuario

| Control | Descripción | Notas |
|---|---|---|
| **Nickname** | Apodo del radio, fácil de usar. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. | Usa el nombre de host del SO si está vacío. Se almacena en AppSettings con la clave `StationName`. Se envía al radio como "client station <nombre>". |

### Información de licencia

La sección **License Info** muestra el estado de la suscripción, la fecha de expiración, el ID del radio y la versión licenciada. Cada campo incluye un botón de copiar al portapapeles junto al valor.

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta si hay actualizaciones de firmware. |
| **Select Installer...** | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el contenido .ssdr y emite el progreso. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |
| **Firmware status** | Vacío hasta que comienza una carga de firmware; luego muestra el progreso y el texto del resultado. |

### Control remoto y reinicio

| Control                                     | Descripción                                                                                                                                                              | Notas                                                                                                                                                                                                                                                                            |
|---------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Remote On**                               | Habilita el encendido remoto / remote-on.                                                                                                                                         |                                                                                                                                                                                                                                                                                  |
| **Reboot Radio**                            | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el arranque finaliza.                                        | Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend admite un reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN, el operador debe reconectarse manualmente después del reinicio.                                                            |
| Agent Automation (MCP):                     | Habilita el puente de automatización dentro de la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por activarlo.      | Nuevo en v26.8.4 (#3646). Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de esta opción y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se configure AETHER_AUTOMATION_ALLOW_TX. |
| Access Token:                               | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del SO.                           | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. El marcador de posición '(loading…)' aparece hasta que se lee el llavero.                                                                                                                                   |
| Copy (Access Token)                         | Copia el token de acceso al portapapeles.                                                                                                                                | Nuevo en v26.8.4.                                                                                                                                                                                                                                                                  |
| Rotate (Access Token)                       | Genera un nuevo token y lo aplica de inmediato, bloqueando a cualquier cliente que aún use el anterior.                                                                        | Nuevo en v26.8.4.                                                                                                                                                                                                                                                                  |
| Allow TX via MCP: Enable transmit control   | Permite que un cliente MCP keye el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; al habilitarlo por primera vez se muestra una confirmación de responsabilidad del operador.                              | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activo) y AETHER_AUTOMATION_NO_TX (fijado a inactivo). Un watchdog de des-keying forzado limita la TX originada por el puente.                                                                 |
| Observe only: Read-only (block all driving) | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) es rechazado.                                          | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija para ejecuciones headless/CI.                                                                                                                           |
| VITA-49 RX buffer:                          | Control deslizante de ajuste a valores predefinidos que establece el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un tamaño mayor absorbe ráfagas del panadapter/waterfall para que no se descarten paquetes. | Nuevo en v26.8.4 (#3810). Valores predefinidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <tamaño>' muestra lo que el kernel realmente concedió.                                                                                                           |
| granted: (VITA-49 RX buffer)                | Muestra el tamaño del buffer que el kernel realmente concedió (frente al valor predefinido solicitado).                                                                                             | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay ninguna conexión activa.                                                                                                                                                                                                       |
### Pestaña SmartLink

La pestaña SmartLink gestiona los certificados TLS SmartLink fijados. Enumera cada certificado fijado con el host, la huella SHA-256 y la fecha de fijación. Un desajuste de certificado fijado ahora pausa firmemente el handshake con un diálogo modal.

#### Certificados SmartLink fijados

| Control | Descripción |
|---|---|
| **Pinned SmartLink Certificates (sección)** | Encabezado de sección para la tabla de certificados fijados. Enumera cada host que este cliente ha fijado en la primera conexión (trust-on-first-use). |
| **Host / SHA-256 fingerprint / Pinned (columnas de tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), huella SHA-256 (monoespaciada), Pinned (YYYY-MM-DD o "(pre-phase 2)"). |
| **Forget selected** | Elimina la huella del certificado fijado del host seleccionado para que la próxima conexión vuelva a fijar silenciosamente. |
| **Forget all** | Borra todos los certificados fijados (con confirmación). La próxima conexión a cada radio vuelve a fijar silenciosamente. Muestra un diálogo de confirmación antes de borrar. |

## Pestaña Network

La pestaña Network muestra información de red del radio y ofrece opciones de configuración de red.

### Información de red (solo lectura)

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |

### Configuración de red

| Control | Predeterminado | Rango | Clave de configuración | Descripción |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | | | | Rechaza pares no RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado. |
| **Network MTU:** | 1450 | 576-9000 bytes | `NetworkMtu` | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | | | | Alterna entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | | | | Campos de configuración de IP estática (visibles solo en modo Static). |
| **Apply** | | | | Envía la configuración de red al radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y los datos de posición en vivo.

| Control | Descripción |
|---|---|
| GPS status | Muestra información de lat/lon/alt/hora/satélites cuando hay un GPS instalado y activo. |

## Pestaña TX

La pestaña TX controla los tiempos de transmisión, los interbloqueos, los límites de potencia, los modos de sintonía y el comportamiento de seguimiento slice/TX.

### Configuración de banda TX

| Control | Descripción |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. |

### Tiempos

| Control | Descripción |
|---|---|
| **Timings** | Tiempos de retención/retardo de TX. |

| Campo | Descripción | Notas |
|---|---|---|
| **ACC TX:** | Retardo de ACC TX en milisegundos. | Comando: `interlock set acc_tx_delay=<ms>` |
| **TX Delay:** | Retardo de TX en milisegundos. | Comando: `interlock set tx_delay=<ms>` |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | Comando: `interlock set tx1_delay=<ms>` |
| **Timeout (sec):** | Tiempo de espera del interbloqueo en segundos. Se muestra e ingresa en segundos completos; el radio almacena el valor internamente en milisegundos. | Comando: `interlock set timeout=<segundos * 1000>` |

### Interbloqueos

| Control | Descripción |
|---|---|
| **TX REQ: RCA** | Habilita la entrada de interbloqueo RCA. |
| **TX REQ: Accessory** | Habilita la entrada de interbloqueo de accesorios. |

### Potencia y sintonía

| Control | Predeterminado | Rango | Descripción |
|---|---|---|---|
| **Max Power:** | | 0-100% | Establece el límite máximo de potencia TX a nivel de radio. |
| **Tune Mode:** | | | Selecciona cómo se comporta el botón de sintonía. |

### Visualización en waterfall

| Control | Descripción |
|---|---|
| **Show TX in Waterfall:** | Cuando está habilitado, la señal de TX se dibuja en la visualización del waterfall. |

### Comportamiento de seguimiento slice/TX

| Control | Predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **TX Follows Active Slice** | False | `TxFollowsActiveSlice` | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | False | `ActiveFollowsTxSlice` | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el keyer CW y los valores predeterminados de RTTY.

### Medidor de nivel

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX. |

### Keyer CW

| Control | Predeterminado | Rango | Descripción |
|---|---|---|---|
| **Iambic:** | | Enabled / Disabled | Habilita o deshabilita el keyer iambic en el radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para el radio como para el keyer de software local. Par mutuamente excluyente. |
| **Swap:** | | | Intercambia dit/dah. |
| **Sideband:** | | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | | | Habilita el keying de macros CWX. |

### Decodificación

| Control | Predeterminado | Clave de configuración | Descripción |
|---|---|---|---|
| **Decode: RX** | True | `CwDecoder` (JSON anidado, campo `rx`) | Habilita la superposición de decodificación CW en el panadapter para CW recibido. |
| **Decode: TX** | False | `CwDecoder` (JSON anidado, campo `tx`) | Decodifica el keying CW del propio operador mediante sidetone del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña RX proporciona controles de calibración de frecuencia y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración son visibles independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, una línea de estado verde dice "GPSDO installed. Manual frequency offset calibration available."
- Si no hay un GPSDO instalado, una línea de estado amarilla dice "Manual frequency offset calibration available."

#### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece de inmediato.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no se inicia.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, ingresada en MHz con seis decimales. | Se envía al radio como `radio set cal_freq=<valor>`. |
| **Start** | Comienza el barrido de calibración. Se deshabilita y se etiqueta **Busy** mientras hay una calibración en curso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (pp
