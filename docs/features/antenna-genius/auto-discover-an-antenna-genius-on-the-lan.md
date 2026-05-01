# Descubrir automáticamente un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet Antenna Genius aparece automáticamente y se conecta sin pasos manuales.

## Antes de comenzar

- Su Antenna Genius debe estar encendido y conectado a la misma LAN que la computadora que ejecuta AetherSDR.
- El panel del applet debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. El descubrimiento comienza inmediatamente en segundo plano — no se requiere acción.
2. Cuando se encuentra un dispositivo, aparece el botón de bandeja **AG** en la barra lateral derecha. Haga clic en **AG** para abrir el applet Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivo. Mostrará **Device found** y luego cambiará a **Connected — \<name\> v\<version\>** una vez que se complete la conexión automática.
4. Confirme que el dispositivo correcto se muestra en el **Device combo**. Si hay más de un Antenna Genius en la LAN, use el combo para seleccionar el que desee y luego haga clic en **Connect**.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Clave de configuración |
|---|---|---|---|
| **Device combo** | Enumera todas las unidades Antenna Genius descubiertas mediante UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado, a menos que ese dispositivo sea un ShackSwitch (que es manejado por el applet ShackSwitch). | — | — |
| **Connect / Disconnect** | Se conecta al dispositivo seleccionado en el combo, o se desconecta si ya está conectado. La etiqueta cambia entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se utiliza cuando el dispositivo no está en la LAN local. El último valor utilizado se restaura en el próximo inicio. | — | `AG_ManualIp` |
| Etiqueta de estado | Muestra el estado de descubrimiento y conexión: **No device found**, **Device found**, **Connected — \<name\> v\<version\>**, **Disconnected**, **Error: \<msg\>** o **Invalid IP address**. | No device found | — |

## Consejos

- Si su red tiene más de un Antenna Genius, el **Device combo** enumera todas las unidades descubiertas. AetherSDR se conecta automáticamente solo al primer dispositivo descubierto que no sea un ShackSwitch. Seleccione una entrada diferente y haga clic en **Connect** para cambiar.
- Los controles del puerto B se ocultan automáticamente cuando el dispositivo conectado reporta solo un puerto de radio.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que Antenna Genius esté encendido y en la misma subred. Los firewalls o switches administrados que bloquean el tráfico de difusión UDP impedirán el descubrimiento. Si el dispositivo está en una red diferente, use **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no se pudo analizar como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — Se intentó la conexión pero el dispositivo la rechazó o cerró. Verifique que ningún otro cliente tenga una conexión exclusiva al Antenna Genius.
- **Un ShackSwitch en la LAN no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos mediante UDP son intencionalmente omitidos por el applet Antenna Genius. Use el applet ShackSwitch para conectarse a y controlar un ShackSwitch.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el puerto A o puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Habilitar el modo AUTO para que AG siga los cambios de banda de radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
