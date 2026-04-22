# Descripción general de la configuración del radio

El diálogo Radio Setup es la ventana central de configuración para su FLEX-8600 conectado. Cubre desde la identidad del radio y los ajustes de red hasta audio, comportamiento de TX, filtros, transvertidores, cables USB y dispositivos periféricos.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio. Radio Setup requiere una conexión activa con el radio.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El diálogo se abre en la pestaña **Radio**. Hay once pestañas disponibles; las pestañas distintas de **Radio** se construyen la primera vez que se seleccionan.

También puede ir directamente a pestañas específicas:

- `Settings > FlexControl...` — abre el diálogo en la pestaña **Serial**.
- `Settings > USB Cables...` — abre el diálogo en la pestaña **USB Cables**.

El diálogo recuerda su tamaño y posición entre sesiones. Ciérrelo con el botón **Close**; todos los cambios surten efecto de inmediato al ajustar los controles — no existe un botón global de Apply ni de Save.

### Resumen de pestañas

| Pestaña | Qué cubre |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones con licencia, estado de FlexControl y multiFLEX, apodo, indicativo, nombre de estación, información de licencia y actualización de firmware. |
| **Network** | IP/máscara/MAC de solo lectura, DHCP frente a IP estática, MTU y aplicación de IP privada. |
| **GPS** | Presencia del GPS y latitud, longitud, altitud, hora y cantidad de satélites en tiempo real. |
| **TX** | Temporizaciones de TX, entradas de interlock, límite de potencia a nivel del radio, modo de sintonía, visualización de TX en el waterfall, comportamiento de seguimiento TX/slice y acceso directo a TX Band Settings. |
| **Phone/CW** | Medidor de nivel del micrófono, manipulador iámbico, inversión dit/dah, banda lateral del tono CW, manipulación de macros CWX, decodificador CW y frecuencia de marca RTTY predeterminada. |
| **RX** | Calibración de desplazamiento de frecuencia GPSDO y selección de fuente de referencia de 10 MHz. |
| **Audio** | Niveles de salida de línea y auriculares del radio, selección de dispositivo de audio del PC, códec de compresión de audio, boost de audio, tamaño del búfer de audio, modo de grabación y carpeta, grabación automática en TX, tiempo de espera por inactividad y control del contenedor NVIDIA BNR. |
| **Filters** | Preferencia de filtro de baja latencia frente a filtro pronunciado por ancho de banda, y filtros de baja latencia forzados para modos digitales. |
| **XVTR** | Configuración por transvertidor; creación, configuración y eliminación de entradas de transvertidor. |
| **USB Cables** | Asignación de adaptadores seriales USB detectados como tipos de cable CAT, BCD, bit o PTT, con parámetros seriales por cable. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL y Antenna Genius. |
| **Serial** | Selección del puerto serial de FlexControl, parámetros de línea, función y polaridad de los pines DTR/RTS, inversión de paleta, apertura automática al iniciar y detección del mando de sintonía. (Presente solo cuando el soporte de puerto serial está incorporado.) |

## Qué hace cada control

Los siguientes controles almacenan configuraciones en el AppSettings de AetherSDR. Todos los demás controles del diálogo se comunican directamente con el radio y no se almacenan localmente.

| Etiqueta | Pestaña | Comportamiento | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto | Auto, Uncompressed, Opus | `AudioCompression` |
| **Audio Boost:** | Audio | Activa ganancia adicional en la ruta de audio del cliente. | — | On / Off | `AudioBoost` |
| **Audio Buffer:** | Audio | Amplía el búfer de audio del lado del cliente para absorber la fluctuación de VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Recording: Radio Side / Client Side** | Audio | Selecciona si la grabación la realiza el radio o AetherSDR en el PC. | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | Audio | Ruta de la carpeta donde se guardan las grabaciones. | — | Cualquier ruta válida | `RecordDir` |
| **Auto-record on TX** | Audio | Inicia la grabación automáticamente cada vez que el radio transmite. | — | On / Off | `AutoRecordTx` |
| **Idle timeout:** | Audio | Segundos de silencio tras los cuales se detiene una grabación activa. | — | — | `RecordIdleTimeout` |

## Consejos

- El control giratorio **Audio Buffer:** (50–1000 ms) es más útil en rutas de red de alta latencia o con fluctuaciones, como VPNs y conexiones SmartLink. Auméntelo si el audio se interrumpe durante la operación remota.
- **Auto-record on TX** combinado con **Idle timeout:** permite capturar transmisiones como archivos individuales sin iniciar ni detener la grabadora manualmente.
- La pestaña **Serial** solo aparece si AetherSDR fue compilado con soporte de puerto serial. Si no la ve, use `Settings > FlexControl...`, que abrirá el diálogo y mostrará la pestaña si está disponible.

## Relacionados

- [Verificar el número de serie, la versión de hardware, la región y las opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Establecer el apodo, el indicativo y el nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN o remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Establecer la potencia máxima de TX por banda y el modo de sintonía](set-per-band-tx-max-power-and-tune-mode.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el boost de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Activar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y pronunciados por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertidor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
