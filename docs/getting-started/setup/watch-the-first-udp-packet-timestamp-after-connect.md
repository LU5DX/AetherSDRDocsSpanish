# Observar la marca de tiempo del primer paquete UDP tras la conexión

El indicador **First UDP Packet** en Network Diagnostics muestra si AetherSDR ha recibido algún dato UDP del radio desde que se estableció la conexión actual. Úselo para confirmar que la ruta de datos UDP está abierta — si falta el primer paquete, los datos de audio, FFT y waterfall no pueden fluir, aunque el canal de comandos TCP esté activo.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No es necesario que el radio esté conectado; el diálogo se abre independientemente.
- Para que el indicador muestre un resultado significativo, conéctese primero a un radio — consulte [Conectarse a un radio en la LAN local](connect-to-a-local-lan-radio.md).

## Pasos

1. Haga clic en `Settings > Network...`.
2. Se abre el diálogo **Network Diagnostics**.
3. Localice el grupo **Network Status** en la zona superior izquierda del diálogo.
4. Lea la fila **First UDP Packet**.
   - **Yes** — ha llegado al menos un paquete UDP del radio desde la conexión.
   - **No** — no se ha recibido ningún paquete UDP en la conexión actual.
5. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **First UDP Packet** | Muestra **Yes** o **No**. Se reinicia cada vez que se establece una nueva conexión. Indica si se ha recibido algún paquete UDP del radio en la sesión actual. |
| **Status** | Estado general del enlace de la conexión. |
| **Local UDP** | El punto de enlace UDP local en el que AetherSDR está escuchando. Si está vacío o es inesperado, el tráfico UDP no puede llegar en absoluto. |
| **Target Radio IP** | Dirección IP del radio conectado. Muestra `Not connected` cuando no hay ningún radio conectado. |

## Consejos

- El indicador se actualiza una vez por segundo. Espere unos segundos después de conectarse antes de concluir que no llega tráfico UDP.
- Si **First UDP Packet** permanece en **No** mientras **Status** muestra un estado conectado, verifique **Local UDP** para confirmar que hay un puerto enlazado. La causa más frecuente es un cortafuegos que bloquea el puerto UDP.
- **First UDP Packet** se reinicia a **No** en cada nueva conexión. Desconéctese y vuelva a conectarse para repetir la prueba después de cambiar la configuración de red.

## Solución de problemas

- **First UDP Packet muestra "No" después de varios segundos conectado** — La ruta de comandos TCP está activa pero el UDP está bloqueado. Verifique que su cortafuegos permita UDP entrante desde la IP del radio. Revise **Local UDP** para confirmar que AetherSDR ha enlazado un puerto. En una red enrutada o VPN, confirme que la ruta es simétrica — consulte [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md).
- **First UDP Packet muestra "Yes" pero el audio no se escucha** — El UDP está llegando; el problema está en una capa posterior a la de red. Revise **RX Buffer Now**, **Underruns (total / last sec)** y **Audio Arrival Gap** en el grupo **Audio Playback** — consulte [Diagnosticar interrupciones de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md).

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP del radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a un radio en la LAN local](connect-to-a-local-lan-radio.md)
- [Diagnosticar interrupciones de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
