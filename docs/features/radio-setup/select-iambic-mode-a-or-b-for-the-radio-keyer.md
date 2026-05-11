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
| **Versión HW** | Cadena de versión de hardware (solo lectura). |
| **Región** | Región regulatoria; predeterminado EE. UU. (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). |
| **Opciones** | Muestra las opciones de radio licenciadas (solo lectura). |
| **Información de Licencia** | Muestra suscripción, fecha de vencimiento, ID de radio y versión licenciada de la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Apodo** | Campo de texto | Apodo de radio fácil de usar. |
| **Indicativo** | Campo de texto | Indicativo de la estación. |
| **Nombre de Estación** | Campo de texto | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Almacenado en `StationName`. Se establece de forma predeterminada en el nombre de host del sistema operativo si se deja vacío. Se envía a la radio como `client station <name>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Encendido Remoto** | Habilita activación remota / encendido remoto. |
| **Buscar Actualización** | Consulta actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado muestra: *Actualización disponible: vX.Y.Z — Descargue el instalador de SmartSDR desde flexradio.com, luego haga clic en 'Seleccionar Instalador...' para prepararlo.* Cuando el firmware está actualizado, la etiqueta muestra: *El firmware está actualizado (vX.Y.Z).* |
| **Seleccionar Instalador...** | Abre un selector de archivos. Acepta un instalador `.msi` de SmartSDR (formato WiX de FlexRadio v4.2+), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` pre-extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (mágico OLE/MSI vs. cabecera MZ PE/COFF) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado como **Buscar .ssdr...** (cambiado en v0.9.3). |
| **Subir Firmware** | Inicia la subida de firmware. Una barra de progreso y una etiqueta de estado realizan el seguimiento del progreso. Habilitado solo después de que un archivo válido haya sido preparado por **Seleccionar Instalador...**. |

### Preparación de una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Buscar Actualización**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Seleccionar Instalador...** y seleccione el archivo descargado `.msi`, `.exe` o `.ssdr`.
   - La etiqueta de estado muestra *Preparando firmware desde <nombre_de_archivo>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se completa, la etiqueta de estado confirma que está listo y **Subir Firmware** se activa.
5. Haga clic en **Subir Firmware** para transferir el firmware a la radio.

---

## Pestaña Red

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Dirección IP / Máscara / Dirección MAC** | Direcciones de red de solo lectura informadas por la radio. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Exigir Conexiones IP Privadas:** | Botón de alternancia | — | Rechaza pares que no sean RFC1918. |
| **MTU de Red:** | Control de número | 1450 | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes. Rango: 576–9000 bytes. Almacenado en `NetworkMtu`. |
| **DHCP / Estática** | Botón de alternancia | — | Cambia entre modos DHCP e IP Estática. |
| **Dirección IP: / Máscara: / Puerta de Enlace:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Aplicar** | Botón de pulsación | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando un receptor GPS está conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y conteo de satélites. Actualizado en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, enclavamientos, límites de potencia, modo de sintonía y comportamiento de seguimiento de segmento.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Tiempos (en ms)** | Control de número | — | Tiempos de espera y retardo de TX en milisegundos. |
| **Enclavamientos - TX REQ: RCA / Accesorio** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Potencia Máx:** | Control de número | — | Límite de potencia TX a nivel de radio (0–100%). |
| **Modo Sintonía:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Sintonizar. |
| **Mostrar TX en Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en la visualización waterfall. |
| **TX Sigue al Segmento Activo** | Botón de pulsación | Falso | TX sigue al segmento activo. Mutuamente excluyente con **El Segmento Activo Sigue a TX**. Se desactiva automáticamente durante la operación en Split. Almacenado en `TxFollowsActiveSlice`. |
| **El Segmento Activo Sigue a TX** | Botón de pulsación | Falso | Cambia el segmento activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Sigue al Segmento Activo**. Almacenado en `ActiveFollowsTxSlice`. |
| **Configuración de Banda TX** | Botón de pulsación | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iámbico

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iámbico:** muestra **Habilitado**. Si muestra **Deshabilitado**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iámbico Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Habilitar/Deshabilitar el Medidor de Nivel Durante la Recepción** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iámbico:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Modo Iámbico: A / B** | Botón de pulsación (par mutuamente excluyente) | A | Selecciona el modo iámbico Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. Añadido en v0.9.1. |
| **Intercambiar:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Banda Lateral:** | Cuadro combinado | — | Selecciona la banda lateral de tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita la activación por macros CWX. |
| **Decodificar:** | Botón de alternancia | Verdadero | Habilita la superposición de decodificación CW en el panadapter. Almacenado en `CwDecodeOverlay`. |
| **Marca RTTY Predeterminada:** | Control de número | — | Frecuencia de marca RTTY predeterminada. |

**Modo A vs. Modo B:** El Modo A (Curtis A) libera el último elemento cuando ambas paletas se sueltan en medio de una pulsación simultánea. El Modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando una respuesta de tono lateral inferior a 5 ms independiente de la latencia de la red.

---

## Pestaña RX

Proporciona calibración de desplazamiento de frecuencia del GPSDO y selección de fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración estuvieron disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo muestra:

- **GPSDO instalado. Calibración manual de desplazamiento de frecuencia disponible.** (verde) — GPSDO presente.
- **Calibración manual de desplazamiento de frecuencia disponible.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Frec. Cal (MHz):**.
4. Haga clic en **Iniciar**.
   - La etiqueta del botón cambia a **Ocupado** y se deshabilita mientras la calibración se ejecuta.
   - La etiqueta de estado informa el progreso (Iniciando… y estados posteriores).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.
6. Si **Frec. Cal (MHz):** está vacío cuando hace clic en **Iniciar**, la etiqueta de estado muestra **Ingrese frecuencia de cal** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Frec. Cal (MHz):** | Control de número | — | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en Iniciar. |
| **Iniciar** | Botón de pulsación | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Deshabilitado y etiquetado como Ocupado durante una calibración activa. |
| **Despl. Frec. (ppb):** | Control de número | — | Desplazamiento de frecuencia manual en partes por billón. Se aplica directamente sin ejecutar un barrido. |
| **Fuente de Referencia de 10 MHz:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador. El cuadro combinado se llena dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **10 MHz Externo** aparecen solo cuando se detecta el hardware correspondiente o se seleccionó previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Bloqueado** / **Desbloqueado**) se agrega y se actualiza en vivo; si **10 MHz Externo** está seleccionado pero no se detecta señal externa, se agrega *(no detectado)*. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Salida de Línea:** | Control deslizante | — | Ganancia de salida de línea. |
| **Silenciar (Salida de Línea)** | Botón de pulsación | — | Silencia la salida de línea. |
| **Auriculares:** | Control deslizante | — | Ganancia de auriculares. |
| **Silenciar (Auriculares)** | Botón de pulsación | — | Silencia la salida de auriculares. |
| **Altavoz Frontal: / Silenciar** | Botón de pulsación | — | Silencia el altavoz frontal (específico del modelo). |
| **Compresión de Audio (SmartLink): Auto / Sin comprimir / Opus** | Botón de pulsación | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Almacenado en `AudioCompression`. |
| **Evitar que el sistema duerma mientras está conectado** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar pérdidas de flujo de audio/TCP/UDP durante la inactividad. Almacenado en `InhibitSleepWhileConnected`. |
| **Dispositivos de Audio del PC: Entrada: / Salida:** | Cuadro combinado | — | Elige los dispositivos de audio de entrada y salida del host. |
| **Mejora de Audio:** | Botón de alternancia | — | Habilita ganancia adicional en la ruta de audio del cliente. Almacenado en `AudioBoost`. |
| **Búfer de Audio:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para compensación de fluctuación en VPN/SmartLink. Rango: 50–1000 ms. Almacenado en `AudioBufferMs`. |
| **Grabación: Lado de la Radio / Lado del Cliente** | Botón de pulsación | Lado de la Radio | Selecciona grabación del lado de la radio o del lado del cliente. Almacenado en `RecordingMode`. |
| **Guardar en:** | Campo de texto | — | Carpeta para grabaciones guardadas (solo lado del cliente). Se establece de forma predeterminada en Documentos/AetherSDR/Grabaciones. Almacenado en `QsoRecordingDir`. |
| **...** | Botón de pulsación | — | Navega por la carpeta de grabación. |
| **Grabación automática en TX** | Casilla de verificación | Falso | Graba automáticamente mientras transmite. Almacenado en `QsoRecordingAutoRecord`. |
| **Tiempo de espera de inactividad:** | Control de número | 120 | Segundos de silencio antes de que la grabación se detenga. Rango: 10–3600 seg. Almacenado en `QsoRecordingIdleTimeout`. |
| **NVIDIA BNR: Iniciar Contenedor Automáticamente / Iniciar / Detener / Verificar Estado** | Botones de pulsación | — | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de estado muestra Ejecutando (verde), Detenido (rojo) o Desconocido (gris). |

---

## Pestaña Filtros

Configura opciones de filtro de baja latencia o nítidos por modo de ancho de banda.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Controles deslizantes de nitidez de filtro Voz / CW / Digital** | Control deslizante | — | Establece la nitidez del filtro (0=mínima latencia a
