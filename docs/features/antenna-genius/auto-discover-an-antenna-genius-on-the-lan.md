# Detectar automáticamente un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante detección UDP. Cuando se encuentra un dispositivo, el applet de Antenna Genius aparece automáticamente y se conecta sin pasos manuales.

## Antes de comenzar

- Su Antenna Genius debe estar encendido y conectado a la misma LAN que la computadora que ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. La detección comienza inmediatamente en segundo plano (no requiere ninguna acción).
2. Cuando se encuentre un dispositivo, el botón de la bandeja **AG** aparecerá en la barra lateral derecha. Haga clic en **AG** para abrir el applet de Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivos. Mostrará **Device found** y luego cambiará a **Connected — \<name\> v\<version\>** una vez que la conexión automática se complete.
4. Confirme que el dispositivo correcto se muestre en el **Device combo**. Si hay más de un Antenna Genius en la LAN, use el combo para seleccionar el que desee y luego haga clic en **Connect**.

## Función de cada control

| Control | Función | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Device combo** | Lista todas las unidades Antenna Genius detectadas mediante UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado, a menos que ese dispositivo sea un ShackSwitch (gestionado por el applet ShackSwitch). | — | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el combo, o desconecta si ya está conectado. La etiqueta cambia entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se usa cuando el dispositivo no está en la LAN local. El último valor usado se restaura en el próximo inicio. | — | `AG_ManualIp` |
| Etiqueta de estado | Muestra el estado de detección y conexión: **No device found**, **Device found**, **Connected — \<name\> v\<version\>**, **Disconnected**, **Error: \<msg\>** o **Invalid IP address**. | No device found | — |

## Consejos

- Si su red tiene más de un Antenna Genius, el **Device combo** lista todas las unidades detectadas. AetherSDR se conecta automáticamente solo al primer dispositivo descubierto que no sea un ShackSwitch. Seleccione una entrada diferente y haga clic en **Connect** para cambiar.
- Los controles del Puerto B se ocultan automáticamente cuando el dispositivo conectado reporta solo un puerto de radio.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que el Antenna Genius esté encendido y en la misma subred. Los cortafuegos o switches administrados que bloquean el tráfico de difusión UDP impedirán la detección. Si el dispositivo está en una red diferente, use **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no pudo interpretarse como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — Se intentó la conexión pero el dispositivo la rechazó o la interrumpió. Verifique que ningún otro cliente tenga una conexión exclusiva con el Antenna Genius.
- **Un ShackSwitch en la LAN no se conecta automáticamente aquí** — Los dispositivos ShackSwitch detectados mediante UDP son omitidos intencionalmente por el applet de Antenna Genius. Use el applet ShackSwitch para conectarse y controlar un ShackSwitch.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
