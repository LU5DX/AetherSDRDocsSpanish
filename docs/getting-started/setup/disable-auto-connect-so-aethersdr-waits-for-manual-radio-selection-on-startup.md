# Desactivar la reconexión automática para que AetherSDR espere la selección manual de radio al iniciar

De forma predeterminada, AetherSDR se reconecta a la última radio utilizada cada vez que se inicia. Desactivar esta opción hace que AetherSDR abra el cuadro de diálogo de conexión al iniciar, permitiéndole elegir una radio manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- No se requiere ninguna conexión de radio para cambiar esta configuración.

## Pasos

1. Haga clic en `Settings > Connect to Radio...`.
2. En el panel "Connect to a Radio", desplácese hasta la parte inferior de la página.
3. Localice la casilla de verificación etiquetada como "Connect to last radio on start up".
4. Desmarque "Connect to last radio on start up".

La configuración se guarda inmediatamente en `AutoConnectToLastRadio`. La próxima vez que AetherSDR se inicie, abrirá el cuadro de diálogo de conexión automáticamente en lugar de reconectarse a la última radio.

## Función de cada control

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Casilla "Connect to last radio on start up" | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se reconecta automáticamente a la última radio utilizada al iniciar. Cuando no está marcada, se abre el cuadro de diálogo de conexión al iniciar y debe seleccionar una radio manualmente. |

## Consejos

- Esta configuración también suprime el intento de conexión automática que ocurre durante el descubrimiento de emisiones y el sondeo de radio enrutada, no solo la reconexión inicial al arranque.
- Si comparte el equipo entre varias estaciones o cambia de radio con frecuencia, dejar esta opción desmarcada evita conectarse a la radio equivocada accidentalmente.

## Solución de problemas

- **AetherSDR sigue reconectándose automáticamente después de desmarcar la casilla** — Confirme que desmarcó la casilla dentro de `Settings > Connect to Radio...` y no en un cuadro de diálogo diferente. La etiqueta de la casilla es exactamente "Connect to last radio on start up". Cierre y reinicie AetherSDR para verificar que el cambio surta efecto.

## Relacionados

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
