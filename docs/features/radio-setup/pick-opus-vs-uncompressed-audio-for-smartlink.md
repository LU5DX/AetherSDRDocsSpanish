# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, APD, temas, serial (FlexControl), nombres de antenas, gestión de certificados anclados SmartLink y acceso a receptores públicos KiwiSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio para acceder a la mayoría de las pestañas.
- Abra `Settings > Radio Setup...`.

## Pestaña Radio

La pestaña Radio muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

| Control | Predeterminado | Comportamiento |
|---------|----------|----------|
| Radio SN | Número de serie del chasis (solo lectura). | Incluye un botón de copiar al portapapeles (ícono de bandeja) junto al valor. Nuevo en v26.5.3 (#2976). |
| Region | USA | Región regulatoria de la radio. |
| HW Version | Cadena de versión de hardware. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| Remote On | — | Habilita el encendido remoto / remote-on. |
| Options | Muestra las opciones de radio licenciadas. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| FlexControl | — | Estado detectado del hardware FlexControl. |
| multiFLEX | — | Estado habilitado de multiFLEX. |
| Model | Modelo de la radio. | Incluye un botón de copiar al portapapeles junto al valor (#2976). |
| Nickname | — | Apodo amigable de la radio. |
| Callsign | — | Indicativo de la estación. |
| Station Name | — | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Se usa el nombre de host del sistema operativo si está vacío. Se almacena como `StationName`. |
| License Info | — | Muestra los detalles de la licencia de la radio (Suscripción / Expiración / ID de Radio / Versión licenciada). Haga clic en el botón de copiar para copiar al portapapeles. |
| Check for Update | — | Consulta actualizaciones de firmware. |
| Select Installer... | — | Elige un archivo de imagen de firmware (`.msi`, `.exe` o `.ssdr`). |
| Upload Firmware | — | Inicia la carga del firmware con barra de progreso y estado. |
| Reboot Radio | — | Solicita confirmación y luego reinicia la radio conectada. AetherSDR se desconecta durante el reinicio. Se reconecta automáticamente en LAN; SmartLink/WAN requiere reconexión manual. El botón está deshabilitado cuando la radio no está conectada o cuando el backend no admite el reinicio del cliente (p. ej., HL2 es solo RX). Nuevo en v26.8.4 (#4448). |
| Agent Automation (MCP) | — | Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por activarlo. Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la activación del puente independientemente de esta opción y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token | — | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | Copia el token de acceso al portapapeles. | Nuevo en v26.8.4. |
| Rotate (Access Token) | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. | Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero se rechaza todo verbo mutador (set/invoke/connect/tune/capture). | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer | — | Control deslizante de ajuste a valores preestablecidos que configura el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas del panadapter/waterfall para que no se descarten paquetes. | Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | Muestra el tamaño de búfer que el kernel realmente concedió (en comparación con el valor preestablecido solicitado). | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay una conexión activa. |

### Botones de copiar valor

Cada indicador de solo lectura (Radio SN, HW Version, License Info, etc.) ahora muestra un pequeño botón de copiar superpuesto al pasar el cursor o al enfocar. Al hacer clic en el botón se copia el valor mostrado al portapapeles del sistema. Aparece una breve ventana emergente "copied" cerca del botón después de una copia exitosa.

### Estado de carga del firmware

El área de carga de firmware muestra una barra de progreso y texto de estado durante una carga activa. Cuando no hay una carga en curso, el área de estado está vacía.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación antes de que continúe el reinicio. AetherSDR se desconecta durante el reinicio:

- **Conexión LAN:** AetherSDR se reconecta automáticamente una vez que la radio termina de iniciar.
- **Conexión SmartLink/WAN:** Debe reconectarse manualmente después de que la radio inicie.

El botón está habilitado solo cuando la radio está conectada y el backend admite un reinicio iniciado por el cliente. Por ejemplo, el botón está deshabilitado en radios HL2 porque son de solo recepción. El botón se actualiza automáticamente cuando cambia el estado de la conexión, por lo que no necesita reabrir el diálogo.

## Pestaña Red

La pestaña Red muestra información de red de la radio y opciones de red avanzadas.

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| IP Address / Mask / MAC Address | — | Direcciones de red de solo lectura. Cada una incluye un botón de copiar al portapapeles. |
| Enforce Private IP Connections | — | Rechaza pares que no sean RFC1918. |
| Agent Automation (MCP) | Disabled | Habilita el puente de automatización en la aplicación para que un asistente de codificación de IA (mediante el servidor MCP) pueda inspeccionar y controlar la aplicación en ejecución. Desactivado por defecto; el operador opta por activarlo. Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento AETHER_AUTOMATION fuerza la activación del puente independientemente de esta opción y deshabilita el control en la interfaz. La activación de transmisión permanece bloqueada a menos que se establezca AETHER_AUTOMATION_ALLOW_TX. |
| Access Token | (none) | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno AETHER_MCP_TOKEN del asistente. Se almacena en el almacén de secretos del sistema operativo. Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero. |
| Copy (Access Token) | — | Copia el token de acceso al portapapeles. Nuevo en v26.8.4. |
| Rotate (Access Token) | — | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior. Nuevo en v26.8.4. |
| Allow TX via MCP: Enable transmit control | False | Permite que un cliente MCP active el transmisor (MOX/PTT/TUNE/ATU/CWX). Desactivado por defecto; la primera activación muestra una confirmación de responsabilidad del operador. Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Anulado por AETHER_AUTOMATION_ALLOW_TX (forzado a activado) y AETHER_AUTOMATION_NO_TX (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| Observe only: Read-only (block all driving) | False | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero se rechaza todo verbo mutador (set/invoke/connect/tune/capture). Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento AETHER_AUTOMATION_READONLY lo fija en activado para ejecuciones headless/CI. |
| VITA-49 RX buffer | 4 MB | Control deslizante de ajuste a valores preestablecidos que configura el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas del panadapter/waterfall para que no se descarten paquetes. Nuevo en v26.8.4 (#3810). Valores preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a net.core.rmem_max; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| granted: (VITA-49 RX buffer) | — | Muestra el tamaño de búfer que el kernel realmente concedió (en comparación con el valor preestablecido solicitado). Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay una conexión activa. |
| Network MTU | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576–9000). Se almacena como `NetworkMtu`. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| DHCP / Static | — | Cambia entre modos de IP dinámica (DHCP) e IP estática. |
| IP Address / Mask / Gateway | — | Campos de configuración de IP estática. |
| Apply | — | Envía la configuración de red a la radio. |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña TX configura tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuraciones de banda de TX.

| Control | Predeterminado | Rango Válido | Comportamiento |
|---------|---------|-------------|----------|
| TX Band Settings | — | — | Abre el diálogo dedicado de potencia/sintonía por banda. |
| ACC TX | — | — | Retardo de mantenimiento de TX en milisegundos. |
| TX Delay | — | — | Retardo de TX en milisegundos. |
| RCA TX1 | — | — | Retardo de RCA TX1 en milisegundos. |
| Timeout (sec) | — | — | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |
| RCA TX2 | — | — | Retardo de RCA TX2 en milisegundos. |
| Interlocks - TX REQ: RCA / Accessory | — | — | Habilita las entradas de enclavamiento RCA y de accesorios. |
| Max Power | — | 0–100 % | Establece el límite de potencia de TX a nivel de radio. |
| Tune Mode | — | — | Selecciona cómo se comporta el botón de sintonía. |
| Show TX in Waterfall | — | — | Dibuja la señal de TX en el waterfall. |
| TX Follows Active Slice | False | — | TX sigue a la slice activa. Mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | False | — | Cambia la slice activa cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de tiempo

Los campos de tiempo en la pestaña TX aceptan valores en milisegundos, excepto Timeout (sec) que muestra y acepta valores en segundos para facilitar la lectura. La radio almacena el valor de tiempo de espera internamente en milisegundos.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Predeterminado | Rango Válido | Comportamiento |
|---------|---------|-------------|----------|
| Enable/Disable the Level Meter During Receive | — | — | Muestra el medidor de nivel de micrófono incluso en RX. |
| Iambic | — | Enabled / Disabled | Habilita o deshabilita el manipulador iambic en la radio. |
| Iambic Mode: A / B | A | A / B | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. |
| Swap | — | — | Intercambia dit/dah. |
| Sideband | — | LSB / USB | Selecciona la banda lateral del tono de CW. |
| CWX | — | — | Habilita el teclado de macros CWX. |
| Decode: RX | True | — | Habilita la superposición de decodificación CW en el panadapter para la CW recibida. Se persiste como un blob JSON anidado bajo `CwDecoder` con campos rx y tx. La clave heredada `CwDecodeOverlay` se migra automáticamente en la primera lectura. |
| Decode: TX | False | — | Decodifica la propia manipulación CW del operador mediante el tono lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paddle/bug. Nuevo en v26.5.3 (#2417). |
| RTTY Mark Default | — | — | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña RX proporciona calibración de compensación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

| Control | Predeterminado | Rango Válido | Comportamiento |
|---------|---------|-------------|----------|
| Cal Frequency (MHz) | — | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start
