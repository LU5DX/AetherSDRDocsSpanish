# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, antenas, filtros, XVTR, cables USB, periféricos, APD, temas, puerto serie y configuración de certificados anclados de SmartLink.

## Abrir el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su tamaño y posición se guardan entre sesiones.

---

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control                                         | Tipo                                                                                                                                                                                        | Comportamiento                                                                                                                                                          |
|-------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Radio SN                                        | Número de serie del chasis (solo lectura).                                                                                                                                                  | Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976).                                                                 |
| Region                                          | Indicador                                                                                                                                                                                   | Región regulatoria de la radio.                                                                                                                                         |
| HW Version                                      | Cadena de versión de hardware.                                                                                                                                                              | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                       |
| Model                                           | Modelo de la radio.                                                                                                                                                                         | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                       |
| Options                                         | Muestra las opciones de radio licenciadas.                                                                                                                                                  | Incluye un botón de copia al portapapeles junto al valor (#2976).                                                                                                       |
| FlexControl                                     | Indicador                                                                                                                                                                                   | Estado detectado del hardware FlexControl.                                                                                                                              |
| multiFLEX                                       | Indicador                                                                                                                                                                                   | Estado habilitado de multiFLEX.                                                                                                                                         |
| Nickname                                        | Campo de texto                                                                                                                                                                              | Apodo descriptivo de la radio.                                                                                                                                          |
| Callsign                                        | Campo de texto                                                                                                                                                                              | Indicativo de la estación.                                                                                                                                              |
| Station Name                                    | Campo de texto                                                                                                                                                                              | Identifica a este cliente de AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Almacenado en AppSettings. Enviado a la radio como 'client station \<nombre\>'. |
| License Info                                    | Indicador                                                                                                                                                                                   | Muestra los detalles de la licencia desde la radio (Suscripción, Vencimiento, ID de radio, Versión licenciada).                                                         |
| Select Installer...                             | Abre un diálogo de archivo para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3.                                                                                              |
| Reboot Radio                                    | Botón pulsador                                                                                                                                                                              | Reinicia la radio conectada. Deshabilitado cuando la radio está desconectada. Muestra un diálogo de confirmación antes de reiniciar. En conexiones LAN, AetherSDR se reconecta automáticamente tras el arranque de la radio; en SmartLink/WAN, se requiere reconexión manual. Nuevo en v26.6.3 (#3334). |
| SmartLink (pestaña)                             | Gestión de certificados TLS anclados de SmartLink. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con opciones Forget selected y Forget All por fila. Nuevo en v26.5.3 (#2951 Fase 2).     | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: una discrepancia de anclaje de certificado ahora pausa el protocolo de enlace con un diálogo modal. |
| Pinned SmartLink Certificates (sección)         | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso).                                          | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}.                                                                  |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), SHA-256 fingerprint (monoespaciado), Pinned (AAAA-MM-DD o '(pre-phase 2)').                                                                         | Respaldado por WanCertCache en WanConnection.cpp.                                                                                                                           |
| Forget selected                                 | Elimina la huella del certificado anclado del host seleccionado para que la siguiente conexión lo vuelva a anclar silenciosamente.                                                                                                   |
| Forget all                                      | Limpia todos los certificados anclados (con confirmación). La siguiente conexión a cada radio vuelve a anclar silenciosamente.                                                                                                  | Muestra QMessageBox::question antes de borrar.                                                                                                                             |

Cada valor de solo lectura tiene un botón de copia al portapapeles junto a él (un icono pequeño que aparece al pasar el ratón). Haga clic en el botón para copiar el valor.

### Encendido Remoto

Haga clic en **Remote On** para habilitar la funcionalidad de activación remota/encendido remoto.

### Reiniciar Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Un diálogo de confirmación advierte:

- **Conexión LAN:** AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de arrancar.
- **Conexión SmartLink/WAN:** AetherSDR se desconecta. Debe reconectarse manualmente después de que la radio se reinicie.

El botón está deshabilitado cuando la radio está desconectada o reconectándose. Se vuelve a habilitar automáticamente cuando la radio se reconecta.

### Actualización de firmware

**Check for Update** consulta a la radio si hay actualizaciones de firmware disponibles. Cuando se encuentra una versión más reciente, AetherSDR muestra un mensaje informativo:

> Actualización disponible: v*X.Y.Z*
> Descargue el instalador de SmartSDR desde flexradio.com,
> luego haga clic en 'Select Installer...' para prepararlo.

**Select Installer...** (renombrado de Browse .ssdr... en v0.9.3) acepta tres tipos de archivo:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | .msi | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | .exe | Versiones anteriores de SmartSDR |
| Archivo de firmware extraído | .ssdr | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (magia OLE/MSI versus cabecera PE/COFF MZ) y extrae la carga útil .ssdr sin necesidad de herramientas externas.

#### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y cualquier error.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

---

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles (#2976). |

### Configuración de red

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Enforce Private IP Connections | Botón de alternancia | — | — | Rechaza peers que no sean RFC1918. |
| Network MTU | Spinbox | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings. |
| DHCP / Static | Botón de alternancia | — | — | Cambia entre los modos DHCP e IP estática. |
| IP Address / Mask / Gateway | Campo de texto | — | — | Campos de configuración de IP estática. |
| Apply | Botón pulsador | — | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

---

## Pestaña TX

La pestaña TX contiene tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, opciones de seguimiento de slice/TX y un acceso directo a la Configuración de Banda de TX.

### Configuración de Banda de TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos

La sección de tiempos de TX incluye campos spinbox para valores en milisegundos.

| Control | Etiqueta de visualización | Predeterminado | Comportamiento |
|---|---|---|---|
| ACC TX | ACC TX: | — | Retardo de tiempo de ACC en ms. |
| TX Delay | TX Delay: | — | Retardo de TX en ms. |
| RCA TX1 | RCA TX1: | — | Retardo de RCA TX1 en ms. |
| Timeout | Timeout (sec): | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |

### Enclavamientos

Los botones de alternancia **TX REQ: RCA** y **TX REQ: Accessory** habilitan las entradas de enclavamiento RCA y de accesorio.

### Potencia y sintonía

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Max Power | Spinbox | — | 0–100% | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | Cuadro combinado | — | — | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Tipo | Predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Show TX in Waterfall | Botón de alternancia | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Falso | `TxFollowsActiveSlice` | TX sigue al slice activo. Excluyente mutuo con 'Active Slice Follows TX'. Se desactiva automáticamente durante una operación Split. |
| Active Slice Follows TX | Botón pulsador | Falso | `ActiveFollowsTxSlice` | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Excluyente mutuo con 'TX Follows Active Slice'. |

---

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

**Enable/Disable the Level Meter During Receive** alterna la visualización del medidor de nivel de micrófono incluso en RX.

### Manipulador CW

| Control | Tipo | Predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Iambic | Botón de alternancia | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode | Botón pulsador | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. Par excluyente mutuo. |
| Swap | Botón de alternancia | — | — | Intercambia dit/dah. |
| Sideband | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | Botón de alternancia | — | — | Habilita el accionamiento por macros CWX. |
| Decode | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. |

### RTTY

El spinbox **RTTY Mark Default** establece la frecuencia predeterminada de la marca RTTY.

---

## Pestaña RX

La pestaña RX contiene la calibración de desviación de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

| Control | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz) | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb) | Spinbox | Desviación de frecuencia manual en ppb. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** lista las fuentes de oscilador disponibles dinámicamente según el hardware presente y el estado del oscilador informado por la radio.

| Etiqueta | Valor interno | Cuándo se muestra |
|---|---|---|
| Auto | auto | Siempre se muestra |
| TCXO | tcxo | Se muestra cuando hay hardware TCXO presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `tcxo` |
| GPSDO | gpsdo | Se muestra cuando hay hardware GPSDO presente o la configuración actual o guardada es `gpsdo` |
| External 10 MHz | external | Se muestra cuando hay una referencia externa presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `external` |

#### Visualización del estado de bloqueo

La etiqueta de estado de bloqueo junto al cuadro combinado muestra información más rica que texto plano:

| Situación | Texto de ejemplo mostrado |
|---|---|
| Estado del oscilador aún no recibido | `Waiting for oscillator status` |
| El modo Auto se ha resuelto a una fuente | `Auto -> GPSDO Locked` |
| La configuración guardada difiere del estado activo | `TCXO -> GPSDO Locked` |
| La configuración y el estado coinciden | `GPSDO Locked` |
| External seleccionado pero referencia no detectada | `External 10 MHz Unlocked (not detected)` |

El color de la etiqueta se actualiza automáticamente: verde (`#00c040`) cuando está bloqueado, rojo (`#c04040`) cuando está desbloqueado y gris (`#8aa8c0`) mientras espera el estado.

---

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, amplificación, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Line Out | Deslizador | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone | Deslizador | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

**Audio Compression (SmartLink):** alterna entre Auto, Uncompressed y Opus. Clave de configuración: `AudioCompression`.

### Suspensión del sistema

La casilla de verificación **Prevent system sleep while connected** mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Predeterminado: Falso. Clave de configuración: `InhibitSleepWhileConnected`.

### Dispositivos de audio del PC

Los cuadros combinados **PC Audio Devices: Input:** y **Output:** seleccionan los dispositivos de audio de entrada y salida del host.

### Amplificación de audio

El botón de alternancia **Audio
