# Resumen de Configuración de Radio

El diálogo de Configuración de Radio es la ventana central de configuración para su FLEX-8600. Reúne en un solo lugar la identificación de la radio, red, GPS, transmisión, audio, filtros, transverters, cables USB, periféricos, nombres de antenas, temas de color de slices, configuración del muestreador APD, gestión de certificados SmartLink y ajustes seriales FlexControl. Ábralo siempre que necesite cambiar algo sobre cómo AetherSDR interactúa con su hardware de radio.

## Antes de comenzar

- La radio debe estar conectada. La Configuración de Radio requiere una conexión de radio activa.

## Cómo funciona

Abra Configuración de Radio desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área distinta de configuración. Las pestañas distintas de Radio cargan su contenido la primera vez que hace clic en ellas.

El diálogo recuerda su tamaño y posición entre sesiones mediante `PersistentDialog`. Una barra de título con el texto "Radio Setup" aparece en la parte superior. Puede arrastrar la barra de título para mover el diálogo.

También puede saltar directamente a pestañas específicas:

- `Settings > USB Cables...` abre Configuración de Radio con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Configuración de Radio con la pestaña **Serial** activa (solo disponible cuando el soporte de puerto serial está integrado).

### Comportamiento de desplazamiento de pestañas

Las pestañas cuyo contenido puede exceder la altura visible del diálogo en pantallas pequeñas o de alta densidad de píxeles (Radio, Audio, Filters, Themes, Peripherals, SmartLink) incrustan automáticamente un área de desplazamiento vertical. La barra de desplazamiento solo aparece cuando es necesaria; los usuarios con pantallas anchas no ven ningún cambio visual.

### Pestañas de un vistazo

| Pestaña | Qué configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones licenciadas, apodo, indicativo, nombre de estación, información de licencia, actualización de firmware y reinicio de radio. |
| **Network** | Dirección IP (DHCP o estática), MTU de red, aplicación de IP privada y el puente opcional Agent Automation (MCP). |
| **GPS** | Estado GPS en vivo: latitud, longitud, altitud, hora y número de satélites. |
| **TX** | Temporizaciones de TX hang/delay, interbloqueos, límite global de potencia, modo de sintonía, visualización TX en waterfall, comportamiento TX/slice de seguimiento y un acceso directo a configuraciones por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, keyer iambic (modo A/B, intercambio, banda lateral), CWX, decodificador CW y valor predeterminado de marca RTTY. |
| **RX** | Calibración de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Calibration** | Calibración manual de frecuencia del lado del host para radios que no pueden calibrarse a sí mismas. Solo visible en backends que reportan la capacidad `hostFrequencyCalibration` (p. ej., HL2). |
| **Antennas** | Muestra y renombra los puertos de antena (ANT1, ANT2, XVTA, XVTB) según los reconoce la radio. |
| **Audio** | Niveles de línea de salida, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio de PC; refuerzo de audio; tamaño de búfer de audio; modo de grabación, carpeta, auto-grabación en TX y tiempo de espera de inactividad; control de contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia vs. nítido por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transverter; crear o eliminar entradas de transverter. |
| **APD** | Configuración del muestreador externo de Pre-Distorsión Adaptativa — selección de puerto de retroalimentación por antena TX y reinicio de ecualizador. Visible solo en radios FLEX-8x00 que reportan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asigna adaptadores seriales USB a los tipos de cable CAT, BCD, bit y PTT y configura sus parámetros seriales. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius, ShackSwitch y amplificadores ACOM. |
| **KiwiSDR** | Gestión de receptores públicos KiwiSDR — agregar, eliminar, explorar y configurar hasta 10 receptores públicos. |
| **Themes** | Esquema de colores de slices: cambiar entre la paleta integrada de AetherSDR y colores personalizados por slice (A–H). |
| **Serial** | Selección de puerto serial FlexControl, parámetros de línea, asignaciones de función de pines (DTR/RTS), intercambio de paddles, auto-apertura y detección de perilla de sintonía. (Visible solo cuando el soporte de puerto serial está integrado). |
| **SmartLink** | Gestión de certificados TLS fijados — lista cada certificado fijado con botones Forget y Forget All. |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistidas o comportamientos notables.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Radio SN** | Radio | Número de serie del chasis (solo lectura). Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. |
| **HW Version** | Radio | Cadena de versión de hardware (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **Options** | Radio | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **Model** | Radio | Modelo de radio (solo lectura). Incluye un botón de copiar al portapapeles junto al valor. |
| **License Info (Subscription / Expiration / Radio ID / Licensed version)** | Radio | Muestra los detalles de licencia de la radio. Cada campo incluye un botón de copiar al portapapeles junto al valor. |
| **IP Address / Mask / MAC Address** | Network | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |
| **Station Name** | Radio | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Se establece al nombre de host del SO si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <nombre>`. |
| **Select Installer...** | Radio | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autocontenido más antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v26.5.3. |
| **Reboot Radio** | Radio | Envía un comando de reinicio a la radio. Primero aparece un diálogo de confirmación. En conexiones LAN, AetherSDR se reconecta automáticamente una vez que la radio termina de iniciar. En conexiones SmartLink/WAN debe reconectarse manualmente. El botón está deshabilitado cuando la radio está desconectada y también cuando el backend no admite reinicio del cliente (p. ej., HL2 es solo RX). |
| **Network MTU:** | Network | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576–9000). El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **Enforce Private IP Connections:** | Network | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. |
| **Agent Automation (MCP):** | Network | Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (a través del servidor MCP) pueda inspeccionar y manejar la aplicación en ejecución. Desactivado por defecto; el operador opta por activarlo. Nuevo en v26.8.4 (#3646). Se conserva mediante `AutomationBridgeSettings`. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de esta alternancia y deshabilita el control en la interfaz. El pulsado de transmisión permanece bloqueado a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`. |
| **Access Token:** | Network | Visualización de solo lectura del token de acceso MCP. Péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén de secretos del SO. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. El marcador `(cargando…)` aparece hasta que se lea el llavero. |
| **Copy (Access Token)** | Network | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| **Rotate (Access Token)** | Network | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | Network | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera habilitación muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por `AETHER_AUTOMATION_ALLOW_TX` (forzado a activado) y `AETHER_AUTOMATION_NO_TX` (fijado a desactivado). Un temporizador de vigilancia de desactivación forzada limita el TX originado por el puente. |
| **Observe only: Read-only (block all driving)** | Network | Hace que el puente sea solo de observación: los clientes MCP pueden leer el estado, pero cada verbo mutador (set/invoke/connect/tune/capture) se rechaza. Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija activado para ejecuciones sin interfaz/CI. |
| **VITA-49 RX buffer:** | Network | Control deslizante con valores preestablecidos que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes. Nuevo en v26.8.4 (#3810). Preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a `net.core.rmem_max`; una etiqueta en vivo "granted: <tamaño>" muestra lo que el kernel realmente concedió. |
| **granted: (VITA-49 RX buffer)** | Network | Muestra el tamaño de búfer que el kernel realmente concedió (en comparación con el preestablecido solicitado). Nuevo en v26.8.4. Muestra "(applies on connect)" cuando no hay una conexión activa. |
| **TX Follows Active Slice** | TX | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic:** | Phone/CW | Habilita o deshabilita el keyer iambic en la radio. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Decode: RX** | Phone/CW | Habilita la superposición de decodificación CW en el panadapter para CW recibido. Se almacena como `CwDecoder` (JSON anidado, campo `rx`). Separado de la alternancia única heredada en v26.5.3. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. Predeterminado: habilitado. |
| **Decode: TX** | Phone/CW | Decodifica el pulsado CW propio del operador mediante tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Se almacena como `CwDecoder` (JSON anidado, campo `tx`). Nuevo en v26.5.3 (#2417). Predeterminado: deshabilitado. |
| **10 MHz Reference Source:** | RX | Selecciona la fuente de referencia del oscilador. El cuadro combinado se llena dinámicamente: Auto siempre está presente; TCXO, GPSDO y External 10 MHz aparecen según lo que la radio reporte como instalado o actualmente activo. Si la radio envía `ext` para el ajuste o estado del oscilador, AetherSDR lo normaliza a `external` antes de mostrarlo. Cuando el ajuste es Auto y la radio ha seleccionado una fuente específica, la etiqueta muestra la resolución (por ejemplo, "Auto -> GPSDO"). El estado de bloqueo (Locked / Unlocked) se muestra en verde o rojo junto al cuadro combinado y se actualiza en vivo. Si se selecciona External 10 MHz pero no se detecta una referencia externa, se agrega "(not detected)" al texto de estado. |
| **Calibration (tab)** | Calibration | Calibración manual de frecuencia del lado del host para radios que no pueden calibrarse a sí mismas. Solo visible en backends que reportan la capacidad `hostFrequencyCalibration` (p. ej., HL2). La página está oculta en radios FLEX, que
