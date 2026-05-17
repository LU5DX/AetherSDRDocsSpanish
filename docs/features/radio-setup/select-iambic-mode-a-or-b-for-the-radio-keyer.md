# Diálogo de Configuración de Radio

Esta página describe cada control en el diálogo **Configuración de Radio**
(`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior;
cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Modelo** | Modelo de la radio (solo lectura). |
| **Versión HW** | Cadena de versión del hardware (solo lectura). |
| **Región** | Región regulatoria; predeterminada EE. UU. (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Opciones** | Muestra las opciones de radio licenciadas (solo lectura). |
| **Información de Licencia** | Muestra la suscripción, expiración, ID de Radio y versión licenciada de la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Apodo** | Campo de texto | Apodo descriptivo de la radio. |
| **Indicativo** | Campo de texto | Indicativo de la estación. |
| **Nombre de Estación** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Se almacena en `StationName`. Si se deja vacío, usa el nombre de host del sistema operativo. Se envía a la radio como `client station <name>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Encendido Remoto** | Habilita el encendido remoto. |
| **Buscar Actualización** | Consulta las actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado dice: *Actualización disponible: vX.Y.Z — Descargue el instalador de SmartSDR desde flexradio.com, luego haga clic en 'Seleccionar Instalador...' para prepararlo.* Cuando el firmware está actualizado, la etiqueta dice: *El firmware está actualizado (vX.Y.Z).* |
| **Seleccionar Instalador...** | Abre un selector de archivos. Acepta un instalador `.msi` de SmartSDR (formato WiX de FlexRadio v4.2+), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. cabecera MZ de PE/COFF) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado como **Examinar .ssdr...** (cambiado en v0.9.3). |
| **Subir Firmware** | Inicia la subida del firmware. Una barra de progreso y una etiqueta de estado rastrean el progreso. Se habilita solo después de que un archivo válido haya sido preparado por **Seleccionar Instalador...** . |

### Preparar una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Buscar Actualización**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Seleccionar Instalador...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparando firmware desde \<nombre de archivo\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se completa, la etiqueta de estado confirma que está listo y **Subir Firmware** se activa.
5. Haga clic en **Subir Firmware** para transferir el firmware a la radio.

---

## Pestaña Red

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Dirección IP / Máscara / Dirección MAC** | Direcciones de red de solo lectura reportadas por la radio. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Exigir Conexiones IP Privadas:** | Botón de alternancia | — | Rechaza pares que no cumplen con RFC1918. |
| **MTU de Red:** | Spinbox | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango: 576–9000. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en `NetworkMtu`. |
| **DHCP / Estática** | Botón de alternancia | — | Cambia entre modos DHCP e IP Estática. |
| **Dirección IP: / Máscara: / Puerta de Enlace:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Aplicar** | Botón pulsador | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y los datos de posición en vivo cuando hay un receptor GPS conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y número de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, enclavamientos, límites de potencia, modo de sintonía y el comportamiento de seguimiento de franja.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Tiempos (en ms)** | Campos Spinbox | — | Tiempos de retención y retardo de TX. Campos: ACC TX (ms), Retardo TX (ms), RCA TX1 (ms). |
| **Tiempo de Espera (seg):** | Spinbox | — | Tiempo de espera de enclavamiento en segundos. El valor se envía a la radio en milisegundos (multiplicado por 1000). |
| **Enclavamientos - SOL TX: RCA / Accesorio** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Potencia Máx.:** | Spinbox | — | Límite máximo de potencia de TX a nivel de radio (0–100%). |
| **Modo de Sintonía:** | Cuadro combinado | — | Selecciona cómo se comporta el botón de Sintonía. |
| **Mostrar TX en Waterfall:** | Botón de alternancia | — | Dibuja la señal de TX en la visualización del waterfall. |
| **TX Sigue a Franja Activa** | Botón pulsador | Falso | TX sigue a la franja activa. Mutuamente excluyente con **Franja Activa Sigue a TX**. Se desactiva automáticamente durante una operación en Split. Se almacena en `TxFollowsActiveSlice`. |
| **Franja Activa Sigue a TX** | Botón pulsador | Falso | Cambia la franja activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Sigue a Franja Activa**. Se almacena en `ActiveFollowsTxSlice`. |
| **Configuración de Banda de TX** | Botón pulsador | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipador iámbico

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** muestre **Habilitado**. Si muestra **Deshabilitado**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iámbico Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Habilitar/Deshabilitar el Medidor de Nivel Durante Recepción** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Modo Iámbico: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iámbico Curtis A o B tanto para el manipulador hardware de la radio como para el manipulador software local. Modo A = Curtis A; Modo B = Curtis B. Añadido en v0.9.1. |
| **Intercambiar:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Banda Lateral:** | Cuadro combinado | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita la manipulación por macros CWX. |
| **Decodificar:** | Botón de alternancia | Verdadero | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. |
| **Marca RTTY Predeterminada:** | Spinbox | — | Frecuencia de marca RTTY predeterminada. |

**Modo A vs. Modo B:** El Modo A (Curtis A) libera el último elemento cuando ambas paletas se sueltan a mitad de un apretón. El Modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador software local refleja el modo que seleccione, proporcionando una respuesta de tono de monitoreo inferior a 5 ms independiente de la latencia de la red.

---

## Pestaña RX

Proporciona calibración de compensación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo muestra:

- **GPSDO instalado. Calibración manual de compensación de frecuencia disponible.** (verde) — GPSDO presente.
- **Calibración manual de compensación de frecuencia disponible.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en **Frec. Cal. (MHz):**.
4. Haga clic en **Iniciar**.
   - La etiqueta del botón cambia a **Ocupado** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado informa el progreso (Iniciando… y estados posteriores).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se rehabilita y la etiqueta de estado se actualiza con el resultado.
6. Si **Frec. Cal. (MHz):** está vacío cuando hace clic en **Iniciar**, la etiqueta de estado muestra **Introduzca frecuencia de calibración** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Frec. Cal. (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Iniciar. |
| **Iniciar** | Botón pulsador | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y etiqueta como Ocupado durante una calibración activa. |
| **Comp. Frec. (ppb):** | Spinbox | — | Compensación de frecuencia manual en partes por billón. Se aplica directamente sin ejecutar un barrido. |
| **Fuente de Referencia de 10 MHz:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador. El cuadro combinado se llena dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **10 MHz Externo** aparecen solo cuando se detecta el hardware correspondiente o se seleccionó previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Bloqueado** / **Desbloqueado**) se agrega y se actualiza en vivo; si se selecciona **10 MHz Externo** pero no se detecta señal externa, se agrega *(no detectado)*. |

---

## Pestaña Antenas

Configura nombres de antena definidos por el usuario para cada puerto de antena de TX.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campos de texto | — | Introduzca un nombre personalizado (hasta 20 caracteres) para cada puerto de antena. Los nombres se envían a la radio y se muestran en los botones de band-stack y en el selector de antena de la franja. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Salida de Línea:** | Deslizador | — | Ganancia de salida de línea. |
| **Silenciar (Salida de Línea)** | Botón pulsador | — | Silencia la salida de línea. |
| **Auriculares:** | Deslizador | — | Ganancia de auriculares. |
| **Silenciar (Auriculares)** | Botón pulsador | — | Silencia la salida de auriculares. |
| **Altavoz Frontal: / Silenciar** | Botón pulsador | — | Silencia el altavoz frontal (específico del modelo). |
| **Compresión de Audio (SmartLink): Auto / Sin comprimir / Opus** | Botón pulsador | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Se almacena en `AudioCompression`. |
| **Evitar que el sistema duerma mientras está conectado** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante la inactividad. Se almacena en `InhibitSleepWhileConnected`. |
| **Dispositivos de Audio del PC: Entrada: / Salida:** | Cuadro combinado | — | Selecciona los dispositivos de audio de entrada y salida del host. |
| **Refuerzo de Audio:** | Botón de alternancia | — | Habilita ganancia extra en la ruta de audio del cliente. Se almacena en `AudioBoost`. |
| **Búfer de Audio:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para compensación de jitter en VPN/SmartLink. Rango: 50–1000 ms. Se almacena en `AudioBufferMs`. |
| **Grabación: Lado Radio / Lado Cliente** | Botón pulsador | Lado Radio | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. |
| **Guardar en:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo lado cliente). La carpeta predeterminada es Documentos/AetherSDR/Grabaciones. Se almacena en `QsoRecordingDir`. |
| **...** | Botón pulsador | — | Examina para seleccionar la carpeta de grabación. |
| **Grabación automática al TX** | Casilla de verificación | Falso | Graba automáticamente mientras transmite. Se almacena en `QsoRecordingAutoRecord`. |
| **Tiempo de espera por inactividad:** | Spinbox | 120 | Segundos de silencio antes de que se detenga la grabación. Rango: 10–3600 seg. Se almacena en `QsoRecordingIdleTimeout`. |
| **NVIDIA B
