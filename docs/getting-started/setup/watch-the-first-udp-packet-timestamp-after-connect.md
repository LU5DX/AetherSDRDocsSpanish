# Verificar el sello de tiempo del primer paquete UDP tras la conexión

Use el diálogo Network Diagnostics para confirmar que el flujo de datos UDP del radio ha llegado a su equipo después de conectarse. El indicador **First UDP Packet** le indica si ha llegado tráfico UDP desde que comenzó la sesión actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo puede abrirse con o sin un radio conectado, pero **First UDP Packet** solo es significativo después de un intento de conexión.
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
| **Local UDP** | El punto de conexión UDP local en el que escucha AetherSDR. Útil para confirmar que el puerto correcto está enlazado. |
| **Target Radio IP** | Dirección IP del radio conectado. |

## Consejos

- El diálogo actualiza todos los indicadores una vez por segundo. Si **First UDP Packet** permanece en `No` varios segundos después de conectarse, el tráfico UDP no está llegando al equipo anfitrión — verifique las reglas del cortafuegos, el enrutamiento y que el punto de conexión UDP local que aparece en **Local UDP** sea accesible desde el radio.
- En un enlace VPN o enrutado, TCP puede conectarse correctamente mientras UDP está bloqueado por separado. Que **First UDP Packet** muestre `No` con **Status** mostrando un estado conectado es un indicador fiable de esta situación.
- **First UDP Packet** se reinicia en cada nueva conexión. Desconéctese y vuelva a conectarse si desea verificar nuevamente la entrega de paquetes tras cambiar la configuración de red.

## Solución de problemas

- **First UDP Packet permanece en "No" después de conectarse** — UDP no está llegando al punto de conexión local. Verifique que ningún cortafuegos esté bloqueando UDP en el puerto que aparece en **Local UDP**, y que el radio pueda enrutar de regreso a la IP de su equipo. En una conexión VPN, confirme que la VPN permite el paso de UDP en ambas direcciones.
- **First UDP Packet muestra "Yes" pero el audio no tiene sonido** — UDP está llegando, pero un problema distinto afecta la reproducción. Revise el grupo **Audio Playback** para detectar interrupciones de buffer o problemas de almacenamiento en búfer, y consulte la página de diagnóstico de audio.

## Relacionados

- [Descripción general de Network Diagnostics](../../features/network-diagnostics/overview.md)
- [Verificar la IP del radio y la dirección de enlace local](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnosticar interrupciones de audio y fluctuaciones de temporización](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar la interfaz de red local para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
