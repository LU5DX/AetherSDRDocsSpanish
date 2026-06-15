# Descubrir automáticamente un Antenna Genius en la LAN

AetherSDR escucha dispositivos 4O3A Antenna Genius en su red local mediante detección por UDP. Cuando se encuentra un dispositivo, el applet Antenna Genius aparece automáticamente y se conecta sin necesidad de pasos manuales.

## Antes de comenzar

- Su Antenna Genius debe estar encendido y conectado a la misma LAN que el equipo que ejecuta AetherSDR.
- El panel de applets debe estar visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Inicie AetherSDR. La detección comienza inmediatamente en segundo plano, sin necesidad de ninguna acción.
2. Cuando se encuentre un dispositivo, el botón de bandeja **AG** aparecerá en la barra lateral derecha. Haga clic en **AG** para abrir el applet de Antenna Genius.
3. Verifique la etiqueta de estado debajo del selector de dispositivos. Leerá **Device found** y luego cambiará a **Connected — \<nombre\> v\<versión\>** una vez que se complete la conexión automática.
4. Confirme que el dispositivo correcto aparece en el **combo de dispositivos**. Si hay más de un Antenna Genius en la LAN, use el combo para seleccionar el que desee y luego haga clic en **Connect**.

## Función de cada control

| Control | Función | Predeterminado | Clave de configuración |
|---|---|---|---|
| **Device combo** | Lista todas las unidades Antenna Genius detectadas mediante UDP. Selecciona y conecta automáticamente al primer dispositivo encontrado. | — | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el combo, o desconecta si ya está conectado. La etiqueta cambia entre **Connect** y **Disconnect** para reflejar el estado actual. | Connect | — |
| **Manual IP** | Introduzca una dirección IPv4 o IPv6 y presione Enter para conectarse directamente al puerto 9007. Se utiliza cuando el dispositivo no está en la LAN local. El último valor usado se restaura en el próximo inicio. | — | `AG_ManualIp` |
| **Botones de antena del Puerto A** | Haga clic para seleccionar una antena en el Puerto A; haga clic de nuevo para anular la selección (antena=0). Los botones se deshabilitan/atenúan si la antena ya está seleccionada en el Puerto B. El color indica el permiso: azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | — | — |
| **Puerto A AUTO** | Active para habilitar el seguimiento de banda en el Puerto A. Cuando está activo, el Antenna Genius cambia automáticamente las antenas a medida que la radio cambia de banda. | — | — |
| **Botones de antena del Puerto B** | Haga clic para seleccionar una antena en el Puerto B; haga clic de nuevo para anular la selección. Mismas reglas de color que el Puerto A. | — | — |
| **Puerto B AUTO** | Active para habilitar el seguimiento de banda en el Puerto B. | — | — |
| Etiqueta de estado | Muestra el estado de detección y conexión: **No device found**, **Device found**, **Connected — \<nombre\> v\<versión\>**, **Disconnected**, **Error: \<mensaje\>** o **Invalid IP address**. | No device found | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| **Banda Puerto A** | Nombre de banda o **—** | Banda activa en el Puerto A, según lo informado por el Antenna Genius o derivado de la frecuencia de la radio. |
| **Antena Puerto A** | Nombre de antena, **\<ant\> TX:\<alt\>**, **\<ant\> [INHIBIT]** o **—** | Antena seleccionada para el Puerto A. Muestra rojo al transmitir, naranja cuando TX se enruta a una antena alternativa o se afirma la inhibición. |
| **Banda Puerto B** | Nombre de banda o **—** | Banda activa en el Puerto B. |
| **Antena Puerto B** | Nombre de antena, **\<ant\> TX:\<alt\>**, **\<ant\> [INHIBIT]** o **—** | Antena seleccionada para el Puerto B. |

## Consejos

- Si su red tiene más de un Antenna Genius, el **combo de dispositivos** lista todas las unidades descubiertas. AetherSDR se conecta automáticamente solo al primer dispositivo descubierto. Seleccione otra entrada y haga clic en **Connect** para cambiar.
- Los controles del Puerto B se ocultan automáticamente cuando el dispositivo conectado informa solo un puerto de radio.
- Los botones de antena tienen códigos de color para mostrar los permisos TX/RX: los botones azules permiten transmitir y recibir en la banda actual, los botones ámbar permiten solo recibir y los botones atenuados indican que no hay permiso en la banda actual.
- La cuadrícula de botones de antena se limpia por completo al desconectarse para mantener la pantalla coherente. Al reconectarse, los botones se reconstruyen a partir de la lista de antenas del dispositivo solo después de que la lista se haya cargado por completo; la cuadrícula no aparecerá en blanco mientras espera la respuesta.

## Solución de problemas

- **La etiqueta de estado permanece en "No device found"** — Verifique que el Antenna Genius esté encendido y en la misma subred. Los cortafuegos o conmutadores administrados que bloquean el tráfico de difusión UDP impedirán la detección. Si el dispositivo está en una red diferente, use **Manual IP** en su lugar.
- **La etiqueta de estado muestra "Invalid IP address"** — El texto introducido en **Manual IP** no pudo interpretarse como una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<mensaje\>"** — Se intentó la conexión, pero el dispositivo la rechazó o la interrumpió. Verifique que ningún otro cliente tenga una conexión exclusiva con el Antenna Genius.

## Relacionado

- [Descripción general de Antenna Genius](overview.md)
- [Conectar manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
