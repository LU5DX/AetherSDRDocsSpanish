# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en IA al audio de su micrófono. Use los controles de la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema de forma independiente a AetherSDR. AetherSDR lo controla pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se inicie, haga clic en **Autostart Container** para activarlo.
5. Para iniciar el contenedor inmediatamente, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin cambiarlo, haga clic en **Check Status**. El punto de estado coloreado junto a los controles se actualiza para mostrar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al iniciarse. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR inmediatamente. |
| **Stop** | Botón | Detiene un contenedor NVIDIA BNR en ejecución inmediatamente. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el punto de estado. |
| Punto de estado NVIDIA BNR | Indicador | Punto coloreado que muestra el estado del contenedor: Running, Stopped o Unknown. |
| **TX Follows Active Slice** | Botón | TX sigue a la franja activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia la franja activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo. El control deslizante se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón | Habilita la selección automática del nivel de filtro para ese modo y desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Connected solo cuando el dispositivo identificado en esa conexión es un Antenna Genius (no un ShackSwitch). |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión AG. La autodetección mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era **Browse .ssdr...** en versiones anteriores a v0.9.3. |
| Pestaña **APD** | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa: selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de las series 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan dinámicamente desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| Pestaña **Themes** | Pestaña | Pestaña de personalización de la interfaz de usuario: actualmente alberga la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color de las franjas entre la paleta integrada de AetherSDR y un conjunto totalmente personalizado por franja. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de franja A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa franja. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter e insignias de canal CAT. Los botones están desactivados cuando **Use Aether defaults** está seleccionado. Hasta 8 franjas. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores de franja personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles en la pestaña **Radio** para verificar actualizaciones de firmware y cargar firmware en la radio.

### Verificación de actualizaciones

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

### Preparación y carga de firmware

En v0.9.3, el botón **Browse .ssdr...** pasó a llamarse **Select Installer...** y ahora acepta el instalador completo de SmartSDR descargado de FlexRadio, además de un archivo `.ssdr` preextraído.

1. Descargue el instalador de SmartSDR desde flexradio.com si aún no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador WiX de FlexRadio v4.2+
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato del archivo a partir de los primeros 8 bytes y extrae el contenido `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *nombrearchivo*..." mientras la preparación está en curso.
4. Cuando la preparación finalice, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado rastrean la carga.

### Notas

- Si la etiqueta de estado no se actualiza después de hacer clic en **Select Installer...**, verifique que el archivo seleccionado sea un `.msi`, `.exe` o `.ssdr` válido.
- No se desconecte de la radio mientras una carga está en curso.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1, los controles de calibración de frecuencia de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, cuando se detectaba un GPSDO, los campos de calibración estaban ocultos y reemplazados por un mensaje que indicaba que no se requería corrección. La pestaña ahora siempre muestra el campo **Cal Frequency (MHz)** y el botón **Start**.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea durante toda la secuencia de calibración:

| Texto de estado | Significado |
|---|---|
| Starting... | AetherSDR ha enviado los comandos de calibración a la radio. |
| Busy | El botón **Start** está desactivado; la calibración está en curso. |
| (texto de error) | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**. |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar). En ambos casos, los controles debajo de la etiqueta se comportan de manera idéntica.

### Cuadro combinado de fuente de referencia de 10 MHz (v0.9.7)

En v0.9.7, el cuadro combinado **10 MHz Reference Source:** y la etiqueta de estado de bloqueo junto a él se actualizaron para proporcionar una visualización más rica.

**Población del cuadro combinado:** La lista de fuentes disponibles ahora se construye dinámicamente cada vez que se abre la pestaña **RX**, según lo que informa la radio. Se incluye una fuente si la radio la tiene seleccionada actualmente, si está activamente en uso, o si el hardware correspondiente está presente. La entrada siempre presente es **Auto**. Las entradas adicionales aparecen de la siguiente manera:

| Entrada | Se muestra cuando |
|---|---|
| TCXO | La radio informa que el hardware TCXO está presente, o TCXO es la configuración actual o el estado activo. |
| GPSDO | La radio informa que el hardware GPSDO está presente, o GPSDO es la configuración actual o el estado activo. |
| External 10 MHz | La radio informa que se detectó una referencia externa, o External es la configuración actual o el estado activo, o se ha recibido el estado del oscilador. |

Nota: la entrada anteriormente etiquetada como **External** ahora está etiquetada como **External 10 MHz**.

**Etiqueta de estado de bloqueo:** La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador en un formato más rico que antes:

| Condición | Texto de la etiqueta (ejemplos) |
|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status |
| Modo Auto, la radio resuelve a una fuente | Auto -> GPSDO Locked |
| La configuración difiere del estado activo | TCXO -> GPSDO Locked |
| La configuración coincide con el estado activo | GPSDO Locked |
| Fuente activa desbloqueada | GPSDO Unlocked |
| External seleccionado, sin señal detectada | External 10 MHz Unlocked (not detected) |

El color de la etiqueta permanece verde cuando está bloqueada y rojo cuando está desbloqueada. Antes de que llegue cualquier estado de la radio, la etiqueta se muestra en un azul grisáceo apagado.

### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración
