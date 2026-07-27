# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, fonía/CW, RX, antenas, filtros, XVTR, cables USB, periféricos, serie/FlexControl, temas, APD, KiwiSDR y gestión de certificados SmartLink. Muchos valores de solo lectura incluyen un botón de copia al portapapeles junto a la etiqueta para compartir fácilmente con soporte técnico.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- La geometría del diálogo se conserva entre sesiones usando `PersistentDialog`.
- Los cambios realizados en algunas pestañas se aplican de inmediato; en otras, se requiere hacer clic en un botón Apply o Connect.
- Si limpia un campo de IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP y el puerto manual guardados se eliminan automáticamente y el dispositivo se desconecta.
- Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Themes, Audio, Filters, Peripherals, KiwiSDR en pantallas pequeñas o de alta densidad de píxeles) están envueltas en un área de desplazamiento vertical para que el diálogo no sobrepase el borde de la pantalla.
- Todos los indicadores QCheckBox usan tokens de ThemeManager para visibilidad en modo oscuro, con estados pseudo de hover y deshabilitado.

## Pestaña Radio

La pestaña Radio muestra información del radio, identificación, información de licencia, controles de actualización de firmware y un botón de reinicio.

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Haga clic en el botón de copia para copiar el número de serie al portapapeles. |
| **Region** | Región reglamentaria del radio (solo lectura). | |
| **HW Version** | Cadena de versión de hardware (solo lectura). | Haga clic en el botón de copia para copiar la cadena de versión al portapapeles. |
| **Remote On** | Habilita el encendido remoto / remote-on. | |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). | Haga clic en el botón de copia para copiar la cadena de opciones al portapapeles. |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). | |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). | |
| **Model** | Modelo del radio (solo lectura). | Haga clic en el botón de copia para copiar la cadena del modelo al portapapeles. |
| **Nickname** | Apodo del radio fácil de usar. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. | Se almacena en AppSettings como `StationName`. Se envía al radio como "client station \<nombre\>". |
| **License Info** | Muestra los detalles de licencia del radio: suscripción, vencimiento, ID de radio y versión licenciada. | Cada campo incluye un botón de copia al portapapeles junto al valor. |
| **Check for Update** | Consulta actualizaciones de firmware. | |
| **Select Installer...** | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | |
| **Reboot Radio** | Envía un comando de reinicio al radio conectado. Deshabilitado cuando el radio está desconectado. Muestra un diálogo de confirmación antes de reiniciar. En LAN, AetherSDR se reconecta automáticamente después de que el radio arranca. En SmartLink/WAN, debe reconectarse manualmente. | Nuevo en v26.6.3. El diálogo se cierra después de que el reinicio comienza. |

### Valores copiables (pestaña Radio)

El Radio SN, HW Version, Options, Model y cada campo de License Info muestran un pequeño botón de copia al pasar el ratón o al enfocarse. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema y aparece un breve mensaje emergente "¡Copiado!" cerca del botón.

### Reiniciar el radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Localice el botón **Reboot Radio**.
4. Haga clic en **Reboot Radio**.
   - Aparece un diálogo de confirmación con texto diferente según el tipo de conexión:
     - **WAN/SmartLink:** "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que el radio termine de arrancar."
     - **LAN:** "AetherSDR se desconectará y se reconectará automáticamente una vez que el radio termine de arrancar."
5. Haga clic en **OK** para confirmar.
   - El diálogo se cierra automáticamente.
   - El radio se reinicia y AetherSDR se desconecta.

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue usted mismo el instalador de SmartSDR desde flexradio.com, luego prepárelo manualmente.

#### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le dirige a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — instalador autoextraíble antiguo
   - `.ssdr` — archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
6. Cuando el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni se desconecte del radio mientras la carga está en progreso.

#### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Actualización disponible: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| El firmware está actualizado (v*x.y.z*) | No se requiere acción. |
| (texto de error en rojo) | La carga falló. Verifique que el archivo sea un archivo de firmware SmartSDR válido e intente de nuevo. |

## Pestaña Network

La pestaña Network muestra información de red del radio y permite configurar opciones de red avanzadas.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled". | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP Estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red al radio. | — |

### Cambiar el MTU de red

El ajuste Network MTU controla el tamaño máximo de paquete que el radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce el MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de selección **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU al radio.

## Pestaña GPS

La pestaña GPS muestra presencia de GPS y latitud, longitud, altitud, hora e información de satélites en vivo.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra presencia de GPS y datos de posición en vivo. |

## Pestaña TX

La pestaña TX controla tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y configuración de banda de TX.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (en ms)** | Tiempos de retención/retardo de TX. | — |
| **ACC TX:** | Retardo ACC TX en milisegundos. | — |
| **TX Delay:** | Retardo TX en milisegundos. | — |
| **RCA TX1:** | Retardo RCA TX1 en milisegundos. | — |
| **Timeout (seg):** | Tiempo de espera de enclavamiento en segundos (se muestra en segundos, se almacena en el radio en milisegundos). | — |
| **TX2 Delay:** | Retardo TX2 en milisegundos. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y Accessory. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante una operación Split. | Falso |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | Falso |

### Campos de tiempos TX

Los campos de tiempos TX controlan retardos y tiempos de espera para operaciones de transmisión. Tenga en cuenta que el campo **Timeout** se muestra en segundos para facilitar la lectura, pero el radio almacena y espera este valor en milisegundos internamente.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Localice la sección **Timings**.
4. Introduzca el valor deseado en cada campo.
   - ACC TX, TX Delay, RCA TX1 y TX2 Delay están en milisegundos.
   - Timeout está en segundos (rango 0–3600 segundos).
5. Pulse Enter o mueva el foco fuera del campo para aplicar el cambio.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en el radio. El botón de alternancia muestra "Enabled". | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita la macroactivación CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. | Verdadero |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. | — |

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz. Todos los controles de calibración son siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

| Control | Descripción |
|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. Vea la tabla a continuación. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Una etiqueta junto al cuadro combinado muestra la fuente resuelta y el estado de bloqueo.

#### Opciones del cuadro combinado

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando se ha recibido el estado del oscilador, o cuando el radio informa `tcxoPresent`, o cuando el ajuste actual o activo es `tcxo`. |
| GPSDO | Cuando el radio informa `gpsdoPresent`, o cuando el ajuste actual o activo es `gpsdo`. |
| External 10 MHz | Cuando se ha recibido el estado del oscilador, o cuando el radio informa `extPresent`, o cuando el ajuste actual o activo es `external`. |

#### Comportamiento de la etiqueta de estado

- Cuando se selecciona **Auto** y el radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <fuente>`.
- Cuando se selecciona una fuente específica y el radio está usando una diferente, la etiqueta muestra `<seleccionado> -> <activo>`.
- Cuando el ajuste y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se anexa: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta ninguna referencia externa, la etiqueta anexa `(not detected)`.
- Mientras el radio no ha informado el estado del oscilador, la etiqueta muestra
