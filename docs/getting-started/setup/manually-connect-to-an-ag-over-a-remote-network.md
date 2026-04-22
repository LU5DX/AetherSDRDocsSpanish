# Conectar manualmente un AG a través de una red remota

Use este procedimiento cuando su Antenna Genius no se encuentre en el mismo segmento de red LAN que AetherSDR y el descubrimiento por UDP no pueda alcanzarlo. Ingresar la dirección IP del dispositivo directamente omite el descubrimiento y se conecta al puerto 9007.

## Antes de comenzar

- Conoce la dirección IPv4 o IPv6 del Antenna Genius en la red remota.
- La red remota permite tráfico TCP al puerto 9007 del Antenna Genius (VPN, reenvío de puertos o ruta enrutada).
- El applet de Antenna Genius es visible. Si el botón AG en la bandeja lateral derecha no aparece, AetherSDR aún no ha detectado ningún dispositivo. Continúe de todos modos — ingresar una IP manual hará que el applet aparezca tras una conexión exitosa.

## Pasos

1. Haga clic en el botón **AG** de la bandeja lateral derecha para abrir el applet de Antenna Genius.
2. Localice el campo **Manual IP** debajo de la etiqueta de estado.
3. Escriba la dirección IPv4 o IPv6 del Antenna Genius en el campo **Manual IP**.
4. Presione **Enter**.
   - AetherSDR valida la dirección. Si está mal formada, la etiqueta de estado se torna roja y muestra `Invalid IP address`. Corrija la dirección y presione **Enter** nuevamente.
   - Si la dirección es válida, AetherSDR la guarda en `AG_ManualIp` e intenta conectarse al puerto 9007.
5. Observe la etiqueta de estado:
   - `Connected — <name> v<version>` confirma una conexión exitosa. El botón **Connect / Disconnect** cambia a **Disconnect**.
   - `Error: <msg>` significa que el dispositivo no fue alcanzable o rechazó la conexión. Verifique la dirección, las reglas del cortafuegos y que el puerto 9007 esté abierto.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave persistente |
|---|---|---|---|
| **Manual IP** | Acepta una dirección IPv4 o IPv6. Presione **Enter** para iniciar una conexión al puerto 9007. Una dirección inválida muestra `Invalid IP address` en rojo. | *(en blanco, o la última dirección usada)* | `AG_ManualIp` |
| **Connect / Disconnect** | Cuando está desconectado y no hay ningún dispositivo descubierto seleccionado en el combo de dispositivos, hacer clic en **Connect** también inicia un intento de conexión por IP manual. Cambia a **Disconnect** cuando está conectado. | Connect | — |
| Etiqueta de estado | Muestra el estado de descubrimiento y conexión: `No device found`, `Device found`, `Connected — <name> v<version>`, `Disconnected`, `Error: <msg>` o `Invalid IP address`. | No device found | — |

## Consejos

- AetherSDR restaura la última IP manual utilizada desde `AG_ManualIp` al iniciarse, por lo que el campo aparece prellenado en lanzamientos posteriores.
- Si ya hay un dispositivo seleccionado en el combo de dispositivos, hacer clic en **Connect** se conecta a ese dispositivo descubierto en lugar de usar la IP manual. Borre o ignore la selección del combo si desea usar la ruta de IP manual.
- El Puerto B se oculta si el Antenna Genius conectado reporta solo un puerto de radio. Esto es normal en dispositivos de un solo puerto.

## Solución de problemas

- **La etiqueta de estado muestra `Invalid IP address`** — El texto en el campo **Manual IP** no es una dirección IPv4 o IPv6 válida. Verifique si hay errores tipográficos, espacios no deseados o un nombre de host (los nombres de host no se aceptan; use una dirección IP numérica).
- **La etiqueta de estado muestra `Error: <msg>` tras una dirección válida** — El Antenna Genius no es alcanzable en el puerto 9007. Verifique que la dirección IP sea correcta, que una VPN o ruta hacia la red remota esté activa, y que ningún cortafuegos esté bloqueando el puerto 9007.
- **El botón AG de la bandeja no es visible** — El applet permanece oculto hasta que se detecta o conecta un dispositivo. Si no puede ver el botón de la bandeja, consulte [Descripción general de Antenna Genius](../../features/antenna-genius/overview.md) para saber cómo mostrar el panel del applet.

## Relacionado

- [Descripción general de Antenna Genius](../../features/antenna-genius/overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Seleccionar una antena para el Puerto A o el Puerto B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
