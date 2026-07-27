# Configurar configuración de radio

El diálogo **Configuración de radio** (`Ajustes > Configuración de radio...`) proporciona la configuración maestra por radio con secciones de pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, transverters, cables USB, periféricos, predistorsión adaptativa, temas, certificados anclados de SmartLink, configuración de puerto serie, navegación de receptores públicos KiwiSDR, parámetros de búsqueda de indicativos, configuración del amplificador (Acom) y parámetros de Automation Bridge.

## Antes de comenzar

- La radio debe estar conectada antes de que la mayoría de las pestañas muestren información en vivo.
- Algunas pestañas (APD, Temas, SmartLink, Serie, KiwiSDR, Búsqueda de indicativo, Acom, Automation Bridge) se construyen de forma diferida y solo aparecen al hacer clic en ellas por primera vez.
- AetherSDR usa una clase base `PersistentDialog` que guarda y restaura la geometría de la ventana automáticamente.

## Pasos para abrir

1. Haga clic en **Ajustes > Configuración de radio...** en el menú principal.
2. El diálogo se abre mostrando la pestaña **Radio** de forma predeterminada.
3. Haga clic en cualquier pestaña para acceder a su configuración.

---

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Lectura de información de la radio

- **Radio SN** — Número de serie del chasis (solo lectura). Muestra el número de serie del chasis si está disponible, de lo contrario, el número de serie de la radio. Incluye un botón de copia al portapapeles junto al valor.
- **Región** — Región regulatoria de la radio (solo lectura).
- **HW Version** — Cadena de versión de hardware (solo lectura). Incluye un botón de copia al portapapeles junto al valor.
- **Modelo** — Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles junto al valor.
- **Opciones** — Opciones de radio bajo licencia (solo lectura). Muestra la lista de opciones de la radio, o un valor predeterminado como "GPS, PGXL" si se detecta un amplificador. Incluye un botón de copia al portapapeles junto al valor.
- **FlexControl** — Estado detectado del hardware FlexControl (solo lectura).
- **multiFLEX** — Estado habilitado de multiFLEX (solo lectura).
- **Información de licencia** — Muestra suscripción, fecha de vencimiento, ID de radio y versión con licencia (solo lectura). Cada campo incluye un botón de copia al portapapeles junto al valor.

### Copiar información de la radio

Cada valor de solo lectura tiene un pequeño botón de copia junto a él. Haga clic en el botón de copia para copiar el valor al portapapeles. Aparece una breve ventana emergente "¡Copiado!" cerca del botón. El botón de copia está deshabilitado cuando el valor está vacío o muestra "—".

### Configuración de identificación

| Control                                             | Qué hace                                                                                                                                                                                   | Notas                                                                                                                               |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Apodo**                                           | Apodo de radio fácil de usar (editable).                                                                                                                                                    | —                                                                                                                                   |
| **Indicativo**                                      | Indicativo de la estación (editable).                                                                                                                                                       | —                                                                                                                                   |
| **Nombre de estación**                              | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en AppSettings.                                                                                              | El valor predeterminado es el nombre de host del SO si está vacío. Se envía a la radio como 'estación cliente <nombre>'.            |
| Seleccionar instalador...                           | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Explorar .ssdr...' a 'Seleccionar instalador...' en v26.5.3.                                                |
| SmartLink (pestaña)                                 | Gestión de certificados TLS anclados de SmartLink. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con botones Olvidar por fila y Olvidar todo. Nuevo en v26.5.3 (#2951 Fase 2). | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de anclaje ahora pausa el protocolo de enlace con un diálogo modal. |
| Certificados SmartLink anclados (sección)           | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso). | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}.                             |
| Host / Huella SHA-256 / Anclado (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), Huella SHA-256 (monoespacio), Anclado (AAAA-MM-DD o '(pre-fase 2)').                                                              | Respaldado por WanCertCache en WanConnection.cpp.                                                                                    |
| Olvidar seleccionado                                | Elimina la huella del certificado anclado del host seleccionado para que la próxima conexión vuelva a anclar silenciosamente.                                                               |                                                                                                                                     |
| Olvidar todo                                        | Limpia todos los certificados anclados (con confirmación). La próxima conexión a cada radio vuelve a anclar silenciosamente.                                                                | Muestra QMessageBox::question antes de borrar.                                                                                       |

### Actualización de firmware

1. Haga clic en **Buscar actualización** para consultar actualizaciones de firmware disponibles. El resultado aparece en la etiqueta de estado. Si hay una actualización disponible, la etiqueta le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Haga clic en **Seleccionar instalador...** para abrir un selector de archivos. Seleccione uno de:
   - `.msi` — Instalador de SmartSDR basado en WiX para firmware 4.2+.
   - `.exe` — Instalador de SmartSDR autoextraíble más antiguo.
   - `.ssdr` — Archivo de firmware preextraído.
3. El gestor de firmware detecta el formato de archivo automáticamente y extrae la carga útil `.ssdr`. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción.
4. Una vez que la extracción se completa, haga clic en **Subir firmware** para iniciar la subida. Una barra de progreso y una etiqueta de estado muestran el progreso de la subida.

| Control | Qué hace | Notas |
|---|---|---|
| **Buscar actualización** | Consulta actualizaciones de firmware disponibles. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador desde flexradio.com. |
| **Seleccionar instalador...** | Abre un selector de archivos para archivos `.msi`, `.exe` o `.ssdr`. | Renombrado desde **Explorar .ssdr...** en v26.5.3. |
| **Subir firmware** | Inicia la subida de firmware con barra de progreso y estado. | Se habilita solo después de que se completa la extracción. |

### Encendido remoto

Haga clic en **Encendido remoto** para habilitar la función de encendido remoto en la radio.

### Reiniciar radio

Haga clic en **Reiniciar radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:
- **Conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de iniciarse.
- **Conexión SmartLink/WAN**: AetherSDR se desconecta y no se reconecta automáticamente. Debe reconectarse manualmente una vez que la radio termina de iniciarse.

El botón está deshabilitado cuando la radio está desconectada. Se rehabilita automáticamente cuando la radio se reconecta.

---

## Pestaña Red

La pestaña **Red** muestra información de red de la radio y opciones de red avanzadas.

### Lectura de información de red

- **Dirección IP / Máscara / Dirección MAC** — Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles.

### Configuración de red

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Exigir conexiones IP privadas:** | Alternar para rechazar pares que no sean RFC1918. | Habilitado | — |
| **MTU de red:** | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes. | 1450 | Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| **DHCP / Estática** | Alterna entre modos DHCP e IP estática. | — | — |
| **Dirección IP: / Máscara: / Puerta de enlace:** | Campos de configuración de IP estática. | — | Se habilita cuando se selecciona el modo Estática. |
| **Aplicar** | Envía la configuración de red a la radio. | — | — |

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información de posición/satélite en vivo cuando hay un receptor GPS activo.

- Latitud, longitud, altitud, hora y número de satélites (solo lectura).
- Indicador de estado de bloqueo de GPS.

---

## Pestaña TX

La pestaña **TX** configura los tiempos de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en cascada, seguimiento de slice/TX y configuración de banda de TX.

### Configuración de banda de TX

Haga clic en **Configuración de banda de TX** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos

Use los cuadros de giro en la sección **Tiempos (en ms)** para configurar los tiempos de retención y retardo de TX.

### Enclavamientos

Active **TX REQ: RCA** y **TX REQ: Accesorio** para habilitar las entradas de enclavamiento de RCA y accesorio.

### Potencia máxima

Establezca el límite superior de potencia de TX a nivel de radio usando el cuadro de giro **Potencia máxima:** (0–100%).

### Modo de sintonía

Seleccione el comportamiento del botón de sintonía en el cuadro combinado **Modo de sintonía:**.

### Cascada

Active **Mostrar TX en cascada:** para dibujar la señal de TX en la cascada.

### Seguimiento de slice/TX

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **TX sigue al slice activo** | TX sigue al slice activo. | Falso | Mutuamente excluyente con **El slice activo sigue a TX**. Se deshabilita automáticamente durante la operación de split. |
| **El slice activo sigue a TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). | Falso | Mutuamente excluyente con **TX sigue al slice activo**. |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de nivel

Active **Habilitar/deshabilitar el medidor de nivel durante la recepción** para mostrar el medidor de nivel de micrófono incluso durante la recepción.

### Manipulador CW

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — | En v0.9.1, se agregaron los botones Modo A y Modo B junto al alternador Habilitado. Modo A = Curtis A; Modo B = Curtis B. |
| **Modo iámbico: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. | A | Par mutuamente excluyente agregado en v0.9.1. |
| **Intercambiar:** | Intercambia dit/dah. | — | — |
| **Banda lateral:** | Selecciona la banda lateral del tono CW. | — | Opciones: LSB / USB. |
| **CWX:** | Habilita la activación de macros CWX. | — | — |
| **Decodificar:** | Habilita la superposición de decodificación CW en el panadapter. | Verdadero | Se almacena como `CwDecodeOverlay`. |

### RTTY

Configure el cuadro de giro **Marca RTTY predeterminada:** con la frecuencia de marca RTTY predeterminada.

---

## Pestaña RX

La pestaña **RX** proporciona la calibración de desviación de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

La sección de calibración siempre está visible, independientemente de si hay un GPSDO instalado.

- **GPSDO instalado** — se muestra en verde: *GPSDO instalado. Calibración manual de desviación de frecuencia disponible.*
- **Sin GPSDO** — se muestra en ámbar: *Calibración manual de desviación de frecuencia disponible.*

| Control | Qué hace | Notas |
|---|---|---|
| **Frecuencia de calibración (MHz):** | Frecuencia usada para la calibración manual. | Siempre se muestra. |
| **Iniciar** | Inicia el barrido de calibración de frecuencia. | Se deshabilita y etiqueta como **Ocupado** mientras está activo. Valida que se haya ingresado una frecuencia de calibración. Restablece el error de frecuencia almacenado a cero antes de iniciar. |
| **Desviación de frecuencia (ppb):** | Desviación de frecuencia manual en partes por billón. | Se restablece a 0 cuando se hace clic en **Iniciar**. |

### Fuente de referencia de 10 MHz

El cuadro combinado **Fuente de referencia de 10 MHz:** se completa dinámicamente según el hardware detectado y el estado del oscilador en vivo.

| Control | Qué hace | Notas |
|---|---|---|
| **Fuente de referencia de 10 MHz:** | Selecciona la fuente de referencia del oscilador. Envía `radio oscillator <valor>` a la radio cuando se cambia. | **Auto** siempre presente. Entradas adicionales: **TCXO**, **GPSDO**, **10 MHz externa**. Las opciones dependen del hardware detectado y del estado del oscilador en vivo. |
| Etiqueta de estado de bloqueo | Muestra la fuente activa, la resolución de Auto y el estado de bloqueo. Se actualiza en vivo. | Verde = Bloqueado; Rojo = Desbloqueado; Gris-azul = esperando estado. Agrega *(no detectado)* cuando la 10 MHz externa está activa pero no hay señal de referencia externa presente. |

La etiqueta de estado de bloqueo muestra:
- *Esperando estado del oscilador* cuando el estado aún no se ha recibido.
- *Auto -> \<fuente resuelta\>* cuando Auto está seleccionado y la radio ha resuelto una fuente específica.
- *\<configuración\> -> \<estado activo\>* cuando la configuración y el estado activo difieren.
- El nombre de la fuente activa solo cuando coinciden.

El estado de bloqueo (*Bloqueado* o *Desbloqueado*) siempre se agrega.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Qué hace | Notas |
|---|---|---|
| **Salida de línea:** | Control deslizante de
