# Conectarse manualmente a un AG a través de una red remota

Use esta página para conectar AetherSDR a un Antenna Genius que no está en la LAN local — por ejemplo, a través de una VPN o una red enrutada — ingresando su dirección IP directamente. La detección por UDP solo funciona en la subred local, por lo que se requiere una entrada IP manual para dispositivos remotos.

## Antes de comenzar

- El Antenna Genius debe ser accesible desde su máquina a través del puerto TCP 9007. Confirme esto con su configuración de red o VPN antes de continuar.
- El applet de Antenna Genius está oculto hasta que se detecta un dispositivo o se conecta manualmente. Si no ve el botón de la bandeja AG en la barra lateral derecha, es normal; aparecerá después de una conexión exitosa.

## Pasos

1. Abra el panel de applets. Si no está visible, haga clic en `View > Applet Panel`.
2. Busque el botón de la bandeja AG en la barra lateral derecha. Si el applet ya está abierto, continúe con el paso 4.
3. Si aún no hay ningún botón de la bandeja AG visible, continúe con los pasos restantes; el botón aparece una vez que se establece una conexión.
4. En el applet de Antenna Genius, localice el campo **Manual IP** (etiquetado como "Manual IP:").
5. Escriba la dirección IPv4 o IPv6 del Antenna Genius remoto en el campo **Manual IP**.
6. Presione **Enter**. AetherSDR valida la dirección y se conecta al puerto 9007.
7. Observe la etiqueta de estado debajo del cuadro combinado del dispositivo. Una conexión exitosa muestra `Connected — <name> v<version>`. Una conexión inalcanzable o rechazada muestra `Error: <msg>`.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Device combo** | Selecciona a qué dispositivo AG detectado conectarse. Se autoselecciona y conecta cuando se detecta el primer dispositivo. | _(poblado desde detección UDP)_ | Poblado desde detección UDP | — |
| **Connect / Disconnect** | Conecta al dispositivo seleccionado en el cuadro combinado Device, o a la dirección IP Manual si no hay ningún dispositivo detectado seleccionado. Cambia a Disconnect cuando está conectado. | Connect | — | — |
| **Manual IP** | Almacena y usa una dirección IP para conectarse directamente, omitiendo la detección UDP. Presionar Enter inicia el intento de conexión. | _(en blanco)_ | Dirección IPv4 o IPv6 | `AG_ManualIp` |
| **Botones de antena del Puerto A** | Haga clic para seleccionar una antena en el Puerto A; haga clic nuevamente para deseleccionar (antena=0). Deshabilitados/atenuados si la antena ya está seleccionada en el Puerto B. Azul = TX+RX, ámbar = solo RX, atenuado = sin permiso en la banda actual. | — | Poblado desde la lista de antenas del AG | — |
| **Puerto A AUTO** | Habilita el seguimiento de banda en el Puerto A. | — | — | — |
| **Botones de antena del Puerto B** | Haga clic para seleccionar una antena en el Puerto B; haga clic nuevamente para deseleccionar. La sección del Puerto B está oculta si el dispositivo AG informa solo un puerto de radio. | — | Misma lista de antenas que el Puerto A | — |
| **Puerto B AUTO** | Habilita el seguimiento de banda en el Puerto B. | — | — | — |

## Indicadores

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | No device found, Device found, Connected — \<name\> v\<version\>, Disconnected, Error: \<msg\>, Invalid IP address | Estado de detección/conexión del Antenna Genius. |
| Puerto A banda | Nombre de banda o '—' | Banda activa en el Puerto A (reportada por el AG o derivada de la frecuencia). |
| Puerto A antena | Nombre de antena, \<ant\> TX:\<alt\>, \<ant\> [INHIBIT], '—' | Antena seleccionada; rojo al transmitir, ámbar cuando TX se enruta a una antena alternativa o se afirma la inhibición. |
| Puerto B banda | Nombre de banda o '—' | Banda activa en el Puerto B. |
| Puerto B antena | Nombre de antena, \<ant\> TX:\<alt\>, \<ant\> [INHIBIT], '—' | Antena seleccionada para el Puerto B. |

## Consejos

- AetherSDR guarda la última dirección utilizada en `AG_ManualIp` cuando presiona Enter. El campo se rellena previamente con esa dirección la próxima vez que abra el applet.
- Si el cuadro combinado **Device** contiene un dispositivo detectado, al hacer clic en **Connect** se conecta a ese dispositivo, no a la IP Manual. Limpie o ignore la selección del cuadro combinado si desea que la IP Manual surta efecto a través del botón **Connect**. Presionar Enter en el campo **Manual IP** siempre usa la dirección escrita, independientemente del estado del cuadro combinado.
- El Puerto B se oculta automáticamente una vez que el Antenna Genius informa su número de puertos de radio. Para conexiones de IP manual, esto ocurre cuando se recibe la respuesta de información. Para dispositivos detectados, esto ocurre cuando se recibe una baliza UDP. El Puerto B puede permanecer visible brevemente después de la conexión hasta que el dispositivo informe que tiene solo un puerto.
- La reconexión automática al detectar se aplica solo a dispositivos Antenna Genius. Si se detecta un ShackSwitch en la misma red, no se conecta automáticamente desde este applet; lo maneja el applet de ShackSwitch.
- La cuadrícula de botones de antena se limpia cuando el dispositivo se desconecta y se reconstruye cuando se establece una conexión. Esto asegura que la pantalla y el modelo permanezcan consistentes mientras está desconectado.
- Los botones de antena no se reconstruyen hasta que el modelo haya cargado la lista de antenas. Si la cuadrícula aparece en blanco brevemente después de conectarse, espere a que llegue la respuesta de la lista de antenas del dispositivo.

## Solución de problemas

- **La etiqueta de estado muestra "Invalid IP address"** — El texto ingresado en **Manual IP** no es una dirección IPv4 o IPv6 válida. Corrija la dirección y presione Enter nuevamente.
- **La etiqueta de estado muestra "Error: \<msg\>"** — AetherSDR llegó a la capa de red pero no pudo completar la conexión. Verifique que el puerto 9007 esté abierto y que el Antenna Genius esté encendido y accesible en la dirección que ingresó.
- **El botón de la bandeja AG nunca aparece** — El applet permanece oculto hasta que se establece una conexión. Verifique la etiqueta de estado dentro del panel del applet para obtener detalles del error. Si el panel en sí no está visible, actívelo a través de `View > Applet Panel`.
- **Un dispositivo detectado no se conecta automáticamente** — Si el primer dispositivo detectado en la LAN es un ShackSwitch, el applet de Antenna Genius no se conectará automáticamente a él. El applet de ShackSwitch maneja ese dispositivo. Verifique si hay un dispositivo Antenna Genius separado presente en su red.
- **La cuadrícula de botones de antena está en blanco después de conectarse** — Esto es normal si la lista de antenas aún no se ha cargado. Espere unos segundos para que el modelo reciba la lista de antenas del dispositivo. Si la cuadrícula permanece en blanco, desconéctese y vuelva a conectarse.

## Relacionado

- [Resumen de Antenna Genius](../../features/antenna-genius/overview.md)
- [Detectar automáticamente un Antenna Genius en la LAN](../../features/antenna-genius/auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](../../features/antenna-genius/select-an-antenna-for-port-a-or-port-b.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](../../features/antenna-genius/enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
