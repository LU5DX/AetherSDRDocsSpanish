# Verificar la marca de tiempo del primer paquete UDP tras la conexión

Use el diálogo Network Diagnostics para confirmar que el flujo de datos UDP del radio ha llegado a su equipo después de conectarse. El indicador **First UDP Packet** le indica si ha llegado algún tráfico UDP desde que comenzó la sesión actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse tanto si hay un radio conectado como si no, pero **First UDP Packet** solo tiene sentido después de un intento de conexión.
- Debe haber iniciado previamente una conexión a un radio FLEX-8600.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el diálogo **Network Diagnostics**, localice el grupo **Network Status**.
3. Lea el indicador **First UDP Packet**. Muestra `Yes` si se ha recibido al menos un paquete UDP desde la conexión, o `No` si aún no ha llegado ninguno.
4. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Indicador | Significado |
|---|---|
| **First UDP Packet** | Muestra `Yes` o `No`. Se actualiza una vez por segundo. Indica si se ha recibido algún paquete UDP del radio en la sesión actual. |
| **Status** | Estado general del enlace. |
| **Local UDP** | El punto de enlace UDP local en el que AetherSDR está escuchando. Útil para confirmar que el puerto correcto está asociado. |
| **Target Radio IP** | Dirección IP del radio conectado. |

## Consejos

- El diálogo actualiza todos los indicadores una vez por segundo. Si **First UDP Packet** permanece en `No` varios segundos después de conectarse, el tráfico UDP no está llegando al equipo — revise las reglas del cortafuegos, el enrutamiento y que el punto de enlace UDP local mostrado en **Local UDP** sea accesible desde el radio.
- En un enlace VPN o enrutado, TCP puede conectarse correctamente mientras que UDP está bloqueado por separado. Que **First UDP Packet** muestre `No` mientras **Status** muestra un estado conectado es un indicador fiable de esta situación.
- **First UDP Packet** se restablece en cada nueva conexión. Desconéctese y vuelva a conectarse si desea verificar nuevamente la entrega de paquetes tras cambiar la configuración de red.

## Solución de problemas

- **First UDP Packet permanece en "No" tras la conexión** — UDP no está llegando al punto de enlace local. Verifique que ningún cortafuegos esté bloqueando UDP en el puerto indicado en **Local UDP**, y que el radio pueda enrutar de vuelta a la IP de su equipo. En una conexión VPN, confirme que la VPN permite el paso de UDP en ambas direcciones.
- **First UDP Packet muestra "Yes" pero el audio no se escucha** — UDP está llegando, pero un problema diferente afecta la reproducción. Revise el grupo **Audio Playback** en busca de interrupciones del búfer (underruns) o problemas de búfer, y consulte la página de diagnóstico de audio.

## Relacionado

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP del radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar interrupciones de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar la interfaz de red local para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
