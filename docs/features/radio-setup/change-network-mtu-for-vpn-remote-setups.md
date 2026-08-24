# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información del radio, red, GPS, TX, teléfono/CW, RX, calibración, antenas, filtros, XVTR, cables USB, periféricos, serial/FlexControl, temas, APD y gestión de certificados SmartLink. Muchos valores de solo lectura incluyen un botón de copiar al portapapeles junto a la etiqueta para facilitar su uso compartido con soporte.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- La geometría del diálogo se conserva entre sesiones usando `PersistentDialog`.
- Los cambios realizados en algunas pestañas se aplican inmediatamente; otros requieren hacer clic en un botón Apply o Connect.
- Si limpia un campo de IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP y el puerto manuales guardados se eliminan automáticamente y el dispositivo se desconecta.
- Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alto DPI) están envueltas en un área de desplazamiento vertical para que el diálogo no desborde el borde de la pantalla.
- Todos los indicadores QCheckBox usan tokens de ThemeManager para visibilidad en modo oscuro, con estados pseudo de hover y deshabilitado.
- El filtro de búsqueda respeta las páginas restringidas por capacidad: escribir una palabra clave que coincida con una página oculta (por ejemplo, "calibration" en un Flex) no muestra una página que el radio no pueda usar.

## Pestaña Radio

La pestaña Radio muestra información del radio, identificación, información de licencia, controles de actualización de firmware y un botón de reinicio.

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Incluye un botón de copiar al portapapeles junto al valor. Nuevo en v26.5.3 (#2976). |
| **Region** | Región regulatoria del radio (solo lectura). | |
| **HW Version** | Cadena de versión de hardware (solo lectura). | Incluye un botón de copiar al portapapeles junto al valor. |
| **Remote On** | Habilita el encendido remoto / remote-on. | |
| **Options** | Muestra las opciones licenciadas del radio (solo lectura). | Incluye un botón de copiar al portapapeles junto al valor. |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). | |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). | |
| **Model** | Modelo del radio (solo lectura). | Incluye un botón de copiar al portapapeles junto al valor. |
| **Nickname** | Apodo amigable del radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se establece por defecto al nombre de host del sistema operativo si está vacío. | Se almacena en AppSettings como `StationName`. Se envía al radio como "client station \<name\>". |
| **License Info** | Muestra los detalles de licencia del radio: suscripción, expiración, ID del radio y versión licenciada. | Cada campo (Subscription, Expiration, Radio ID, Licensed version) incluye un botón de copiar al portapapeles junto al valor. |
| **Check for Update** | Consulta actualizaciones de firmware. | |
| **Select Installer...** | Abre un diálogo de archivos para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr pre-extraído. Pasa la ruta seleccionada a FirmwareStager que extrae el contenido .ssdr y emite el progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. | |
| **Reboot Radio** | Reinicia el radio conectado con un diálogo de confirmación. AetherSDR se desconecta y (en LAN) se reconecta automáticamente una vez que el arranque finaliza. | Nuevo en v26.8.4 (#4448). Solo se habilita cuando está conectado y el backend soporta un reinicio del cliente (por ejemplo, HL2 es solo RX, por lo que el botón está deshabilitado). En SmartLink/WAN el operador debe reconectarse manualmente después del reinicio. |
| Agent Automation (MCP): | Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por habilitarlo. | Nuevo en v26.8.4 (#3646). Se conserva mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz. El keying de transmisión permanece bloqueado a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token: | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén secreto del sistema operativo. | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador de posición '(loading…)' hasta que la lectura del llavero esté disponible. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP keyee el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado a desactivado). Un watchdog de fuerza-deskey limita TX originado por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero todo verbo mutador (set/invoke/connect/tune/capture) es rechazado. | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija a activado para ejecuciones headless/CI. |
| VITA-49 RX buffer: | Control deslizante de ajuste a valores preestablecidos que establece el buffer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se descarten paquetes. | Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión en net.core.rmem_max; una etiqueta en vivo 'granted: \<size\>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de buffer que el kernel realmente concedió (vs. el valor preestablecido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay conexión activa. |

### Valores copiables (pestaña Radio)

Los campos Radio SN, HW Version, Options, Model y cada campo de License Info muestran un pequeño botón de copiar al pasar el cursor o al enfocarlos. Al hacer clic en el botón se copia el valor mostrado al portapapeles del sistema y se muestra un aviso breve "Copied!" cerca del botón.

### Reiniciar el radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Localice el botón **Reboot Radio**.
4. Haga clic en **Reboot Radio**.
   - Aparece un diálogo de confirmación con texto diferente según el tipo de conexión:
     - **WAN/SmartLink:** "AetherSDR will disconnect. SmartLink/WAN sessions do not auto-reconnect today — you will need to reconnect manually once the radio finishes booting."
     - **LAN:** "AetherSDR will disconnect and automatically reconnect once the radio finishes booting."
5. Haga clic en **OK** para confirmar.
   - El diálogo se cierra automáticamente.
   - El radio se reinicia y AetherSDR se desconecta.

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue el instalador SmartSDR de flexradio.com usted mismo y luego prepárelo manualmente.

#### Preparación de una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le dirige a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — instalador autoextraíble más antiguo
   - `.ssdr` — archivo de firmware pre-extraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
6. Cuando el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni se desconecte del radio mientras la carga esté en curso.

#### Mensajes de estado de firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com y luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere acción. |
| (texto de error en rojo) | La carga falló. Verifique que el archivo sea un archivo de firmware SmartSDR válido e intente nuevamente. |

## Pestaña Network

La pestaña Network muestra la información de red del radio y le permite configurar opciones de red avanzadas.

| Control | Descripción | Predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no son RFC1918. El botón de alternancia muestra "Enabled". | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Alterna entre modos de IP DHCP y estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red al radio. | — |

### Cambiar el MTU de red

La configuración de Network MTU controla el tamaño máximo de paquete que el radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce el MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de giro **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de ruta de su red.
5. Haga clic en **Apply** para enviar el nuevo MTU al radio.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la latitud, longitud, altitud, hora e información de satélites en vivo.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra la presencia de GPS y los datos de posición en vivo. |

## Pestaña TX

La pestaña TX controla los tiempos de TX, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y la configuración de banda de TX.

| Control | Descripción | Predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (in ms)** | Tiempos de retención/retardo de TX. | — |
| **ACC TX:** | Retardo de ACC TX en milisegundos. | — |
| **TX Delay:** | Retardo de TX en milisegundos. | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de interbloqueo en segundos (se muestra en segundos, se almacena en el radio en milisegundos). | — |
| **TX2 Delay:** | Retardo de TX2 en milisegundos. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de interbloqueo RCA y de accesorio. | — |
| **Max Power:** | Establece el límite máximo de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |

### Campos de tiempos de TX

Los campos de tiempos de TX controlan los retardos y tiempos de espera para las operaciones de transmisión. Tenga en cuenta que el campo **Timeout** se muestra en segundos para
