# Descripción general de Radio Setup

Radio Setup es el diálogo maestro de configuración por radio en AetherSDR. Reúne todos los ajustes de hardware y software específicos de un FLEX-8600 conectado: identificación, red, GPS, transmisión, audio, filtros, transvertores, cables USB y periféricos.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. Radio Setup requiere una conexión de radio activa.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El diálogo contiene un conjunto de pestañas; cada pestaña agrupa ajustes relacionados. Las pestañas distintas a Radio se construyen en el primer acceso, por lo que puede haber una breve demora la primera vez que haga clic en una pestaña.

También puede ir directamente a pestañas específicas:

- `Settings > USB Cables...` abre el diálogo con la pestaña USB Cables activa.
- `Settings > FlexControl...` abre el diálogo con la pestaña Serial activa.

El diálogo recuerda su tamaño y posición entre sesiones.

### Resumen de pestañas

| Pestaña | Contenido |
|---|---|
| Radio | Número de serie, versión de hardware, región, opciones con licencia, apodo, indicativo, nombre de estación, información de licencia, actualización de firmware. |
| Network | Dirección IP, dirección MAC, MTU, conmutación DHCP/IP estática, aplicación de IP privada. |
| GPS | Presencia de GPS y posición en tiempo real, altitud, hora y cantidad de satélites. |
| TX | Temporizaciones de TX, interbloqueos, límite máximo de potencia (0–100 %), modo de ajuste, visualización TX en el waterfall, modos de seguimiento TX/slice, y acceso directo a TX Band Settings. |
| Phone/CW | Medidor de nivel de micrófono, keyer iámbico, intercambio dit/dah, banda lateral de CW, CWX, decodificador CW, valor predeterminado de marca RTTY. |
| RX | Calibración de desplazamiento de frecuencia GPSDO, desplazamiento de frecuencia manual en ppb, fuente de referencia de 10 MHz (Internal o External). |
| Audio | Niveles de salida de línea y auriculares del radio, selección de dispositivo de audio del PC, compresión de audio, refuerzo de audio, búfer de audio, modo de grabación y carpeta, grabación automática en TX, tiempo de espera por inactividad, contenedor NVIDIA BNR. |
| Filters | Familia de filtros Low Latency o Sharp por ancho de banda, con opción para forzar filtros de baja latencia en modos digitales. |
| XVTR | Configuración por transvertor, activación de solo recepción, eliminación y Create New Transverter. |
| USB Cables | Asigna adaptadores seriales USB a tipos de cable CAT, BCD, bit y PTT con parámetros seriales por cable. |
| Peripherals | Conexión manual por IP para periféricos TGXL, PGXL y Antenna Genius. |
| Serial | Selección de puerto serial de FlexControl, parámetros de línea, asignación de función de pines DTR/RTS, intercambio de paleta, apertura automática al inicio. (Presente solo cuando el soporte de puerto serial está disponible.) |

## Qué hace cada control

Los siguientes ajustes son guardados por AetherSDR entre sesiones.

| Etiqueta | Pestaña | Comportamiento | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|---|
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado para conexiones SmartLink y LAN. | Auto | Auto, Uncompressed, Opus | `AudioCompression` |
| Audio Boost: | Audio | Activa ganancia adicional en la ruta de audio del cliente. | — | On/Off | `AudioBoost` |
| Audio Buffer: | Audio | Aumenta el búfer de audio para absorber jitter en conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| Recording: Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en el radio o en el PC cliente. | — | Radio Side, Client Side | `RecordMode` |
| Save to: | Audio | Establece la carpeta donde se guardan las grabaciones. | — | Cualquier ruta válida | `RecordDir` |
| Auto-record on TX | Audio | Inicia automáticamente la grabación cuando el radio transmite. | — | On/Off | `AutoRecordTx` |
| Idle timeout: | Audio | Número de segundos de silencio antes de que se detenga una grabación activa. | — | — | `RecordIdleTimeout` |

## Consejos

- Si opera a través de una VPN o SmartLink y el audio se escucha entrecortado, aumente `AudioBuffer` (pestaña Audio) y considere configurar `AudioCompression` en Opus.
- La pestaña Serial solo está presente cuando AetherSDR fue compilado con soporte de puerto serial. Si no la ve, use `Settings > FlexControl...` como acceso directo — abrirá el diálogo e indicará si la pestaña está disponible.
- El diálogo se vuelve a abrir en la pestaña que utilizó por última vez durante la sesión, pero siempre inicia en la pestaña Radio después de un arranque nuevo.

## Relacionados

- [Verificar el número de serie del radio, versión de hardware, región y opciones](check-radio-serial-hardware-version-region-and-options.md)
- [Establecer el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Establecer la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y elegir una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
