# Descripción general de la configuración de radio

El diálogo Radio Setup es la ventana central de configuración de su FLEX-8600. Agrupa todos los ajustes por radio — identificación, red, GPS, transmisión, audio, filtros, transvertidores, cables USB y periféricos externos — en una única interfaz con pestañas.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Radio Setup requiere una conexión de radio activa.

## Cómo funciona

Abra el diálogo desde `Settings > Radio Setup...`. AetherSDR también ofrece dos accesos directos que abren el diálogo en una pestaña específica: `Settings > FlexControl...` salta a la pestaña Serial, y `Settings > USB Cables...` salta a la pestaña USB Cables.

El diálogo contiene las siguientes pestañas:

**Radio** — Muestra información de hardware de solo lectura (número de serie, región, versión de hardware, opciones con licencia, estado de FlexControl, estado de multiFLEX) y campos de identificación editables (Nickname, Callsign, Station Name). También muestra los detalles de la licencia y proporciona controles para actualizar el firmware.

**Network** — Muestra la dirección IP actual de la radio, la máscara de subred y la dirección MAC. Permite cambiar entre DHCP e IP estática, configurar un MTU de red personalizado y forzar conexiones con IP privada.

**GPS** — Muestra datos GPS en tiempo real (latitud, longitud, altitud, hora, cantidad de satélites) cuando hay un receptor GPS presente.

**TX** — Controla los tiempos de transmisión, los interlocks TX/RCA, la potencia de salida máxima (0–100 %), el modo de ajuste, la visualización TX en el waterfall y el comportamiento de seguimiento TX/slice. Abre el diálogo TX Band Settings por banda mediante el botón `TX Band Settings`.

**Phone/CW** — Configura el medidor de nivel del micrófono, el keyer iámbico (Iambic, Swap), la banda lateral de CW (LSB o USB), el tecleo de macros CWX, el decodificador de CW y la frecuencia de marca RTTY predeterminada.

**RX** — Proporciona la calibración de frecuencia GPSDO (Cal Frequency, Freq Offset en ppb, Start) y permite seleccionar la fuente de referencia de 10 MHz (Internal o External).

**Audio** — Controla los niveles de salida del lado de la radio (Line Out, Headphone, Front Speaker) con botones de silencio, selecciona el códec de audio para SmartLink (`AudioCompression`: Auto, Uncompressed u Opus), elige los dispositivos de entrada y salida de audio del PC, habilita `AudioBoost`, establece el tamaño de `AudioBuffer` (50–1000 ms), configura las opciones de grabación y gestiona el contenedor de eliminación de ruido NVIDIA BNR.

**Filters** — Selecciona las familias de filtros Low Latency o Sharp por ancho de banda y, opcionalmente, fuerza el uso de filtros de baja latencia para modos digitales (DIGU/DIGL).

**XVTR** — Crea y gestiona definiciones de transvertidores. Cada entrada de transvertidor tiene su propia pestaña anidada con el modo RX Only y un botón Remove. El botón `Create New Transverter` agrega una nueva entrada.

**USB Cables** — Muestra los adaptadores serie USB detectados con su estado de conexión/desconexión y asigna a cada cable un tipo (CAT, BCD, bit o PTT) con configuración completa de parámetros serie.

**Peripherals** — Conecta dispositivos externos (TGXL, PGXL, Antenna Genius) por dirección IP mediante botones Connect y Disconnect por dispositivo.

**Serial** — Configura el puerto serie de FlexControl: selección de puerto, parámetros de baudios/datos/paridad/bits de parada, función y asignación de polaridad DTR/RTS, intercambio de paleta y detección del mando de sintonía FlexControl. Esta pestaña solo está presente cuando AetherSDR se compila con soporte de puerto serie.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|
| Audio Compression (SmartLink): Auto / Uncompressed / Opus | Selecciona el códec de audio utilizado a través de SmartLink o LAN | Auto | Auto, Uncompressed, Opus | `AudioCompression` |
| Audio Boost: | Habilita ganancia adicional en la ruta de audio del cliente | — | On / Off | `AudioBoost` |
| Audio Buffer: | Aumenta el búfer de audio del cliente para absorber la fluctuación de VPN o SmartLink | — | 50–1000 ms | `AudioBuffer` |
| Recording: Radio Side / Client Side | Selecciona si el audio se graba en la radio o en este PC | — | Radio Side, Client Side | `RecordMode` |
| Save to: | Ruta de carpeta donde se guardan las grabaciones | — | Cualquier ruta con permisos de escritura | `RecordDir` |
| Auto-record on TX | Inicia la grabación automáticamente cuando la radio transmite | — | On / Off | `AutoRecordTx` |
| Idle timeout: | Segundos de silencio tras los cuales se detiene una grabación activa | — | — | `RecordIdleTimeout` |

## Consejos

- El diálogo recuerda su tamaño y posición entre sesiones. Ajústelo una vez y se volverá a abrir con las mismas dimensiones.
- Station Name usa de forma predeterminada el nombre del host del sistema operativo si se deja en blanco. Identifica este cliente AetherSDR ante otras estaciones multiFLEX en la misma radio.
- Aumentar `AudioBuffer` reduce los cortes de audio en enlaces de alta latencia a costa de un mayor retardo.

## Temas relacionados

- [Verificar el número de serie, la versión de hardware, la región y las opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Establecer el apodo, el indicativo y el nombre de estación de la radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Subir un nuevo firmware .ssdr a la radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Configurar la potencia máxima TX y el modo de ajuste por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
- [Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda](toggle-low-latency-vs-sharp-filters-per-bandwidth.md)
- [Crear una nueva entrada de transvertidor](create-a-new-transverter-entry.md)
- [Asignar un cable USB como CAT, BCD, bit o PTT](assign-a-usb-cable-as-cat-bcd-bit-or-ptt.md)
- [Conectar TGXL, PGXL o Antenna Genius por IP](../../getting-started/setup/connect-tgxl-pgxl-or-antenna-genius-by-ip.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
