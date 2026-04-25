# Observar la marca de tiempo del primer paquete UDP tras la conexión

El indicador **First UDP Packet** en Network Diagnostics confirma que el flujo de datos UDP del radio ha llegado a su equipo después de establecer una conexión. Úselo para verificar que el camino UDP está abierto y que los paquetes fluyen, no solo el canal de control TCP.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Se debe haber realizado un intento de conexión al radio. El indicador es más útil inmediatamente después de conectar.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. En el grupo **Network Status**, localice la fila **First UDP Packet**.
3. Lea el valor. Muestra **Yes** o **No**.

## Qué hace cada control

| Indicador | Significado | Notas |
|---|---|---|
| **First UDP Packet** | Muestra **Yes** si se ha recibido al menos un paquete UDP del radio desde la conexión; **No** en caso contrario. | Se reinicia cada vez que se establece una nueva conexión. |

## Consejos

- El diálogo se actualiza una vez por segundo. Si el valor cambia de **No** a **Yes** poco después de conectar, el camino UDP se abrió correctamente.
- Si **First UDP Packet** permanece en **No** mientras **Status** muestra conexión activa, el canal de control TCP está activo pero el tráfico UDP está bloqueado. Verifique las reglas de firewall y NAT del enrutador para el puerto UDP utilizado por el radio.
- **First UDP Packet** solo indica que llegó un paquete. Compruebe las tasas de **Audio**, **FFT** y **Waterfall** en el grupo **Incoming Stream Rates** para confirmar un flujo de datos sostenido.

## Solución de problemas

- **First UDP Packet permanece en "No" tras conectar** — El handshake TCP fue exitoso pero no han llegado paquetes UDP. Es probable que un firewall o una regla NAT esté bloqueando el flujo UDP. Verifique que su firewall permita UDP entrante desde la IP del radio. En una ruta enrutada o VPN, confirme que el UDP no está filtrado entre los dos extremos.

## Relacionados

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP del radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
