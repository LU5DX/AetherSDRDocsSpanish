# Panel de conexión

El panel de Conexión es el punto de entrada principal para conectar AetherSDR a un radio FlexRadio. Proporciona tres modos de conexión: Local (descubrimiento en LAN), SmartLink (radios remotos WAN) y Manual (conexión IP directa, útil para VPN o redes enrutadas).

## Conectarse a un radio LAN local

1. Abra **Settings > Connect to Radio...**.
2. Asegúrese de que **Local** esté seleccionado en la parte superior del diálogo.
3. Espere a que la lista "Available radios" se llene con los radios descubiertos en su LAN.
4. Seleccione el radio al que desea conectarse de la lista.
5. Haga clic en **Connect Selected Radio**.

Si no aparecen radios, haga clic en **Retry Discovery** para volver a ejecutar el descubrimiento en LAN.

### Establecer un apodo personalizado para un radio que no sea FlexRadio

Para radios que no tienen un almacén de nombres interno (por ejemplo, HL2, simulador), puede establecer un apodo personalizado sin conectarse primero.

1. Abra **Settings > Connect to Radio...**.
2. Asegúrese de que **Local** esté seleccionado en la parte superior del diálogo.
3. Espere a que la lista "Available radios" se llene con los radios descubiertos en su LAN.
4. Haga clic derecho en el radio que desea apodar.
5. Seleccione **Set Nickname...** del menú contextual.
6. Ingrese el apodo deseado en el diálogo.
7. Haga clic en **OK**.

El apodo se guarda y aparecerá en la lista de radios en posteriores exploraciones de descubrimiento. Esta opción no se muestra para radios FlexRadio, cuyos nombres se configuran desde Radio Setup mientras están conectados.

## Conectarse a un radio remoto a través de SmartLink

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Remote with SmartLink** o seleccione el botón de modo **SmartLink**.
3. Ingrese su correo electrónico de la cuenta FlexRadio en el campo **Email**.
4. Ingrese su contraseña de la cuenta FlexRadio en el campo **Password**.
5. Haga clic en **Sign In**.
6. Después de la autenticación exitosa, seleccione un radio de la lista **Remote radios**.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión, haga clic en **Sign Out**.

## Conectarse por IP a través de una VPN o red enrutada

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Connect by IP** o seleccione el botón de modo **Manual**.
3. Ingrese la dirección IP del radio en el campo **Radio IP address**.
4. (Opcional) Seleccione una interfaz de red local del menú desplegable **Advanced: Source path** si necesita enrutar a través de una NIC específica.
5. Haga clic en **Connect by IP (manual)**.

## Opciones de conexión para enlaces lentos

1. Abra **Settings > Connect to Radio...**.
2. Desplácese al final del panel.
3. Localice la sección **Connection options for slower links**.
4. Marque **Use low bandwidth mode** para habilitar flujos de tasa reducida.
5. Marque **Enable adaptive frame-rate throttle** para reducir automáticamente la velocidad de fotogramas FFT/waterfall cuando la calidad de la red se degrade.

## Desconectarse del radio actual

- Haga clic en **Disconnect** en cualquier momento para terminar la conexión con el radio actual.

## Diagnósticos de red

- Haga clic en **Open Network Diagnostics** desde cualquier modo para abrir el diálogo de Diagnósticos de red y solucionar problemas de conectividad.

## Deshabilitar la reconexión automática para selección manual de radio al inicio

De forma predeterminada, AetherSDR se reconecta al último radio utilizado cada vez que se inicia. Deshabilitar esto hace que AetherSDR abra el diálogo de conexión al inicio, para que pueda elegir un radio manualmente cada sesión.

### Antes de comenzar

- AetherSDR debe estar en ejecución.
- No se requiere ninguna conexión de radio para cambiar esta configuración.

### Pasos

1. Haga clic en **Settings > Connect to Radio...**.
2. En el diálogo Connect to Radio, desplácese al final de la página.
3. Localice la casilla de verificación etiquetada **Connect to last radio on start up**.
4. Desmarque **Connect to last radio on start up**.

La configuración se guarda inmediatamente en `AutoConnectToLastRadio`. La próxima vez que se inicie AetherSDR, abrirá automáticamente el diálogo de conexión en lugar de reconectarse al último radio.

### Qué hace cada control

| Control | Predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Casilla "Connect to last radio on start up" | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se reconecta automáticamente al último radio utilizado al inicio y durante la exploración de descubrimiento/sonda de radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y debe seleccionar un radio manualmente cada sesión. |

### Consejos

- Esta configuración también suprime el intento de conexión automática que ocurre durante el descubrimiento de difusión y la sonda de radio enrutada, no solo la reconexión inicial al inicio.
- Si comparte la computadora entre varias estaciones o cambia de radio con frecuencia, dejar esto desmarcado evita conectarse al radio equivocado accidentalmente.

### Solución de problemas

- **AetherSDR aún se reconecta automáticamente después de desmarcar la casilla** — Confirme que desmarcó la casilla dentro de **Settings > Connect to Radio...** y no en otro diálogo. La etiqueta de la casilla es exactamente "Connect to last radio on start up". Salga y reinicie AetherSDR para verificar que el cambio surta efecto.

## Resumen de todos los controles

| Control | Predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Botones de modo Local / SmartLink / Manual | Local | `ConnectionMode` | Cambia entre los tres modos de conexión. |
| Lista Available radios | — | — | Muestra los radios LAN descubiertos mediante mDNS/descubrimiento Flex. Haga clic derecho en un radio que no sea FlexRadio para establecer un apodo personalizado. |
| Connect Selected Radio | — | — | Se conecta al radio LAN resaltado. |
| No local radios found yet | — | — | Aviso que se muestra cuando el descubrimiento está vacío. |
| Retry Discovery | — | — | Vuelve a ejecutar el descubrimiento en LAN. |
| Remote with SmartLink | — | — | Atajo a la página SmartLink. |
| Connect by IP | — | — | Atajo a la página Manual. |
| Open Network Diagnostics | — | — | Abre NetworkDiagnosticsDialog. |
| Cuenta SmartLink: Email | — | `SmartLinkEmail` | Correo electrónico de la cuenta SmartLink. |
| Cuenta SmartLink: Password | — | — | Contraseña de SmartLink (no se persiste). |
| Sign In | — | — | Autentica con SmartLink. |
| Sign Out | — | — | Cierra sesión en SmartLink. |
| Lista Remote radios | — | — | Enumera los radios WAN SmartLink disponibles para la cuenta. |
| Connect Remote Radio | — | — | Inicia una conexión WAN al radio seleccionado. |
| Radio IP address | — | `ManualRadioIp` | IP manual a la que conectarse. |
| Advanced: Source path | — | `ManualBindSource` | Selecciona la NIC local utilizada para la conexión manual. |
| Connect by IP (manual) | — | — | Inicia la conexión manual/VPN. |
| Use low bandwidth mode | — | `LowBandwidthMode` | Habilita flujos de tasa reducida para enlaces lentos. |
| Enable adaptive frame-rate throttle | Sin marcar (False) | `AdaptiveThrottleEnabled` | Reduce automáticamente la velocidad de fotogramas FFT/waterfall cuando la calidad de la red se degrada. |
| Connect to last radio on start up | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se reconecta automáticamente al último radio utilizado al inicio y durante la exploración de descubrimiento/sonda de radio enrutada. Cuando no está marcada, se abre el diálogo de conexión y debe seleccionar un radio manualmente cada sesión. |
| Disconnect | — | — | Desconecta del radio actual. |

## Indicadores

| Etiqueta | Significado |
|---|---|
| Status label | Estado actual de la conexión (searching / connecting / connected / errored). |
| Manual result label | Texto de resultado después de sondear una IP manual (success o error). |
| Source warning label | Advierte cuando la NIC de origen seleccionada está obsoleta o es inaccesible. |

## Relacionados

- [Conectarse a un radio LAN local](connect-to-a-local-lan-radio.md)
- [Conectarse a un radio remoto a través de SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Desconectarse del radio actual](disconnect-from-the-current-radio.md)
