# Conectar manualmente un AG a través de una red remota

Use esta página para conectar AetherSDR a un Antenna Genius que no se encuentra en la LAN local — por ejemplo, a través de una VPN o una red enrutada — ingresando su dirección IP directamente. El descubrimiento por UDP solo funciona en la subred local, por lo que se requiere una entrada manual de IP para dispositivos remotos.

## Antes de comenzar

- El Antenna Genius debe ser accesible desde su equipo en el puerto TCP 9007. Confirme esto con la configuración de su red o VPN antes de continuar.
- El applet de Antenna Genius permanece oculto hasta que se descubre un dispositivo o se conecta manualmente. Si no ve el botón de bandeja del AG en la barra lateral derecha, eso es normal — aparecerá tras una conexión exitosa.

## Pasos

1. Abra el panel de applets. Si no está visible, haga clic en `View > Applet Panel`.
2. Busque el botón de bandeja del AG en la barra lateral derecha. Si el applet ya está abierto, vaya al paso 4.
3. Si aún no aparece ningún botón de bandeja del AG, continúe con los pasos restantes — el botón aparece una vez que se establece una conexión.
4. En el applet de Antenna Genius, localice el campo **Manual IP** (etiquetado "Manual IP:").
5. Escriba la dirección IPv4 o IPv6 del Antenna Genius remoto en el campo **Manual IP**.
6. Presione **Enter**. AetherSDR valida la dirección y se conecta al puerto 9007.
7. Observe la etiqueta de estado debajo del combo de dispositivos. Una conexión exitosa muestra `Connected — <name> v<version>`. Una conexión inalcanzable o rechazada muestra `Error: <msg>`.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Manual IP** | Almacena y utiliza una dirección IP para conectarse directamente, omitiendo el descubrimiento por UDP. Al presionar Enter se inicia el intento de conexión. | _(en blanco)_ | Dirección IPv4 o IPv6 | `AG_ManualIp` |
| **Connect / Disconnect** | Se conecta al dispositivo seleccionado en el combo de dispositivos, o a la dirección de **Manual IP** si no hay ningún dispositivo descubierto seleccionado. Cambia a Disconnect cuando está conectado. | Connect | — | — |
| Etiqueta de estado | Muestra el estado actual de descubrimiento o conexión. | No device found | No device found, Device found, Connected — \<name\> v\<version\>, Disconnected, Error: \<msg\>, Invalid IP address | — |

## Consejos

- AetherSDR guarda la última dirección utilizada en `AG_ManualIp` al presionar Enter. El campo se rellena previamente con esa dirección la próxima vez que abra el applet.
- Si el combo de dispositivos contiene un dispositivo descubierto, hacer clic en Connect se conecta a ese dispositivo, no a la **Manual IP**. Borre o ignore la selección del combo si desea que la **Manual IP** surta efecto mediante el botón Connect. Presionar Enter en el campo **Manual IP** siempre utiliza la dirección escrita, independientemente del estado del combo.
- El Puerto B se oculta automáticamente si el Antenna Genius conectado reporta solo un puerto de radio.

## Solución de problemas

- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — AetherSDR alcanzó la capa de red pero no pudo completar la conexión. Verifique que el puerto 9007 esté abierto y que el Antenna Genius esté encendido y sea accesible en la dirección ingresada.
- **El botón de bandeja del AG nunca aparece** — El applet permanece oculto hasta que se establece una conexión. Revise la etiqueta de estado dentro del panel de applets para obtener detalles del error. Si el panel en sí no está visible, actívelo mediante `View > Applet Panel`.

## Relacionados

- [Descripción general del Antenna Genius](../../features/antenna-genius/overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
