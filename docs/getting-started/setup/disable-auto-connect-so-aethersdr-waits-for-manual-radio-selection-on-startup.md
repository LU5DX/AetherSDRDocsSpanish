# Deshabilitar la conexión automática para que AetherSDR espere la selección manual del radio al iniciar

De forma predeterminada, AetherSDR se reconecta al último radio utilizado cada vez que se inicia. Deshabilitar esta opción hace que AetherSDR abra el diálogo de conexión al iniciar, de modo que pueda elegir un radio manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- No se requiere ninguna conexión de radio para cambiar esta configuración.

## Pasos

1. Haga clic en `Settings > Connect to Radio...`.
2. En el panel "Connect to a Radio", desplácese hasta la parte inferior de la página.
3. Localice la casilla de verificación etiquetada como "Connect to last radio on start up".
4. Desmarque "Connect to last radio on start up".

La configuración se guarda inmediatamente en `AutoConnectToLastRadio`. La próxima vez que AetherSDR se inicie, abrirá el diálogo de conexión automáticamente en lugar de reconectarse al último radio.

## Qué hace cada control

| Control | Valor predeterminado | Configuración persistida | Comportamiento |
|---|---|---|---|
| Casilla "Connect to last radio on start up" | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se conecta automáticamente al último radio utilizado al iniciar. Cuando está desmarcada, el diálogo de conexión se abre al iniciar y debe seleccionar un radio manualmente. |

## Consejos

- Esta configuración también suprime el intento de conexión automática que ocurre durante el descubrimiento por difusión y el sondeo de radios enrutados, no solo la reconexión inicial al iniciar.
- Si comparte el equipo entre varias estaciones o cambia de radio con frecuencia, dejar esta opción desmarcada evita conectarse al radio incorrecto por accidente.

## Solución de problemas

- **AetherSDR sigue conectándose automáticamente después de desmarcar la casilla** — Confirme que desmarcó la casilla dentro de `Settings > Connect to Radio...` y no en un diálogo diferente. La etiqueta de la casilla es exactamente "Connect to last radio on start up". Cierre y vuelva a iniciar AetherSDR para verificar que el cambio surte efecto.

## Relacionados

- [Conectarse a un radio en la red LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto mediante SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Desconectarse del radio actual](disconnect-from-the-current-radio.md)
