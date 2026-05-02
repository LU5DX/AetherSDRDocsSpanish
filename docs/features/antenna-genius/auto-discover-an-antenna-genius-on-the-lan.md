# Detección automática de un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet Antenna Genius aparece automáticamente y se conecta sin ningún paso manual.

## Antes de comenzar

- El Antenna Genius debe estar encendido y conectado a la misma LAN que el equipo donde se ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. El descubrimiento comienza de inmediato en segundo plano — no se requiere ninguna acción.
2. Cuando se encuentre un dispositivo, el botón **AG** aparece en la barra lateral derecha. Haga clic en **AG** para abrir el applet Antenna Genius.
3. Verifique la etiqueta de estado que aparece debajo del selector de dispositivos. Mostrará **Device found** y luego cambiará a **Connected — \<name\> v\<version\>** una vez que se complete la conexión automática.
4. Confirme que el dispositivo correcto aparece en el **Device combo**. Si hay más de un Antenna Genius en la LAN, use el combo para seleccionar el que desea y haga clic en **Connect**.

## Función de cada control

| Control | Función | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Device combo** | Muestra todas las unidades Antenna Genius descubiertas por UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado, a menos que ese dispositivo sea un ShackSwitch (que es gestionado por el applet ShackSwitch). | — | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el combo o desconecta si ya hay una conexión activa. La etiqueta alterna entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se utiliza cuando el dispositivo no está en la LAN local. El último valor utilizado se restaura al siguiente inicio. | — | `AG_ManualIp` |
| Etiqueta de estado | Muestra el estado de descubrimiento y conexión: **No device found**, **Device found**, **Connected — \<name\> v\<version\>**, **Disconnected**, **Error: \<msg\>** o **Invalid IP address**. | No device found | — |

## Sugerencias

- Si su red tiene más de un Antenna Genius, el **Device combo** muestra todas las unidades descubiertas. AetherSDR se conecta automáticamente solo al primer dispositivo descubierto que no sea un ShackSwitch. Seleccione una entrada diferente y haga clic en **Connect** para cambiar.
- Los controles del puerto B se ocultan automáticamente cuando el dispositivo conectado reporta únicamente un puerto de radio.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que el Antenna Genius esté encendido y en la misma subred. Los cortafuegos o conmutadores administrados que bloquean el tráfico de difusión UDP impedirán el descubrimiento. Si el dispositivo está en una red diferente, use **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no pudo interpretarse como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — Se realizó el intento de conexión, pero el dispositivo lo rechazó o lo interrumpió. Verifique que ningún otro cliente mantenga una conexión exclusiva con el Antenna Genius.
- **Un ShackSwitch en la LAN no se conecta automáticamente aquí** — Los dispositivos ShackSwitch descubiertos por UDP son omitidos intencionalmente por el applet Antenna Genius. Use el applet ShackSwitch para conectarse y controlar un ShackSwitch.

## Temas relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el puerto A o el puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
