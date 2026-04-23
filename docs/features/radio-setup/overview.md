# Descripción general de la configuración del radio

El diálogo Radio Setup es la ventana de configuración central para su radio Flex conectado. Reúne identificación del radio, red, GPS, transmisión, audio, filtros, transvertidores, cables USB y periféricos en una única interfaz con pestañas.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio Flex. El diálogo requiere una conexión activa con el radio.

## Cómo funciona

Abra el diálogo mediante `Settings > Radio Setup...`. El diálogo permanece abierto mientras trabaja; ciérrelo con el botón Close cuando termine.

El diálogo está organizado en pestañas. Cada pestaña cubre un área específica de la configuración del radio. Las pestañas distintas a Radio se construyen en el primer acceso, por lo que puede haber una breve demora la primera vez que hace clic en una pestaña.

También puede ir directamente a pestañas específicas:

- `Settings > FlexControl...` abre el diálogo en la pestaña Serial.
- `Settings > USB Cables...` abre el diálogo en la pestaña USB Cables.

### Resumen de pestañas

| Pestaña | Qué cubre |
|---|---|
| Radio | Identificación del radio, apodo, indicativo, nombre de estación, información de licencia y actualización de firmware. |
| Network | Dirección IP, MTU, DHCP vs. IP estática y restricción de IP privada. |
| GPS | Presencia de GPS y posición en tiempo real, altitud, hora y datos de satélites. |
| TX | Tiempos de TX, enclavamientos, potencia máxima (0–100 %), modo de ajuste, visualización TX en el waterfall y comportamiento de seguimiento TX/slice. |
| Phone/CW | Medidor de nivel de micrófono, tecleador iámbico, intercambio dit/dah, banda lateral del tono CW (LSB o USB), CWX, decodificador CW y marca predeterminada de RTTY. |
| RX | Calibración de frecuencia GPSDO, desplazamiento de frecuencia manual (ppb) y fuente de referencia de 10 MHz (Internal o External). |
| Audio | Salidas de audio del radio (línea de salida, auriculares, altavoz frontal), selección de dispositivo de audio del PC, compresión de audio, boost, búfer, grabación y eliminación de ruido NVIDIA BNR. |
| Filters | Preferencia de filtro Low Latency vs. Sharp por ancho de banda, con opción para forzar filtros de baja latencia en modos digitales. |
| XVTR | Configuración por transvertidor: modo solo RX, eliminar y Create New Transverter. |
| USB Cables | Asigna adaptadores USB serie a los tipos de cable CAT, BCD, bit y PTT, con control completo de parámetros serie. |
| Peripherals | Conexión manual por IP para dispositivos TGXL, PGXL y Antenna Genius. |
| Serial | Selección del puerto serie de FlexControl, parámetros de línea, asignación de función de pines, intercambio de paleta, apertura automática y detección del mando de sintonía de FlexControl. (Solo se muestra cuando la compatibilidad con puerto serie está compilada.) |

### Configuración de audio y grabación

La pestaña Audio contiene los controles con ajustes persistentes que se modifican con más frecuencia en operación remota y con SmartLink.

| Control | Qué hace | Clave de ajuste | Valor predeterminado | Rango |
|---|---|---|---|---|
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | `AudioCompression` | Auto | Auto, Uncompressed, Opus |
| Audio Boost: | Activa ganancia adicional en la ruta de audio del cliente. | `AudioBoost` | — | On / Off |
| Audio Buffer: | Aumenta el búfer de audio para absorber la fluctuación de VPN o SmartLink. | `AudioBuffer` | — | 50–1000 ms |
| Recording: Radio Side / Client Side | Selecciona si la grabación se realiza en el radio o en este equipo. | `RecordMode` | — | Radio Side, Client Side |
| Save to: | Carpeta donde se guardan las grabaciones. | `RecordDir` | — | Cualquier ruta válida |
| Auto-record on TX | Inicia la grabación automáticamente cada vez que transmite. | `AutoRecordTx` | — | On / Off |
| Idle timeout: | Segundos de silencio tras los cuales se detiene una grabación activa. | `RecordIdleTimeout` | — | — |

## Consejos

- El acceso directo TX Band Settings en la pestaña TX abre el diálogo dedicado de potencia y ajuste por banda, el mismo accesible mediante `Settings > TX Band Settings...`.
- Station Name toma como valor predeterminado el nombre de host del sistema operativo si se deja en blanco. Identifica este cliente ante otras estaciones multiFLEX.
- La pestaña Serial aparece solo en compilaciones que incluyen compatibilidad con puerto serie. Si no la ve, use `Settings > FlexControl...` para confirmar si la compatibilidad con puerto serie está disponible en su instalación.

## Relacionado

- [Establecer el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Establecer la potencia máxima de TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el boost de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertidor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
