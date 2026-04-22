# Verificar la marca de tiempo del primer paquete UDP tras la conexión

Use el indicador **First UDP Packet** en Network Diagnostics para confirmar que la ruta de datos UDP desde el radio se ha establecido después de conectarse.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- No es necesario tener una conexión de radio activa para abrir el diálogo, pero el indicador solo es significativo después de un intento de conexión.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Localice el grupo **Network Status** en la parte superior izquierda del diálogo.
3. Lea la fila **First UDP Packet**.
   - Muestra **Yes** una vez que se ha recibido el primer paquete UDP del radio desde que se estableció la conexión actual.
   - Muestra **No** si aún no ha llegado ningún paquete UDP.
4. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **First UDP Packet** | Muestra **Yes** o **No**. **Yes** significa que se ha recibido al menos un paquete UDP del radio desde la conexión. **No** significa que la ruta UDP aún no ha transportado ningún dato. |

## Consejos

- El indicador se restablece cada vez que se reconecta. Si se desconecta y vuelve a conectarse, abra nuevamente el diálogo para ver el estado actualizado.
- Si el indicador permanece en **No** mientras **Status** muestra un estado conectado, la ruta de control TCP está activa pero la ruta de flujo UDP está bloqueada. Verifique las reglas del firewall y confirme que el extremo UDP local que aparece en **Local UDP** sea accesible desde el radio.
- En una red VPN o enrutada, el UDP suele estar bloqueado mientras el TCP pasa sin problemas. Consulte la sección de contenido relacionado para obtener orientación sobre esas configuraciones.

## Resolución de problemas

- **First UDP Packet muestra "No" indefinidamente después de conectarse** — El radio puede alcanzar AetherSDR por TCP (los comandos funcionan) pero los paquetes UDP no están llegando. Verifique que cualquier firewall en el host Linux permita UDP entrante en el puerto que aparece en **Local UDP**. En una ruta enrutada o VPN, confirme que el UDP no esté filtrado entre el radio y la máquina cliente.

## Contenido relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP del radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Medir el RTT y la pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
