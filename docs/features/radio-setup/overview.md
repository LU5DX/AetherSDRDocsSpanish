# Descripción general de la configuración del radio

El diálogo Radio Setup es la ventana de configuración central para su FLEX-8600. Reúne en un solo lugar la identificación del radio, la red, el GPS, la transmisión, el audio, los filtros, los transvertidores, los accesorios USB, los periféricos externos y — en las compilaciones que lo soportan — el puerto serie para FlexControl. Ábralo una vez para familiarizarse con él; regrese a las pestañas específicas cuando necesite cambiar algún ajuste.

## Cómo funciona

Abra el diálogo con `Settings > Radio Setup...`. El diálogo tiene una barra de pestañas en la parte superior; cada pestaña cubre un área específica de la configuración del radio. Las pestañas se construyen en el primer uso, por lo que cambiar a una pestaña por primera vez puede tomar un momento mientras AetherSDR examina el hardware conectado.

También puede ir directamente a pestañas específicas mediante `Settings > USB Cables...` (abre la pestaña USB Cables) y `Settings > FlexControl...` (abre la pestaña Serial, cuando está disponible).

El diálogo no tiene botón Apply ni OK en la mayoría de las pestañas — los cambios surten efecto de inmediato al interactuar con un control. La excepción es la pestaña Network, que tiene su propio botón "Apply". Cierre el diálogo con el botón "Close" en la parte inferior.

### Resumen de pestañas

| Pestaña | Contenido |
|---|---|
| Radio | Número de serie, región, versión de hardware, opciones con licencia, apodo, indicativo, nombre de la estación, información de licencia y actualización de firmware. |
| Network | Direcciones IP/MAC de solo lectura, cambio entre DHCP/estático, campos de IP estática, MTU y restricción de IP privada. |
| GPS | Indicador de presencia de GPS y datos en tiempo real de latitud, longitud, altitud, hora y cantidad de satélites. |
| TX | Temporización de TX, enclavamientos, límite máximo de potencia (0–100 %), modo de ajuste, visualización de TX en el waterfall, modos de seguimiento TX/slice y acceso directo a TX Band Settings. |
| Phone/CW | Medidor de nivel de micrófono, manipulador iámbico, intercambio dit/dah, banda lateral de CW, macros CWX, decodificador CW y marca RTTY predeterminada. |
| RX | Calibración de frecuencia GPSDO, compensación de frecuencia manual (ppb) y fuente de referencia de 10 MHz (Internal o External). |
| Audio | Ganancia y silencio de salida de línea y auriculares, selección de dispositivo de audio del PC, códec de compresión de audio, refuerzo de audio, tamaño del búfer de audio, modo de grabación y carpeta, grabación automática en TX, tiempo de espera por inactividad y controles del contenedor NVIDIA BNR. |
| Filters | Selección de filtro Low Latency o Sharp por ancho de banda, y una opción separada para forzar filtros de baja latencia en modos digitales. |
| XVTR | Pestañas de configuración por transvertidor, interruptor de solo recepción, eliminación y Create New Transverter. |
| USB Cables | Lista los adaptadores serie USB detectados; asigna cada uno como CAT, BCD, bit o PTT con todos los parámetros de serie. |
| Peripherals | Conexión y desconexión manual por IP para TGXL, PGXL y Antenna Genius. |
| Serial | Selección del puerto serie para FlexControl, parámetros de línea, asignación de pines DTR/RTS, intercambio de paleta, apertura automática al iniciar y detección/cierre del mando de sintonía. Disponible solo en compilaciones con soporte de puerto serie. |

### Ajustes persistentes en la pestaña Audio

Los siguientes ajustes se guardan en la configuración de la aplicación AetherSDR y se conservan entre sesiones.

| Control | Clave de ajuste | Valor predeterminado | Rango válido | Función |
|---|---|---|---|---|
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | `AudioCompression` | Auto | Auto, Uncompressed, Opus | Selecciona el códec de audio utilizado a través de SmartLink o LAN. |
| Audio Boost: | `AudioBoost` | — | On / Off | Activa ganancia adicional en la ruta de audio del cliente. |
| Audio Buffer: | `AudioBuffer` | — | 50–1000 ms | Aumenta el búfer de audio para absorber la fluctuación de latencia de VPN o SmartLink. |
| Recording: Radio Side / Client Side | `RecordMode` | — | Radio Side, Client Side | Selecciona si la grabación ocurre en el radio o en este PC. |
| Save to: | `RecordDir` | — | Cualquier ruta de carpeta con permisos de escritura | Carpeta donde se guardan las grabaciones. |
| Auto-record on TX | `AutoRecordTx` | — | On / Off | Inicia la grabación automáticamente cuando transmite. |
| Idle timeout: | `RecordIdleTimeout` | — | — (segundos) | Segundos de silencio tras los cuales se detiene una grabación iniciada automáticamente. |

## Consejos

- Si `Settings > FlexControl...` no es visible en su menú, la compilación no incluye soporte de puerto serie.
- La pestaña Serial también estará ausente de la barra de pestañas en ese caso.
- Se puede acceder a TX Band Settings desde `Settings > TX Band Settings...` en el menú o desde el botón "TX Band Settings" dentro de la pestaña TX.

## Temas relacionados

- [Verificar el número de serie, la versión de hardware, la región y las opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Establecer el apodo, el indicativo y el nombre de la estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN o remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Configurar la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Seleccionar los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y filtros Sharp por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertidor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serie FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
