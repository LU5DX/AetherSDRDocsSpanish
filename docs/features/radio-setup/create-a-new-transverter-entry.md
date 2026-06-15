# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona controles para información de la radio, red, GPS, TX, antenas, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, puerto serie (FlexControl), APD, Temas y gestión de certificados anclados de SmartLink.

## Cómo abrir el diálogo

1. Seleccione `Settings > Radio Setup...` en el menú principal.
2. El diálogo se abre como una ventana persistente que recuerda su posición y tamaño entre sesiones. Puede arrastrarla por la barra de título.
3. Cierre el diálogo haciendo clic en el botón **X** de la barra de título o presionando `Escape`.

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, información de licencia y controles de actualización de firmware. El contenido de la pestaña está envuelto en un área desplazable para que todos los controles permanezcan accesibles en pantallas pequeñas o de alta densidad de píxeles (high-DPI).

### Información de la radio (solo lectura)

Cada campo de solo lectura incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor del campo al portapapeles del sistema. Una breve ventana emergente "¡Copiado!" confirma la acción.

| Control | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copia para copiar. |
| **Region** | Región normativa de la radio. |
| **HW Version** | Versión del hardware. Haga clic en el botón de copia para copiar. |
| **Model** | Modelo de la radio. |
| **Options** | Muestra las opciones de radio bajo licencia. Haga clic en el botón de copia para copiar. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado de multiFLEX habilitado. |
| **License Info** | Muestra suscripción, fecha de vencimiento, ID de la radio (haga clic en el botón de copia para copiar) y detalles de la versión licenciada. |

### Campos de identificación

| Control | Comportamiento |
|---|---|
| **Nickname** | Apodo de la radio fácil de usar. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. Se almacena en la configuración `StationName`. Se envía a la radio como "client station <nombre>". |

### Remote On (Encendido remoto)

Haga clic en **Remote On** para habilitar la activación remota (wake remoto / encendido remoto).

### Reboot Radio (Reiniciar la radio)

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparecerá un diálogo de confirmación antes de que se realice el reinicio.

- **En una conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de iniciar.
- **En una conexión SmartLink/WAN**: AetherSDR se desconecta. Deberá reconectarse manualmente después de que la radio termine de iniciar.

El botón está deshabilitado cuando la radio está desconectada. Se vuelve a habilitar automáticamente cuando la radio se reconecta, sin necesidad de volver a abrir el diálogo.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar al servidor de actualizaciones de FlexRadio sobre las versiones de firmware disponibles.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que debe descargar el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` previamente extraído. El stagista detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación (staging).
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio.

## Pestaña Network (Red)

La pestaña **Network** muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red (solo lectura)

| Control | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada campo incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor al portapapeles del sistema. |

### Configuración de red

| Control | Valor por defecto | Rango | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** (Forzar conexiones IP privadas) | Desactivado | - | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en la configuración `NetworkMtu`. |
| **DHCP / Static** | DHCP | - | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | - | - | Campos de configuración de IP estática (se muestran cuando se selecciona el modo Static). |
| **Apply** (Aplicar) | - | - | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** controla los tiempos de TX, enclavamientos (interlocks), potencia máxima, modo de sintonía (tune), visualización en el waterfall, seguimiento de slice/TX y proporciona un acceso directo a la configuración de banda de TX (TX Band Settings).

### TX Band Settings (Configuración de banda de TX)

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones de TX

| Control | Valor por defecto | Rango | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** (Temporizaciones en ms) | - | - | Tiempos de espera/retardo de TX. |

### Otros controles de TX

| Control | Valor por defecto | Rango | Comportamiento |
|---|---|---|---|
| **Interlocks - TX REQ: RCA / Accessory** (Enclavamientos - Solicitud TX) | Desactivado | - | Habilita las entradas de enclavamiento RCA y Accessory. |
| **Max Power:** (Potencia máxima) | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** (Modo de sintonía) | - | - | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** (Mostrar TX en el waterfall) | Desactivado | - | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | Falso | - | El TX sigue al slice activo. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. Se almacena en la configuración `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Falso | - | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. Se almacena en la configuración `ActiveFollowsTxSlice`. |

## Pestaña Antennas (Antenas)

La pestaña **Antennas** le permite asignar nombres personalizados a cada puerto de antena de la radio. Esta pestaña se construye de forma diferida (lazy) cuando se hace clic por primera vez.

### Campos de nombre de antena

| Control | Comportamiento |
|---|---|
| **ANT1 - ANT8** | Campos de texto para asignar nombres fáciles de usar a cada puerto de antena. Los nombres se almacenan en la radio. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW (keyer) y los valores predeterminados de RTTY.

### Medidor de audio

| Control | Comportamiento |
|---|---|
| **Enable/Disable the Level Meter During Receive** (Habilitar/Deshabilitar el medidor de nivel durante la recepción) | Muestra el medidor de nivel del micrófono incluso en RX. |

### Manipulador CW (CW keyer)

| Control | Valor por defecto | Rango | Comportamiento |
|---|---|---|---|
| **Iambic:** | Deshabilitado | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | Desactivado | - | Intercambia dit/dah. |
| **Sideband:** | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Desactivado | - | Habilita la activación de macros CWX. |
| **Decode:** | Verdadero | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena en la configuración `CwDecodeOverlay`. |

### RTTY

| Control | Comportamiento |
|---|---|
| **RTTY Mark Default:** (Frecuencia de marca RTTY predeterminada) | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** proporciona la calibración del offset de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo indica:
- **GPSDO instalado. Calibración manual de offset de frecuencia disponible.** (verde) — GPSDO presente.
- **Calibración manual de offset de frecuencia disponible.** (ámbar) — sin GPSDO.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** (Frecuencia de calibración) | Introduzca la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** (Iniciar) | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** (Ocupado) mientras el barrido está en curso. |
| **Freq Offset (ppb):** (Offset de frecuencia en ppb) | Offset de frecuencia manual en partes por billón (ppb). Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de la calibración: Iniciando, texto de progreso o error. Se actualiza en vivo durante el barrido. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** (Fuente de referencia de 10 MHz) selecciona qué oscilador utiliza la radio como referencia de frecuencia.

#### Población del cuadro combinado

El cuadro combinado se llena dinámicamente según lo que informa la radio. Los elementos aparecen de acuerdo con las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando la radio ha informado algún estado del oscilador, cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando la radio ha informado algún estado del oscilador, cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual de la radio. Si ese valor no está en la lista, el cuadro combinado recurre a la selección actual y luego a **Auto**.

#### Etiqueta de estado de bloqueo

La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador y la condición de bloqueo.

| Condición | Texto de la etiqueta | Color |
|---|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status (Esperando estado del oscilador) | Gris |
| La configuración es Auto, la radio ha seleccionado una fuente | Auto -> <fuente> Locked / Unlocked (Bloqueado / Desbloqueado) | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración difiere del estado activo | <configuración> -> <activo> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración coincide con el estado activo | <fuente> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| External seleccionado pero no se detecta señal externa | <texto> (not detected) (no detectado) añadido | Verde (bloqueado) / Rojo (desbloqueado) |

La radio envía `ext` para la fuente externa en algunas respuestas de firmware. AetherSDR normaliza esto a `external` antes de mostrarlo, por lo que la etiqueta siempre muestra **External 10 MHz** en lugar de **Ext**.

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo (boost), búfer, grabación y el contenedor NVIDIA BNR. El contenido de la pestaña está envuelto en un área desplazable para que todos los controles permanezcan accesibles en pantallas pequeñas o de alta densidad de píxeles.

### Salidas de la radio

| Control | Comportamiento |
|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. |
| **Mute (Line Out)** (Silenciar) | Silencia la salida de línea. |
| **Headphone:** | Deslizador de ganancia de auriculares. |
| **Mute (Headphone)** (Silenciar) | Silencia los auriculares. |
| **Front Speaker: / Mute** (Altavoz frontal / Silenciar) | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Valor por defecto | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** (Compresión de audio) | Auto | Selecciona el códec de audio para SmartLink/LAN. Se almacena en la configuración `AudioCompression`. |

### Gestión de energía

| Control | Valor por defecto | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** (Evitar que el sistema duerma mientras esté conectado) | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena en la configuración `InhibitSleepWhileConnected`. |

### Dispositivos de audio del PC

| Control | Comportamiento |
|---|---|
| **PC Audio Devices: Input: (Entrada) / Output: (Salida)** | Selecciona los dispositivos de audio de entrada/salida del host. |

### Refuerzo de audio y búfer

| Control | Valor por defecto | Rango | Comportamiento |
|---|---|---|---|
| **Audio Boost:** (Refuerzo de audio) | Desactivado | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en la configuración `AudioBoost`. |
| **Audio Buffer:** (Búfer
