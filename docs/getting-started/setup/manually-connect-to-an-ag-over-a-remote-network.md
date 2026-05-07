# Conectarse manualmente a un AG a través de una red remota

Utilice esta página para conectar AetherSDR a un Antenna Genius que no esté en la LAN local (por ejemplo, a través de una VPN o una red enrutada) ingresando su dirección IP directamente. El descubrimiento por UDP solo funciona en la subred local, por lo que se requiere una entrada manual de IP para dispositivos remotos.

## Antes de comenzar

- El Antenna Genius debe ser accesible desde su máquina a través del puerto TCP 9007. Confirme esto con su configuración de red o VPN antes de proceder.
- El applet de Antenna Genius está oculto hasta que se descubre un dispositivo o se conecta manualmente. Si no ve el botón de la bandeja AG en la barra lateral derecha, es normal: aparecerá después de una conexión exitosa.

## Pasos

1. Abra el panel de applets. Si no está visible, haga clic en `View > Applet Panel`.
2. Busque el botón de la bandeja AG en la barra lateral derecha. Si el applet ya está abierto, continúe con el paso 4.
3. Si aún no hay ningún botón de la bandeja AG visible, continúe con los pasos restantes: el botón aparece una vez que se establece una conexión.
4. En el applet de Antenna Genius, localice el campo **Manual IP** (etiquetado "Manual IP:").
5. Escriba la dirección IPv4 o IPv6 del Antenna Genius remoto en el campo **Manual IP**.
6. Presione **Enter**. AetherSDR valida la dirección y se conecta al puerto 9007.
7. Observe la etiqueta de estado debajo del combo de dispositivos. Una conexión exitosa muestra `Connected — <nombre> v<versión>`. Una conexión inalcanzable o rechazada muestra `Error: <mensaje>`.

## Función de cada control

| Control | Qué hace | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Manual IP** | Almacena y utiliza una dirección IP para conectarse directamente, omitiendo el descubrimiento UDP. Presionar Enter inicia el intento de conexión. | _(en blanco)_ | Dirección IPv4 o IPv6 | `AG_ManualIp` |
| **Connect / Disconnect** | Se conecta al dispositivo seleccionado en el combo de dispositivos, o a la dirección IP manual si no hay ningún dispositivo descubierto seleccionado. Cambia a Disconnect cuando está conectado. | Connect | — | — |
| Etiqueta de estado | Muestra el estado actual de descubrimiento o conexión. | No device found | No device found, Device found, Connected — \<nombre\> v\<versión\>, Disconnected, Error: \<mensaje\>, Invalid IP address | — |

## Consejos

- AetherSDR guarda la última dirección utilizada en `AG_ManualIp` cuando presiona Enter. El campo se rellena previamente con esa dirección la próxima vez que abra el applet.
- Si el combo de dispositivos contiene un dispositivo descubierto, al hacer clic en Connect se conecta a ese dispositivo, no a la IP manual. Borre o ignore la selección del combo si desea que la IP manual tenga efecto a través del botón Connect. Presionar Enter en el campo Manual IP siempre utiliza la dirección escrita, independientemente del estado del combo.
- El puerto B se oculta automáticamente si el Antenna Genius conectado informa solo un puerto de radio.
- La auto-conexión al descubrirse aplica solo a dispositivos Antenna Genius. Si se descubre un ShackSwitch en la misma red, no se conecta automáticamente desde este applet; el applet ShackSwitch lo maneja por separado.

## Solución de problemas

- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<mensaje\>"** — AetherSDR llegó a la capa de red pero no pudo completar la conexión. Verifique que el puerto 9007 esté abierto y que el Antenna Genius esté encendido y accesible en la dirección que ingresó.
- **El botón de la bandeja AG nunca aparece** — El applet permanece oculto hasta que se establece una conexión. Revise la etiqueta de estado dentro del panel de applets para ver los detalles del error. Si el panel en sí no está visible, actívalo mediante `View > Applet Panel`.
- **Un dispositivo descubierto no se conecta automáticamente** — Si el primer dispositivo descubierto en la LAN es un ShackSwitch, el applet de Antenna Genius no se conectará automáticamente a él. El applet de ShackSwitch maneja ese dispositivo. Verifique si hay un dispositivo Antenna Genius independiente presente en su red.

## Relacionado

- [Antenna Genius overview](../../features/antenna-genius/overview.md)
- [Auto-discover an Antenna Genius on the LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Select an antenna for Port A or Port B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Enable AUTO mode so the AG follows radio band changes](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
