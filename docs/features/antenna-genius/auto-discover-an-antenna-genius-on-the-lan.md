# Descubrimiento automático de un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet Antenna Genius aparece automáticamente y se conecta sin ningún paso manual.

## Antes de comenzar

- El Antenna Genius debe estar encendido y conectado a la misma LAN que el equipo donde se ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. El descubrimiento comienza de inmediato en segundo plano — no se requiere ninguna acción.
2. Cuando se encuentra un dispositivo, el botón de bandeja **AG** aparece en la barra lateral derecha. Haga clic en **AG** para abrir el applet Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivo. Mostrará **Device found** y luego cambiará a **Connected — \<name\> v\<version\>** una vez que la conexión automática se complete.
4. Confirme que el dispositivo correcto aparece en el **Device combo**. Si hay más de un Antenna Genius en la LAN, utilice el combo para seleccionar el que desea y luego haga clic en **Connect**.

## Qué hace cada control

| Control | Función | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Device combo** | Lista todas las unidades Antenna Genius descubiertas mediante UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado. | — | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el combo, o desconecta si ya está conectado. La etiqueta alterna entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se utiliza cuando el dispositivo no está en la LAN local. El último valor ingresado se restaura al siguiente inicio. | — | `AG_ManualIp` |
| Etiqueta de estado | Muestra el estado de descubrimiento y conexión: **No device found**, **Device found**, **Connected — \<name\> v\<version\>**, **Disconnected**, **Error: \<msg\>**, o **Invalid IP address**. | No device found | — |

## Consejos

- Si su red tiene más de un Antenna Genius, el **Device combo** lista todas las unidades descubiertas. AetherSDR se conecta automáticamente solo a la primera que encuentra. Seleccione una entrada diferente y haga clic en **Connect** para cambiar.
- Los controles del puerto B se ocultan automáticamente cuando el dispositivo conectado reporta un solo puerto de radio.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que el Antenna Genius esté encendido y en la misma subred. Los cortafuegos o conmutadores administrados que bloquean el tráfico de difusión UDP impedirán el descubrimiento. Si el dispositivo está en una red diferente, utilice **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no pudo interpretarse como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — Se realizó el intento de conexión, pero el dispositivo lo rechazó o lo interrumpió. Verifique que ningún otro cliente mantenga una conexión exclusiva con el Antenna Genius.

## Relacionados

- [Descripción general del Antenna Genius](overview.md)
- [Conectar manualmente un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el puerto A o el puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda del radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
