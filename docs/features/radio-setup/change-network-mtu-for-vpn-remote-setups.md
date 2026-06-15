# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, fonía/CW, RX, antenas, filtros, XVTR, cables USB, periféricos, serie/FlexControl, temas y gestión de certificados SmartLink. Muchos valores de solo lectura incluyen un botón de copia al portapapeles junto a la etiqueta para compartir fácilmente con soporte técnico.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- La geometría del diálogo se conserva entre sesiones usando `PersistentDialog`.
- Los cambios realizados en algunas pestañas se aplican de inmediato; otros requieren hacer clic en un botón Apply o Connect.
- Si limpia un campo IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP y el puerto manual guardados se eliminan automáticamente y el dispositivo se desconecta.
- Las pestañas cuyo contenido puede exceder la altura visible del diálogo (Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alta DPI) están envueltas en un área de desplazamiento vertical para que el diálogo no desborde el borde de la pantalla.

## Radio (pestaña)

La pestaña Radio muestra información de la radio, identificación, información de licencia, controles de actualización de firmware y un botón de reinicio.

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Haga clic en el botón de copia para copiar el número de serie al portapapeles. |
| **Region** | Región regulatoria de la radio (solo lectura). | |
| **HW Version** | Cadena de versión de hardware (solo lectura). | Haga clic en el botón de copia para copiar la cadena de versión al portapapeles. |
| **Remote On** | Habilita el encendido remoto / remote-on. | |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). | Haga clic en el botón de copia para copiar la cadena de opciones al portapapeles. |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). | |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). | |
| **Model** | Modelo de radio (solo lectura). | Haga clic en el botón de copia para copiar la cadena del modelo al portapapeles. |
| **Nickname** | Apodo amigable de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. | Se almacena en AppSettings como `StationName`. Se envía a la radio como "client station \<nombre\>". |
| **License Info** | Muestra los detalles de la licencia de la radio: suscripción, vencimiento, ID de radio y versión licenciada. | Cada campo incluye un botón de copia al portapapeles junto al valor. |
| **Check for Update** | Consulta actualizaciones de firmware. | |
| **Select Installer...** | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3. |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | |
| **Reboot Radio** | Envía un comando de reinicio a la radio conectada. Deshabilitado cuando la radio está desconectada. Muestra un diálogo de confirmación antes de reiniciar. En LAN, AetherSDR se reconecta automáticamente después de que la radio arranca. En SmartLink/WAN, debe reconectarse manualmente. | Nuevo en v26.6.3. El diálogo se cierra después de que comienza el reinicio. |

### Valores copiables (pestaña Radio)

Radio SN, HW Version, Options, Model y cada campo de License Info muestran un pequeño botón de copia al pasar el ratón o al enfocar. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema y se muestra un breve mensaje emergente "Copied!" cerca del botón.

### Reiniciar la radio

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Localice el botón **Reboot Radio**.
4. Haga clic en **Reboot Radio**.
   - Aparece un diálogo de confirmación con texto diferente según el tipo de conexión:
     - **WAN/SmartLink:** "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que la radio termine de arrancar."
     - **LAN:** "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de arrancar."
5. Haga clic en **OK** para confirmar.
   - El diálogo se cierra automáticamente.
   - La radio se reinicia y AetherSDR se desconecta.

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue el instalador de SmartSDR desde flexradio.com usted mismo y luego prepárelo manualmente.

#### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le dirige a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — Instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — Instalador autoextraíble más antiguo
   - `.ssdr` — Archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
6. Cuando el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso sigue la carga.
   - No cierre el diálogo ni se desconecte de la radio mientras la carga está en progreso.

#### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se necesita acción. |
| (texto de error en rojo) | La carga falló. Verifique que el archivo sea un archivo de firmware SmartSDR válido e intente nuevamente. |

## Network (pestaña)

La pestaña Network muestra la información de red de la radio y permite configurar opciones de red avanzadas.

| Control | Descripción | Predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled". | — |
| **Network MTU:** | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes. Rango 576–9000 bytes. El predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red a la radio. | — |

### Cambiar el MTU de red

La configuración de Network MTU controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce el MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de selección **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## GPS (pestaña)

La pestaña GPS muestra presencia de GPS e información en vivo de latitud, longitud, altitud, hora y satélites.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra presencia de GPS y datos de posición en vivo. |

## TX (pestaña)

La pestaña TX controla tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y Configuración de Banda de TX.

| Control | Descripción | Predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (in ms)** | Tiempos de espera/retardo de TX. | — |
| **ACC TX:** | Retardo de ACC TX en milisegundos. | — |
| **TX Delay:** | Retardo de TX en milisegundos. | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento en segundos (mostrado en segundos, almacenado en la radio en milisegundos). | — |
| **TX2 Delay:** | Retardo de TX2 en milisegundos. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accesorio. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante operación en Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |

### Campos de tiempo de TX

Los campos de tiempo de TX controlan los retardos y tiempos de espera para operaciones de transmisión. Tenga en cuenta que el campo **Timeout** se muestra en segundos para facilitar la lectura, pero la radio almacena y espera este valor en milisegundos internamente.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Localice la sección **Timings**.
4. Ingrese el valor deseado en cada campo.
   - ACC TX, TX Delay, RCA TX1 y TX2 Delay están en milisegundos.
   - Timeout está en segundos (rango 0–3600 segundos).
5. Presione Enter o mueva el foco lejos del campo para aplicar el cambio.

## Phone/CW (pestaña)

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Descripción | Predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en la radio. El botón de alternancia muestra "Enabled". | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita la activación de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |

## RX (pestaña)

La pestaña RX proporciona calibración de desplazamiento de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz. Todos los controles de calibración son siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

| Control | Descripción |
|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. Ver tabla a continuación. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Una etiqueta junto al cuadro combinado muestra la fuente resuelta y el estado de bloqueo.

#### Opciones del cuadro combinado

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

#### Comportamiento de la etiqueta de estado

- Cuando **Auto** está seleccionado y la radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <fuente>`.
- Cuando se selecciona una fuente específica y la radio está usando una diferente, la etiqueta muestra `<seleccionado> -> <activo>`.
- Cuando la configuración y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se agrega: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta ninguna referencia externa, la etiqueta agrega `(not detected)`.
- Mientras la radio no ha informado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en gris.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que av
