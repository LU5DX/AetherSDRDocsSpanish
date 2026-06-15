# Conectar manualmente a un AG a través de una red remota

Utilice esta página para conectar AetherSDR a un Antenna Genius que no está en la LAN local — por ejemplo, a través de una VPN o una red enrutada — ingresando su dirección IP directamente. La detección por UDP solo funciona en la subred local, por lo que se requiere una entrada IP manual para dispositivos remotos.

## Antes de comenzar

- El Antenna Genius debe ser accesible desde su equipo en el puerto TCP 9007. Confirme esto con su configuración de red o VPN antes de proceder.
- El applet de Antenna Genius está oculto hasta que se descubre un dispositivo o se conecta manualmente. Si no ve el botón de la bandeja AG en la barra lateral derecha, es normal; aparecerá después de una conexión exitosa.

## Pasos

1. Abra el panel de applets. Si no está visible, haga clic en `View > Applet Panel`.
2. Busque el botón de la bandeja AG en la barra lateral derecha. Si el applet ya está abierto, omita el paso 4.
3. Si aún no hay ningún botón de la bandeja AG visible, continúe con los pasos restantes; el botón aparece una vez que se establece una conexión.
4. En el applet de Antenna Genius, localice el campo **IP manual** (etiquetado como "Manual IP:").
5. Escriba la dirección IPv4 o IPv6 del Antenna Genius remoto en el campo **IP manual**.
6. Presione **Enter**. AetherSDR valida la dirección y se conecta al puerto 9007.
7. Observe la etiqueta de estado debajo del cuadro combinado del dispositivo. Una conexión exitosa muestra `Connected — <nombre> v<versión>`. Una conexión inalcanzable o rechazada muestra `Error: <msg>`.

## Función de cada control

| Control | Lo que hace | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Cuadro combinado de dispositivo** | Selecciona a qué dispositivo AG descubierto conectarse. Se selecciona y conecta automáticamente cuando se descubre el primer dispositivo. | _(completado desde la detección UDP)_ | Completado desde la detección UDP | — |
| **Conectar / Desconectar** | Conecta al dispositivo seleccionado en el cuadro combinado de dispositivo, o a la dirección IP manual si no hay ningún dispositivo descubierto seleccionado. Se convierte en Desconectar cuando está conectado. | Conectar | — | — |
| **IP manual** | Almacena y usa una dirección IP para conectar directamente, omitiendo la detección UDP. Presionar Enter inicia el intento de conexión. | _(en blanco)_ | Dirección IPv4 o IPv6 | `AG_ManualIp` |
| **Botones de antena del Puerto A** | Haga clic para seleccionar una antena en el Puerto A; haga clic de nuevo para anular la selección (antena=0). Deshabilitados/atenuados si la antena ya está seleccionada en el Puerto B. Azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | — | Completado desde la lista de antenas del AG | — |
| **AUTO del Puerto A** | Habilita el seguimiento de banda en el Puerto A. | — | — | — |
| **Botones de antena del Puerto B** | Haga clic para seleccionar una antena en el Puerto B; haga clic de nuevo para anular la selección. La sección del Puerto B está oculta si el dispositivo AG informa solo un puerto de radio. | — | Misma lista de antenas que el Puerto A | — |
| **AUTO del Puerto B** | Habilita el seguimiento de banda en el Puerto B. | — | — | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | No device found, Device found, Connected — \<nombre\> v\<versión\>, Disconnected, Error: \<msg\>, Invalid IP address | Estado de detección/conexión del Antenna Genius. |
| Banda del Puerto A | Nombre de banda o '—' | Banda activa en el Puerto A (reportada por el AG o derivada de la frecuencia). |
| Antena del Puerto A | Nombre de antena, \<ant\> TX:\<alt\>, \<ant\> [INHIBIT], '—' | Antena seleccionada; roja al transmitir, ámbar cuando la TX se enruta a una antena alternativa o se afirma la inhibición. |
| Banda del Puerto B | Nombre de banda o '—' | Banda activa en el Puerto B. |
| Antena del Puerto B | Nombre de antena, \<ant\> TX:\<alt\>, \<ant\> [INHIBIT], '—' | Antena seleccionada para el Puerto B. |

## Consejos

- AetherSDR guarda la última dirección utilizada en `AG_ManualIp` cuando presiona Enter. El campo se rellena previamente con esa dirección la próxima vez que abra el applet.
- Si el cuadro combinado de dispositivo contiene un dispositivo descubierto, al hacer clic en Conectar se conecta a ese dispositivo, no a la IP manual. Borre o ignore la selección del cuadro combinado si desea que la IP manual surta efecto a través del botón Conectar. Presionar Enter en el campo IP manual siempre usa la dirección escrita, independientemente del estado del cuadro combinado.
- El Puerto B se oculta automáticamente si el Antenna Genius conectado informa solo un puerto de radio.
- La conexión automática al detectar se aplica solo a dispositivos Antenna Genius. Si se descubre un ShackSwitch en la misma red, no se conecta automáticamente desde este applet; lo maneja el applet de ShackSwitch.
- La cuadrícula de botones de antena se limpia cuando el dispositivo se desconecta y se reconstruye cuando se establece una conexión. Esto garantiza que la visualización y el modelo permanezcan coherentes mientras está desconectado.
- Los botones de antena no se reconstruyen hasta que el modelo haya cargado la lista de antenas. Si la cuadrícula aparece en blanco brevemente después de conectar, espere a que llegue la lista de antenas desde el dispositivo.

## Solución de problemas

- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **IP manual** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — AetherSDR llegó a la capa de red pero no pudo completar la conexión. Verifique que el puerto 9007 esté abierto y que el Antenna Genius esté encendido y accesible en la dirección que ingresó.
- **El botón de la bandeja AG nunca aparece** — El applet permanece oculto hasta que se establece una conexión. Revise la etiqueta de estado dentro del panel del applet para obtener detalles del error. Si el panel en sí no es visible, actívelo a través de `View > Applet Panel`.
- **Un dispositivo descubierto no se conecta automáticamente** — Si el primer dispositivo descubierto en la LAN es un ShackSwitch, el applet de Antenna Genius no se conectará automáticamente a él. El applet de ShackSwitch maneja ese dispositivo. Verifique si hay un dispositivo Antenna Genius independiente en su red.
- **La cuadrícula de botones de antena está en blanco después de conectar** — Esto es normal si la lista de antenas aún no se ha cargado. Espere unos segundos para que el modelo reciba la lista de antenas del dispositivo. Si la cuadrícula permanece en blanco, desconecte y vuelva a conectar.

## Relacionados

- [Descripción general de Antenna Genius](../../features/antenna-genius/overview.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
