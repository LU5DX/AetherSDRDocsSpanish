# Descubrir automáticamente un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet de Antenna Genius aparece automáticamente y se conecta sin pasos manuales.

## Antes de comenzar

- Su Antenna Genius debe estar encendido y conectado a la misma LAN que el ordenador que ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. El descubrimiento comienza inmediatamente en segundo plano — no se requiere ninguna acción.
2. Cuando se encuentre un dispositivo, el botón de bandeja **AG** aparecerá en la barra lateral derecha. Haga clic en **AG** para abrir el applet de Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivos. Leerá **Device found** y luego cambiará a **Connected — \<nombre\> v\<versión\>** una vez que se complete la conexión automática.
4. Confirme que el dispositivo correcto se muestra en el **Device combo**. Si hay más de un Antenna Genius en la LAN, use el combo para seleccionar el que desee y luego haga clic en **Connect**.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Clave de ajuste |
|---|---|---|---|
| **Device combo** | Lista todas las unidades Antenna Genius descubiertas mediante UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado. | — | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el combo, o desconecta si ya está conectado. La etiqueta cambia entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectar directamente al puerto 9007. Se usa cuando el dispositivo no está en la LAN local. El último valor usado se restaura al siguiente inicio. | — | `AG_ManualIp` |
| **Botones de antena del Puerto A** | Haga clic para seleccionar una antena en el Puerto A; vuelva a hacer clic para anular la selección (antena=0). Los botones están deshabilitados/atenuados si la antena ya está seleccionada en el Puerto B. El color indica permiso: azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | — | — |
| **Puerto A AUTO** | Alterne para habilitar el seguimiento de banda en el Puerto A. Cuando está activo, el Antenna Genius cambia automáticamente las antenas a medida que la radio cambia de bandas. | — | — |
| **Botones de antena del Puerto B** | Haga clic para seleccionar una antena en el Puerto B; vuelva a hacer clic para anular la selección. Mismas reglas de color que el Puerto A. | — | — |
| **Puerto B AUTO** | Alterne para habilitar el seguimiento de banda en el Puerto B. | — | — |
| Etiqueta de estado | Muestra el estado de descubrimiento y conexión: **No device found**, **Device found**, **Connected — \<nombre\> v\<versión\>**, **Disconnected**, **Error: \<mensaje\>** o **Invalid IP address**. | No device found | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Puerto A banda** | Nombre de la banda o **—** | Banda activa en el Puerto A, según lo informado por el Antenna Genius o derivado de la frecuencia de la radio. |
| **Puerto A antena** | Nombre de la antena, **\<ant\> TX:\<alt\>**, **\<ant\> [INHIBIT]** o **—** | Antena seleccionada para el Puerto A. Muestra rojo cuando está transmitiendo, naranja cuando TX se enruta a una antena alternativa o se activa la inhibición. |
| **Puerto B banda** | Nombre de la banda o **—** | Banda activa en el Puerto B. |
| **Puerto B antena** | Nombre de la antena, **\<ant\> TX:\<alt\>**, **\<ant\> [INHIBIT]** o **—** | Antena seleccionada para el Puerto B. |

## Consejos

- Si su red tiene más de un Antenna Genius, el **Device combo** lista todas las unidades descubiertas. AetherSDR se conecta automáticamente solo al primer dispositivo descubierto. Seleccione una entrada diferente y haga clic en **Connect** para cambiar.
- Los controles del Puerto B se ocultan automáticamente cuando el dispositivo conectado informa solo un puerto de radio.
- Los botones de antena están codificados por colores para mostrar permisos de TX/RX: los botones azules permiten tanto transmisión como recepción en la banda actual, los botones ámbar permiten solo recepción y los botones atenuados indican que no hay permiso en la banda actual.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que el Antenna Genius esté encendido y en la misma subred. Los cortafuegos o switches administrados que bloquean el tráfico de difusión UDP impedirán el descubrimiento. Si el dispositivo está en una red diferente, use **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no pudo analizarse como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<mensaje\>"** — Se intentó la conexión pero el dispositivo la rechazó o la interrumpió. Verifique que ningún otro cliente tenga una conexión exclusiva con el Antenna Genius.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
