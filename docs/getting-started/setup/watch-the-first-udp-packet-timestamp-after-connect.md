# Verificar la marca de tiempo del primer paquete UDP tras la conexión

El indicador **First UDP Packet** en Network Diagnostics confirma si la radio ha abierto correctamente la ruta de datos UDP hacia su máquina. Comprobarlo inmediatamente después de conectarse le ayuda a distinguir un enlace en buen estado de una conexión unilateral en la que TCP negoció correctamente pero no llegó ningún flujo UDP.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Debe haber intentado conectarse a una radio FLEX-8600. El indicador solo tiene significado después de un intento de conexión; no requiere que la conexión esté completamente establecida.

## Pasos

1. Abra `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice la sección **Network Status**.
3. Lea el campo **First UDP Packet**.
   - **Yes** — al menos un paquete UDP ha llegado desde la radio desde la última conexión.
   - **No** — aún no se ha recibido ningún paquete UDP.
4. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **First UDP Packet** | Muestra **Yes** o **No**. Indica si el primer paquete UDP proveniente de la radio se ha recibido desde que se estableció la conexión actual. El valor se restablece en cada nueva conexión. |
| **Status** | Estado general del enlace con la radio. |
| **Local UDP** | El extremo local en el que AetherSDR escucha el tráfico UDP entrante. |
| **Target Radio IP** | La dirección IP de la radio a la que AetherSDR está conectado. |

## Consejos

- Si **First UDP Packet** permanece en **No** después de varios segundos, el flujo UDP de la radio no está llegando a su máquina. Verifique las reglas del cortafuegos en el equipo host: la radio envía UDP al puerto indicado en **Local UDP**, y ese puerto debe ser accesible desde la IP de la radio que se muestra en **Target Radio IP**.
- El diálogo se actualiza una vez por segundo, por lo que **First UDP Packet** cambiará a **Yes** en un segundo tras la llegada del primer paquete.
- **First UDP Packet** por sí solo no confirma un flujo en buen estado. Una vez que muestre **Yes**, compruebe también **Latency (RTT)** y las tasas por categoría (Audio, FFT, Waterfall) para confirmar que los datos fluyen con normalidad.

## Solución de problemas

- **First UDP Packet permanece en "No" tras conectarse** — La ruta UDP desde la radio hasta su máquina está bloqueada. Verifique que ningún cortafuegos ni regla NAT esté descartando el tráfico UDP entrante en el puerto indicado en **Local UDP**. En una red VPN o enrutada, confirme que la radio puede alcanzar la IP de su máquina en ese puerto.
- **First UDP Packet muestra "Yes" pero el audio está en silencio** — UDP está llegando, pero es posible que el flujo de audio no esté activo. Compruebe la tasa **Audio** en la sección Incoming Stream Rates, así como los campos **RX Buffer Now** y **Underruns** en Audio Playback.

## Relacionados

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP de la radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Comprobar las tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](../../features/network-diagnostics/check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
