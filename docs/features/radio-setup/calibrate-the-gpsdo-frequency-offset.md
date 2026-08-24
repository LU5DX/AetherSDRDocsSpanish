# Configuración de radio

El diálogo de Configuración de radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, Calibración, Antenas, Audio, Filtros, XVTR, cables USB, periféricos, APD, Temas, SmartLink y Serial (FlexControl).

## Abrir Configuración de radio

1. Haga clic en **Settings** en el menú principal.
2. Seleccione **Radio Setup...**.

El diálogo recuerda su posición y tamaño entre sesiones.

## Radio (pestaña)

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un botón de copiar que aparece con un icono de documento al pasar el cursor o al enfocarlo; haga clic en él para copiar el valor al portapapeles. Una breve ventana emergente "Copied!" confirma la acción.

### Información de la radio

Los siguientes campos son indicadores de solo lectura de la radio conectada:

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles (icono de bandeja) junto al valor. |
| **Region** | Región regulatoria de la radio (p. ej., USA). |
| **HW Version** | Cadena de versión del hardware. Incluye un botón de copiar al portapapeles junto al valor. |
| **Options** | Opciones de radio licenciadas. Incluye un botón de copiar al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado de habilitación de multiFLEX. |
| **Model** | Modelo de la radio. Incluye un botón de copiar al portapapeles junto al valor. |
| **License Info** | Detalles de suscripción, fecha de expiración, ID de radio y versión licenciada. Cada campo incluye un botón de copiar al portapapeles junto al valor. |

### Campos de identificación de la radio

| Control | Descripción |
|---|---|
| **Nickname** | Apodo amigable de la radio. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo por defecto. Clave de configuración: `StationName`. |

### Control remoto y reinicio

| Control                                     | Descripción                                                                                                                                                                                                                                                                | Notas                                                                                                                                                                                                                                                                           |
|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Remote On**                               | Habilita el encendido remoto / activación remota.                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                 |
| **Reboot Radio**                            | Reinicia la radio conectada con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente cuando el arranque finaliza.                                                                                                                     | Nuevo en v26.8.4 (#4448). Solo se habilita cuando hay conexión y el backend admite reinicio del cliente (p. ej., HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN, el operador debe reconectarse manualmente después del reinicio.                    |
| Agent Automation (MCP):                     | Habilita el puente de automatización integrado en la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador decide activarlo.                    | Nuevo en v26.8.4 (#3646). Se guarda mediante AutomationBridgeSettings. La variable de entorno AETHER_AUTOMATION fuerza la activación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado salvo que se defina AETHER_AUTOMATION_ALLOW_TX. |
| Access Token:                               | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo.                                                                                        | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero de claves.                                                                                   |
| Copy (Access Token)                         | Copia el token de acceso al portapapeles.                                                                                                                                                                                                                                   | Nuevo en v26.8.4.                                                                                                                                                                                                                                                               |
| Rotate (Access Token)                       | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior.                                                                                                                                                                   | Nuevo en v26.8.4.                                                                                                                                                                                                                                                               |
| Allow TX via MCP: Enable transmit control   | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador.                                                                                              | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (forzado a desactivado). Un vigilante de des-keying forzado limita la TX originada por el puente.          |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero cada verbo de mutación (set/invoke/connect/tune/capture) es rechazado.                                                                                                            | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI.                                                                          |
| VITA-49 RX buffer:                          | Control deslizante de ajuste rápido que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para evitar la pérdida de paquetes.                                                | Nuevo en v26.8.4 (#3810). Valores predefinidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió.                                                                        |
| granted: (VITA-49 RX buffer)                | Muestra el tamaño de búfer que el kernel realmente concedió (frente al valor predefinido solicitado).                                                                                                                                                                      | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa.                                                                                                                                                                                                 |

### Actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta actualizaciones de firmware. |
| **Select Installer...** | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager, que extrae el contenido .ssdr y emite el progreso. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. |

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el archivo descargado. AetherSDR acepta `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio. Una barra de progreso y texto de estado muestran el avance de la carga.

## SmartLink (pestaña)

La pestaña SmartLink gestiona los certificados TLS SmartLink fijados. Enumera cada certificado fijado (host, huella digital SHA-256, fecha de fijación) con botones Forget y Forget All por fila. La pestaña se construye de forma diferida al hacer clic por primera vez. Si ocurre una discrepancia de fijación de certificado, el apretón de manos se pausa con un diálogo modal.

| Control | Descripción |
|---|---|
| **Pinned SmartLink Certificates (sección)** | Encabezado de sección para la tabla de certificados fijados. Enumera cada host que este cliente ha fijado en la primera conexión (confianza en el primer uso). |
| **Host / SHA-256 fingerprint / Pinned (columnas de tabla)** | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (YYYY-MM-DD o '(pre-phase 2)'). |
| **Forget selected** | Elimina la huella digital del certificado fijado del host seleccionado, de modo que la próxima conexión vuelva a fijar silenciosamente. |
| **Forget all** | Borra todos los certificados fijados (con confirmación). La próxima conexión a cada radio vuelve a fijar silenciosamente. Muestra un diálogo de confirmación antes de borrar. |

## Network (pestaña)

La pestaña Network muestra información de red de la radio y ofrece opciones de red avanzadas.

### Información de red

| Control | Descripción |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |

### Configuración de red

| Control | Descripción |
|---|---|
| **Enforce Private IP Connections** | Conmutador para rechazar pares no RFC1918. |
| **Network MTU** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango válido: 576-9000 bytes. Predeterminado: 1450. Clave de configuración: `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |

### Configuración de IP

1. Cambie entre **DHCP** y **Static** usando el botón conmutador.
2. En modo Static, ingrese la **IP Address**, **Mask** y **Gateway**.
3. Haga clic en **Apply** para enviar la configuración de red a la radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS e información en vivo, incluidos latitud, longitud, altitud, hora y número de satélites.

## TX (pestaña)

La pestaña TX proporciona configuración de transmisión, incluidos tiempos, enclavamientos, límites de potencia, modo de sintonía y opciones de visualización en el waterfall.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos

| Control | Descripción |
|---|---|
| **Timings (in ms)** | Tiempos de retención / retardo de TX. |

### Enclavamientos

| Control | Descripción |
|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y de accesorio. |

### Potencia y sintonía

| Control | Descripción |
|---|---|
| **Max Power** | Establece el límite máximo de potencia TX a nivel de radio. Rango válido: 0-100%. |
| **Tune Mode** | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Descripción |
|---|---|
| **Show TX in Waterfall** | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | La TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. Clave de configuración: `TxFollowsActiveSlice`. Predeterminado: False. |
| **Active Slice Follows TX** | Cambia el slice activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Clave de configuración: `ActiveFollowsTxSlice`. Predeterminado: False. |

## Phone/CW (pestaña)

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

| Control | Descripción |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Descripción |
|---|---|
| **Iambic** | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. Predeterminado: A. |
| **Swap** | Intercambia dit/dah. |
| **Sideband** | Selecciona la banda lateral del tono CW. Rango válido: LSB, USB. |
| **CWX** | Habilita el keying de macros CWX. |
| **Decode: RX** | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Clave de configuración: `CwDecoder` (JSON anidado, campo `rx`). Predeterminado: True. |
| **Decode: TX** | Decodifica el propio keying CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Clave de configuración: `CwDecoder` (JSON anidado, campo `tx`). Predeterminado: False. |

### RTTY

| Control | Descripción |
|---|---|
| **RTTY Mark Default** | Frecuencia predeterminada de marca RTTY. |

## RX (pestaña)

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

1. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia conocida y precisa.
2. Haga clic en **Start** para comenzar el barrido de calibración. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido.
3. Cuando el barrido se complete, revise la desviación medida en **Freq Offset (ppb):**.
4. Si prefiere establecer la desviación manualmente, edite **Freq Offset (ppb):** directamente.

### Mensajes de estado de calibración

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul-gris | La secuencia de comandos de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. |
| Busy | — | Se muestra en el propio botón **Start** mientras un barrido está en curso. |

### Fuente de referencia de 10 MHz

| Control | Descripción |
|---|---|
| **10 MHz Reference Source** | Selecciona la fuente de referencia del oscilador. Valores válidos: Auto, TCXO, GPSDO, External 10 MHz. Las opciones mostradas dependen del hardware instalado. |

La etiqueta de estado de bloqueo junto al cuadro combinado muestra el estado actual del oscilador:

| Visualización | Significado |
|---|---|
| `Auto -> GPSDO` (locked) | Auto seleccionado, la radio eligió GPSDO, bloqueado |
| `GPSDO` (locked) | Fuente coincidente y bloqueada |
| `External 10 MHz` (not detected) | External seleccionado pero no se detecta señal |

Codificación de colores:
- Verde (`#00c040`): El oscilador está bloqueado.
- Rojo (`#c04040`): El oscilador está desbloqueado.
- Azul-gris (`#8aa8c0`): El estado del oscilador aún no se ha recibido.

### Banner de estado GPSDO

- **Banner verde**: GPSDO instalado. La calibración manual de desviación de frecuencia está disponible.
- **Banner ámbar**: Sin GPSDO instalado. La calibración manual de desviación de frecuencia está disponible.

## Calibration (pestaña)

La pestaña
