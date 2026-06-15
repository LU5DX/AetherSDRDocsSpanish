# Configuración de Radio

El diálogo de Configuración de Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD, temas, gestión de certificados SmartLink y (opcionalmente) FlexControl serial.

El diálogo recuerda su tamaño y posición entre sesiones.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

**Soporte de desplazamiento:** En v26.6.3, la pestaña Radio (y otras pestañas con grupos de contenido apilados) se envolvió en un QScrollArea vertical. Esto evita que el diálogo exceda la altura de la pantalla en pantallas pequeñas o de alta densidad. La barra de desplazamiento se oculta cuando el contenido ya cabe.

| Control                                             | Comportamiento                                                                                                                                                                                    | Predeterminado                                                                                                                             |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| Radio SN                                            | Número de serie del chasis (solo lectura).                                                                                                                                                        | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976).                                    |
| Region                                              | Región regulatoria de la radio (solo lectura).                                                                                                                                                    | USA                                                                                                                                        |
| HW Version                                          | Cadena de versión de hardware.                                                                                                                                                                    | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                          |
| Remote On                                           | Habilita el encendido remoto / activación remota.                                                                                                                                                  | —                                                                                                                                          |
| Options                                             | Muestra las opciones de radio licenciadas.                                                                                                                                                        | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                          |
| FlexControl                                         | Estado detectado del hardware FlexControl (solo lectura).                                                                                                                                         | —                                                                                                                                          |
| multiFLEX                                           | Estado habilitado de multiFLEX (solo lectura).                                                                                                                                                    | —                                                                                                                                          |
| Model                                               | Modelo de radio.                                                                                                                                                                                  | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                          |
| Nickname                                            | Apodo amigable de la radio.                                                                                                                                                                       | —                                                                                                                                          |
| Callsign                                            | Indicativo de la estación.                                                                                                                                                                        | —                                                                                                                                          |
| Station Name                                        | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto es el nombre de host del sistema operativo si está vacío.                                                            | —                                                                                                                                          |
| License Info                                        | Muestra los detalles de la licencia de la radio (Suscripción / Expiración / ID de Radio / Versión licenciada).                                                                                    | —                                                                                                                                          |
| Check for Update                                    | Consulta actualizaciones de firmware.                                                                                                                                                             | —                                                                                                                                          |
| Upload Firmware                                     | Inicia la carga de firmware con barra de progreso y estado.                                                                                                                                       | —                                                                                                                                          |
| Select Installer...                                 | Abre un diálogo de archivo para un instalador SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3.                                                              |
| Reboot Radio                                        | Reinicia la radio conectada. Abre un diálogo de confirmación antes de enviar el comando de reinicio. Cuando está conectado a través de SmartLink/WAN, la reconexión automática no es compatible después del reinicio; reconéctese manualmente después de que la radio termine de iniciar. En LAN, AetherSDR se reconecta automáticamente una vez que la radio vuelve a estar en línea. El diálogo se cierra después del reinicio. | Deshabilitado cuando la radio está desconectada; habilitado/deshabilitado automáticamente según el estado de la conexión.                 |
| SmartLink (pestaña)                                 | Gestión de certificados TLS SmartLink anclados. Enumera cada certificado anclado (host, huella SHA-256, fecha de anclaje) con olvidar por fila y Olvidar Todos. Nuevo en v26.5.3 (#2951 Fase 2).   | Construido perezosamente al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de anclaje ahora pausa firmemente el protocolo de enlace con un diálogo modal. |
| Pinned SmartLink Certificates (sección)             | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Enumera cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso).    | Fase 2 de GHSA-wfx7-w6p8-4jr2. Esquema de anclaje migrado de cadenas simples a objetos {fp, pinnedAt}.                                   |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), huella SHA-256 (monoespaciada), Pinned (AAAA-MM-DD o '(pre-fase 2)').                                                             | Respaldado por WanCertCache en WanConnection.cpp.                                                                                          |
| Forget selected                                     | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión vuelva a anclar silenciosamente.                                                                     |                                                                                                                                            |
| Forget all                                          | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio vuelve a anclar silenciosamente.                                                                      | Muestra QMessageBox::question antes de borrar.                                                                                            |

### Botones de copia

Cada indicador de solo lectura en la pestaña Radio (Radio SN, Region, HW Version, Options, FlexControl, multiFLEX, Model, campos de License Info) ahora incluye un pequeño botón de copia que aparece al pasar el ratón. Haga clic en el botón para copiar el valor mostrado al portapapeles.

### Área de resumen

La pestaña Radio también muestra:
- **Firmware status** — Vacío hasta que comience una carga de firmware, luego muestra el progreso y el texto del resultado.
- **License Info** — Estado de suscripción, fecha de expiración, ID de Radio y versión licenciada.

## Pestaña Red

La pestaña Red muestra información de red de la radio y opciones avanzadas de red.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| IP Address / Mask / MAC Address | Direcciones de red de solo lectura. | — | — |
| Enforce Private IP Connections: | Rechaza pares no RFC1918. | — | — |
| Network MTU: | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. | 1450 | `NetworkMtu` |
| DHCP / Static | Cambia entre modos DHCP e IP estática. | — | — |
| IP Address: / Mask: / Gateway: | Campos de configuración de IP estática. | — | — |
| Apply | Envía la configuración de red a la radio. | — | — |

**Nota:** El MTU predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de lat/lon/alt/hora/satélites.

## Pestaña TX

La pestaña TX configura temporizaciones TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuración de bandas TX.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| TX Band Settings | Abre el diálogo dedicado de potencia/sintonía por banda. | — | — |
| Timings | Temporizaciones de retención/retardo TX en milisegundos; el tiempo de espera se muestra en segundos. | — | — |
| Interlocks - TX REQ: RCA / Accessory | Habilita las entradas de enclavamiento RCA y accessory. | — | — |
| Max Power: | Establece el límite de potencia TX a nivel de radio (0-100%). | — | — |
| Tune Mode: | Selecciona cómo se comporta el botón de sintonía. | — | — |
| Show TX in Waterfall: | Dibuja la señal TX en el waterfall. | — | — |
| TX Follows Active Slice | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. | Falso | `TxFollowsActiveSlice` |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. | Falso | `ActiveFollowsTxSlice` |

**Nota sobre el campo de tiempo de espera:** El campo "Timeout" ahora está etiquetado como **Timeout (sec)** y muestra el valor en segundos. Internamente la radio lo almacena en milisegundos; la configuración se convierte automáticamente al enviarla.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el tecleador CW y los valores predeterminados de RTTY.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Enable/Disable the Level Meter During Receive | Muestra el medidor de nivel de micrófono incluso en RX. | — | — |
| Iambic: | Habilita o deshabilita el tecleador iambic en la radio. | — | — |
| Iambic Mode: A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el tecleador de software local. | A | — |
| Swap: | Intercambia dit/dah. | — | — |
| Sideband: | Selecciona la banda lateral de tono CW (LSB | USB). | — | — |
| CWX: | Habilita el tecleo de macros CWX. | — | — |
| Decode: | Habilita la superposición de decodificación CW en el panadapter. | Verdadero | `CwDecodeOverlay` |
| RTTY Mark Default: | Frecuencia de marca RTTY predeterminada. | — | — |

**Nota:** En v0.9.1, se agregaron los botones Modo A y Modo B junto al interruptor de habilitación. Modo A = Curtis A; Modo B = Curtis B. Estos también controlan el nuevo tecleador iambic de software local (IambicKeyer) que refleja el estado iambic de la radio para un tono de prueba de menos de 5 ms.

## Pestaña RX

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y configuración de la fuente de referencia de 10 MHz.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Cal Frequency (MHz): | Frecuencia utilizada para la calibración manual. | — | — |
| Start | Inicia el barrido de calibración de frecuencia. | — | — |
| Freq Offset (ppb): | Desviación de frecuencia manual en ppb. | — | — |
| 10 MHz Reference Source: | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/Externa). | Auto | — |

### Visualización de la fuente de referencia de 10 MHz (v0.9.7)

El cuadro combinado `10 MHz Reference Source:` en la pestaña `RX` se actualizó en v0.9.7. La lista de fuentes disponibles y la etiqueta de estado de bloqueo junto a ella ahora se comportan de manera diferente a versiones anteriores.

#### Cuadro combinado de fuente

El cuadro combinado ahora se completa dinámicamente según el hardware presente en la radio conectada y la configuración actual del oscilador y el estado informado por la radio. Pueden aparecer las siguientes fuentes:

| Entrada | Cuándo se muestra |
|---|---|
| Auto | Siempre se muestra. |
| TCXO | Se muestra cuando la radio informa que hay un TCXO presente, o cuando el estado actual o informado se refiere a TCXO. |
| GPSDO | Se muestra cuando la radio informa que hay un GPSDO presente, o cuando el estado actual o informado se refiere a GPSDO. |
| External 10 MHz | Se muestra cuando la radio informa que hay una referencia externa presente o activa, o cuando el estado actual o informado se refiere a externa. Nota: la etiqueta cambió de "External" a "External 10 MHz" en v0.9.7. |

El cuadro combinado selecciona automáticamente la configuración de oscilador guardada cuando se abre el diálogo. Si la configuración guardada no está en la lista, se intenta con el estado actual informado; si ese también está ausente, se selecciona Auto.

#### Etiqueta de estado de bloqueo

La etiqueta de estado junto al cuadro combinado se actualizó para mostrar información más rica:

- Cuando se selecciona Auto y la radio ha cambiado a una fuente específica, la etiqueta muestra **Auto -> \<fuente\>** seguido de **Locked** o **Unlocked**.
- Cuando la fuente solicitada difiere de la fuente activa, la etiqueta muestra **\<solicitada\> -> \<activa\>** seguido de **Locked** o **Unlocked**.
- Cuando las fuentes solicitada y activa coinciden, la etiqueta muestra **\<fuente\> Locked** o **\<fuente\> Unlocked**.
- Cuando se selecciona External 10 MHz pero no se detecta ninguna referencia externa, la etiqueta agrega **(not detected)**.
- Mientras se espera que la radio informe el estado del oscilador, la etiqueta muestra **Waiting for oscillator status**.

El color de la etiqueta es verde cuando está bloqueada y rojo cuando está desbloqueada. Antes de que la radio informe cualquier estado del oscilador, la etiqueta se muestra en gris neutro.

## Pestaña Antenas

La pestaña Antenas le permite asignar nombres amigables a cada puerto de antena de la radio.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| ANT1 / ANT2 / XVTA / XVTB | Campos de texto para establecer nombres amigables para cada puerto de antena. | — | — |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Line Out: | Control deslizante de ganancia de salida de línea. | — | — |
| Mute (Line Out) | Silencia la salida de línea. | — | — |
| Headphone: | Control deslizante de ganancia de auriculares. | — | — |
| Mute (Headphone) | Silencia los auriculares. | — | — |
| Front Speaker: / Mute | Silencia el altavoz frontal (específico del modelo). | — | — |
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio para SmartLink/LAN. | Auto | `AudioCompression` |
| Prevent system sleep while connected | Mantiene el sistema operativo despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. | Falso | `InhibitSleepWhileConnected` |
| PC Audio Devices: Input: / Output: | Selecciona los dispositivos de audio de entrada/salida del host. | — | — |
| Audio Boost: | Habilita ganancia adicional en la ruta de audio del cliente. | — | `AudioBoost` |
| Audio Buffer: | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. | 200 | `AudioBufferMs` |
| Recording: Radio Side / Client Side | Selecciona la grabación del lado de la radio o del lado del cliente. | Radio Side | `RecordingMode` |
| Save to: | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. | — | `QsoRecordingDir` |
| ... | Navega para buscar la carpeta de grabación. | — | — |
| Auto-record on TX | Graba automáticamente mientras transmite. | Falso | `Qso
