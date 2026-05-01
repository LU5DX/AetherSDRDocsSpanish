# Conectar manualmente a un AG a través de una red remota

Use esta página para conectar AetherSDR a un Antenna Genius que no está en la LAN local — por ejemplo, a través de una VPN o una red enrutada — ingresando su dirección IP directamente. El descubrimiento UDP solo funciona en la subred local, por lo que se requiere una entrada manual de IP para dispositivos remotos.

## Antes de comenzar

- El Antenna Genius debe ser accesible desde su máquina en el puerto TCP 9007. Confirme esto con su configuración de red o VPN antes de continuar.
- El applet Antenna Genius está oculto hasta que se descubre o se conecta manualmente un dispositivo. Si no ve el botón de bandeja AG en la barra lateral derecha, eso es normal — aparecerá después de una conexión exitosa.

## Pasos

1. Abra el panel de applets. Si no es visible, haga clic en `View > Applet Panel`.
2. Busque el botón de bandeja AG en la barra lateral derecha. Si el applet ya está abierto, vaya al paso 4.
3. Si aún no se ve ningún botón de bandeja AG, continúe con los pasos restantes — el botón aparece una vez que se establece una conexión.
4. En el applet Antenna Genius, localice el campo **Manual IP** (etiquetado como "Manual IP:").
5. Escriba la dirección IPv4 o IPv6 del Antenna Genius remoto en el campo **Manual IP**.
6. Presione **Enter**. AetherSDR valida la dirección y se conecta al puerto 9007.
7. Observe la etiqueta de estado debajo del combo de dispositivos. Una conexión exitosa muestra `Connected — <name> v<version>`. Una conexión inaccesible o rechazada muestra `Error: <msg>`.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Manual IP** | Almacena y usa una dirección IP para conectarse directamente, omitiendo el descubrimiento UDP. Al presionar Enter se desencadena el intento de conexión. | _(en blanco)_ | Dirección IPv4 o IPv6 | `AG_ManualIp` |
| **Connect / Disconnect** | Se conecta al dispositivo seleccionado en el combo de dispositivos, o a la dirección IP manual si no hay dispositivo descubierto seleccionado. Se convierte en Disconnect cuando está conectado. | Connect | — | — |
| Etiqueta de estado | Muestra el estado actual de descubrimiento o conexión. | No device found | No device found, Device found, Connected — \<name\> v\<version\>, Disconnected, Error: \<msg\>, Invalid IP address | — |

## Consejos

- AetherSDR guarda la última dirección utilizada en `AG_ManualIp` cuando presiona Enter. El campo se completa previamente con esa dirección la próxima vez que abre el applet.
- Si el combo de dispositivos contiene un dispositivo descubierto, hacer clic en Connect se conecta a ese dispositivo, no a la IP manual. Borre o ignore la selección del combo si desea que la IP manual tenga efecto a través del botón Connect. Al presionar Enter en el campo Manual IP siempre se usa la dirección escrita independientemente del estado del combo.
- El Puerto B se oculta automáticamente si el Antenna Genius conectado reporta solo un puerto de radio.
- La conexión automática al descubrimiento aplica solo a dispositivos Antenna Genius. Si se descubre un ShackSwitch en la misma red, no se conecta automáticamente desde este applet; en su lugar, lo maneja el applet ShackSwitch.

## Solución de problemas

- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — AetherSDR alcanzó la capa de red pero no pudo completar la conexión. Verifique que el puerto 9007 está abierto y que el Antenna Genius está encendido y accesible en la dirección que ingresó.
- **El botón de bandeja AG nunca aparece** — El applet permanece oculto hasta que se establece una conexión. Consulte la etiqueta de estado dentro del panel de applets para obtener detalles del error. Si el panel en sí no es visible, habilítelo a través de `View > Applet Panel`.
- **Un dispositivo descubierto no se conecta automáticamente** — Si el primer dispositivo descubierto en la LAN es un ShackSwitch, el applet Antenna Genius no se conectará automáticamente a él. El applet ShackSwitch maneja ese dispositivo. Compruebe si hay un dispositivo Antenna Genius separado presente en su red.

## Relacionado

- [Descripción general de Antenna Genius](../../features/antenna-genius/overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar una antena para Puerto A o Puerto B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Habilitar modo AUTO para que el AG siga los cambios de banda de radio](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
