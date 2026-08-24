# Panel de conexión

El panel de conexión es el punto de entrada principal para conectar AetherSDR a una radio FlexRadio. Ofrece tres modos de conexión: Local (descubrimiento en LAN), SmartLink (radios WAN remotas) y Manual (conexión IP directa, útil para VPN o redes enrutadas).

## Conectarse a una radio LAN local

1. Abra **Settings > Connect to Radio...**.
2. Asegúrese de que **Local** esté seleccionado en la parte superior del diálogo.
3. Espere a que la lista "Available radios" se complete con las radios descubiertas en su LAN.
4. Seleccione la radio a la que desea conectarse de la lista.
5. Haga clic en **Connect Selected Radio**.

Si no aparece ninguna radio, haga clic en **Retry Discovery** para volver a ejecutar el descubrimiento en la LAN.

### Establecer un apodo personalizado para una radio que no sea FlexRadio

Para radios que no tienen un almacén de nombres en la propia radio (p. ej., HL2, simulador), puede establecer un apodo personalizado sin necesidad de conectarse primero.

1. Abra **Settings > Connect to Radio...**.
2. Asegúrese de que **Local** esté seleccionado en la parte superior del diálogo.
3. Espere a que la lista "Available radios" se complete con las radios descubiertas en su LAN.
4. Haga clic con el botón derecho en la radio a la que desea poner apodo.
5. Seleccione **Set Nickname...** en el menú contextual.
6. Introduzca el apodo deseado en el diálogo.
7. Haga clic en **OK**.

El apodo se guarda y aparecerá en la lista de radios en los siguientes barridos de descubrimiento. Esta opción no se muestra para radios FlexRadio, cuyos nombres se establecen desde Radio Setup mientras están conectadas.

## Conectarse a una radio remota a través de SmartLink

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Remote with SmartLink** o seleccione el botón de modo **SmartLink**.
3. Introduzca el correo electrónico de su cuenta FlexRadio en el campo **Email**.
4. Introduzca la contraseña de su cuenta FlexRadio en el campo **Password**.
5. Haga clic en **Sign In**.
6. Tras una autenticación correcta, seleccione una radio de la lista **Remote radios**.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión, haga clic en **Sign Out**.

## Conexión por IP a través de una VPN o red enrutada

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Connect by IP** o seleccione el botón de modo **Manual**.
3. Introduzca la dirección IP o el nombre de host de la radio (p. ej., `ic-705.local`) en el campo **Radio IP address**.
4. (Opcional) Seleccione una interfaz de red local en el menú desplegable **Advanced: Source path** si necesita enrutar a través de una NIC específica.
5. Haga clic en **Connect by IP (manual)**.

La página Manual recuerda las últimas tres direcciones introducidas. La dirección puede ser una dirección IP numérica o un nombre de host; ambas se guardan en la lista de direcciones recientes. Anteriormente, solo se recordaban las direcciones IP numéricas, por lo que las radios VPN alcanzadas por nombre DNS no aparecían en la lista reciente.

## Opciones de conexión para enlaces más lentos

1. Abra **Settings > Connect to Radio...**.
2. Desplácese hasta la parte inferior del panel.
3. Localice la sección **Connection options for slower links**.
4. Marque **Use low bandwidth mode** para habilitar flujos de tasa reducida.
5. Marque **Enable adaptive frame-rate throttle** para reducir automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada.

## Desconectarse de la radio actual

- Haga clic en **Disconnect** en cualquier momento para terminar la conexión con la radio actual.

## Diagnóstico de red

- Haga clic en **Open Network Diagnostics** desde cualquier modo para abrir el diálogo de diagnóstico de red y solucionar problemas de conectividad.

## Deshabilitar la reconexión automática para la selección manual de radio al inicio

De forma predeterminada, AetherSDR se reconecta a la última radio utilizada cada vez que se inicia. Deshabilitar esta opción hace que AetherSDR abra el diálogo de conexión al inicio, de modo que pueda elegir una radio manualmente en cada sesión.

### Antes de comenzar

- AetherSDR debe estar en ejecución.
- No se requiere ninguna conexión de radio para cambiar esta configuración.

### Pasos

1. Haga clic en **Settings > Connect to Radio...**.
2. En el diálogo Connect to Radio, desplácese hasta la parte inferior de la página.
3. Localice la casilla de verificación denominada **Connect to last radio on start up**.
4. Desmarque **Connect to last radio on start up**.

La configuración se guarda inmediatamente en `AutoConnectToLastRadio`. La próxima vez que se inicie AetherSDR, abrirá automáticamente el diálogo de conexión en lugar de reconectarse a la última radio.

### Qué hace cada control

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Casilla "Connect to last radio on start up" | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y durante el descubrimiento por difusión / sondeo de radio enrutada. Cuando está desmarcada, se abre el diálogo de conexión y debe seleccionar una radio manualmente en cada sesión. |

### Consejos

- Esta configuración también suprime el intento de conexión automática que ocurre durante el descubrimiento por difusión y el sondeo de radio enrutada, no solo la reconexión inicial al inicio.
- Si comparte el equipo entre varias estaciones o cambia de radio con frecuencia, dejar esta opción desmarcada evita conectarse a la radio equivocada por accidente.

### Solución de problemas

- **AetherSDR aún se conecta automáticamente después de desmarcar la casilla** — Confirme que desmarcó la casilla dentro de **Settings > Connect to Radio...** y no en un diálogo diferente. La etiqueta de la casilla es exactamente "Connect to last radio on start up". Salga y reinicie AetherSDR para verificar que el cambio surte efecto.

## Resumen de todos los controles

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Botones de modo Local / SmartLink / Manual | Local | `ConnectionMode` | Cambia entre los tres modos de conexión. |
| Lista de radios disponibles | — | — | Muestra las radios LAN descubiertas mediante mDNS/Flex discovery. Haga clic con el botón derecho en una radio que no sea Flex para establecer un apodo personalizado. |
| Connect Selected Radio | — | — | Conecta con la radio LAN resaltada. |
| No local radios found yet | — | — | Aviso que se muestra cuando el descubrimiento está vacío. |
| Retry Discovery | — | — | Vuelve a ejecutar el descubrimiento en la LAN. |
| Remote with SmartLink | — | — | Acceso directo a la página SmartLink. |
| Connect by IP | — | — | Acceso directo a la página Manual. |
| Open Network Diagnostics | — | — | Abre NetworkDiagnosticsDialog. |
| Cuenta SmartLink: Email | — | `SmartLinkEmail` | Correo electrónico de la cuenta SmartLink. |
| Cuenta SmartLink: Password | — | — | Contraseña de SmartLink (no se guarda). |
| Sign In | — | — | Autentica con SmartLink. |
| Sign Out | — | — | Cierra la sesión de SmartLink. |
| Lista de radios remotas | — | — | Enumera las radios WAN SmartLink disponibles para la cuenta. |
| Connect Remote Radio | — | — | Inicia una conexión WAN con la radio seleccionada. |
| Radio IP address | — | `ManualRadioIp` | Dirección IP manual o nombre de host al que conectarse. Los nombres de host como `ic-705.local` ahora se recuerdan en la lista de direcciones recientes. |
| Advanced: Source path | — | `ManualBindSource` | Selecciona la NIC local utilizada para la conexión manual. |
| Connect by IP (manual) | — | — | Inicia la conexión manual/VPN. |
| Use low bandwidth mode | — | `LowBandwidthMode` | Habilita flujos de tasa reducida para enlaces lentos. |
| Enable adaptive frame-rate throttle | Desmarcada (False) | `AdaptiveThrottleEnabled` | Reduce automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. |
| Connect to last radio on start up | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y durante el descubrimiento por difusión / sondeo de radio enrutada. Cuando está desmarcada, se abre el diálogo de conexión y debe seleccionar una radio manualmente en cada sesión. |
| Disconnect | — | — | Desconecta de la radio actual. |

## Indicadores

| Etiqueta | Significado |
|---|---|
| Etiqueta de estado | Estado actual de la conexión (searching / connecting / connected / errored). |
| Etiqueta de resultado manual | Texto de resultado tras sondear una IP manual (éxito o error). |
| Etiqueta de advertencia de origen | Advierte cuando la NIC de origen seleccionada está obsoleta o es inalcanzable. |

## Relacionado

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
