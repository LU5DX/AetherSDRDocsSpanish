# Descripción general de la configuración del radio

El cuadro de diálogo Radio Setup es la ventana de configuración central de su FLEX-8600. Reúne en un solo lugar la identificación del radio, la red, el GPS, la transmisión, el audio, los filtros, los transvertores, los cables USB, los periféricos y la configuración serial de FlexControl. Ábralo siempre que necesite cambiar algún aspecto de la interacción entre AetherSDR y el hardware de su radio.

## Antes de comenzar

- El radio debe estar conectado. Radio Setup requiere una conexión activa con el radio.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El cuadro de diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área de configuración específica. Las pestañas distintas a Radio cargan su contenido la primera vez que hace clic en ellas.

También puede ir directamente a pestañas específicas:

- `Settings > USB Cables...` abre Radio Setup con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Radio Setup con la pestaña **Serial** activa (disponible únicamente cuando el soporte de puerto serial está integrado).

El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

### Pestañas de un vistazo

| Pestaña | Qué se configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones licenciadas, apodo, indicativo, nombre de la estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado del GPS en tiempo real: latitud, longitud, altitud, hora y cantidad de satélites. |
| **TX** | Tiempos de retención/retardo de TX, bloqueos, límite de potencia global, modo de ajuste, visualización de TX en el waterfall, comportamiento de seguimiento TX/slice y acceso directo a los ajustes por banda. |
| **Phone/CW** | Medidor de nivel del micrófono, keyer iámbico (modo A/B, inversión, banda lateral), CWX, decodificador CW y frecuencia de marca RTTY predeterminada. |
| **RX** | Calibración de frecuencia GPSDO y selección de fuente de referencia de 10 MHz. |
| **Audio** | Niveles de salida de línea, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; refuerzo de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática al transmitir y tiempo de espera por inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia o filtro cortante por ancho de banda, y una opción independiente para modos digitales. |
| **XVTR** | Configuración por transvertor; creación o eliminación de entradas de transvertor. |
| **USB Cables** | Asignación de adaptadores seriales USB a tipos de cable CAT, BCD, bit y PTT, y configuración de sus parámetros seriales. |
| **Peripherals** | Conexión manual por IP a dispositivos externos: TGXL, PGXL y Antenna Genius. |
| **Serial** | Selección del puerto serial de FlexControl, parámetros de línea, asignación de funciones de pines (DTR/RTS), inversión de paleta, apertura automática y detección del mando de sintonía. (Visible únicamente cuando el soporte de puerto serial está integrado.) |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistentes.

| Control | Pestaña | Comportamiento | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto | Auto, Uncompressed, Opus | `AudioCompression` |
| **Audio Boost:** | Audio | Activa ganancia adicional en la ruta de audio del lado del cliente. | — | Habilitado / Deshabilitado | `AudioBoost` |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio para absorber la fluctuación de fase (jitter) de VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en el radio o en este equipo. | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | Audio | Ruta de la carpeta donde se guardan las grabaciones. | — | Cualquier ruta de directorio válida | `RecordDir` |
| **Auto-record on TX** | Audio | Inicia la grabación automáticamente cada vez que el radio transmite. | — | Activado / Desactivado | `AutoRecordTx` |
| **Idle timeout:** | Audio | Segundos de silencio tras los cuales una grabación activa se detiene automáticamente. | — | — | `RecordIdleTimeout` |

## Consejos

- Si opera a través de una VPN o SmartLink y escucha interrupciones de audio, aumente **Audio Buffer:** hacia el extremo superior de su rango de 50–1000 ms.
- **Auto-record on TX** combinado con **Idle timeout:** es útil para el registro en concursos: la grabación comienza cuando transmite y se detiene automáticamente tras un período de silencio configurable.
- El botón **TX Band Settings** en la pestaña TX abre el cuadro de diálogo dedicado de potencia y ajuste por banda, el mismo disponible en `Settings > TX Band Settings...`.

## Relacionados

- [Establecer el apodo, el indicativo y el nombre de la estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Verificar el número de serie, la versión de hardware, la región y las opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Configurar la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Seleccionar el modo iámbico A o B para el keyer del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre audio Opus o sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática al transmitir y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y filtros cortantes por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
