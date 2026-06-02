# Panel de conexión

El panel de Conexión es el punto de entrada principal para conectar AetherSDR a un radio FlexRadio. Ofrece tres modos de conexión: Local (descubrimiento en LAN), SmartLink (radios remotas WAN) y Manual (conexión IP directa, útil para VPN o redes enrutadas).

## Conectar a un radio LAN local

1. Abra **Settings > Connect to Radio...**.
2. Asegúrese de que **Local** esté seleccionado en la parte superior del diálogo.
3. Espere a que la lista "Available radios" se complete con los radios descubiertos en su LAN.
4. Seleccione el radio al que desea conectarse de la lista.
5. Haga clic en **Connect Selected Radio**.

Si no aparece ningún radio, haga clic en **Retry Discovery** para volver a ejecutar el descubrimiento en LAN.

## Conectar a un radio remoto a través de SmartLink

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Remote with SmartLink** o seleccione el botón de modo **SmartLink**.
3. Ingrese su correo electrónico de cuenta FlexRadio en el campo **Email**.
4. Ingrese su contraseña de cuenta FlexRadio en el campo **Password**.
5. Haga clic en **Sign In**.
6. Después de la autenticación exitosa, seleccione un radio de la lista **Remote radios**.
7. Haga clic en **Connect Remote Radio**.

Para cerrar sesión, haga clic en **Sign Out**.

## Conectar por IP a través de una VPN o red enrutada

1. Abra **Settings > Connect to Radio...**.
2. Haga clic en **Connect by IP** o seleccione el botón de modo **Manual**.
3. Ingrese la dirección IP del radio en el campo **Radio IP address**.
4. (Opcional) Seleccione una interfaz de red local del menú desplegable **Advanced: Source path** si necesita enrutar a través de una NIC específica.
5. Haga clic en **Connect by IP (manual)**.

## Opciones de conexión para enlaces lentos

1. Abra **Settings > Connect to Radio...**.
2. Desplácese hasta la parte inferior del panel.
3. Localice la sección **Connection options for slower links**.
4. Marque **Use low bandwidth mode** para habilitar flujos de tasa reducida.
5. Marque **Enable adaptive frame-rate throttle** para reducir automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrade.

## Desconectar del radio actual

- Haga clic en **Disconnect** en cualquier momento para terminar la conexión con el radio actual.

## Diagnóstico de red

- Haga clic en **Open Network Diagnostics** desde cualquier modo para abrir el diálogo de Diagnóstico de red y solucionar problemas de conectividad.

## Deshabilitar la reconexión automática al radio manual al inicio

Por defecto, AetherSDR se reconecta al último radio utilizado cada vez que se inicia. Deshabilitar esto hace que AetherSDR abra el diálogo de conexión al inicio, permitiéndole seleccionar un radio manualmente en cada sesión.

### Antes de comenzar

- AetherSDR debe estar en ejecución.
- No se requiere conexión a un radio para cambiar esta configuración.

### Pasos

1. Haga clic en **Settings > Connect to Radio...**.
2. En el diálogo Conectar a Radio, desplácese hasta la parte inferior de la página.
3. Localice la casilla de verificación etiquetada **Connect to last radio on start up**.
4. Desmarque **Connect to last radio on start up**.

La configuración se guarda inmediatamente en `AutoConnectToLastRadio`. La próxima vez que AetherSDR se inicie, abrirá el diálogo de conexión automáticamente en lugar de reconectarse al último radio.

### Qué hace cada control

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Casilla "Connect to last radio on start up" | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se reconecta automáticamente al último radio usado al inicio y durante el descubrimiento por difusión / sondeo de radio enrutado. Cuando no está marcada, se abre el diálogo de conexión y debe seleccionar un radio manualmente cada sesión. |

### Consejos

- Esta configuración también suprime el intento de conexión automática que ocurre durante el descubrimiento por difusión y el sondeo de radio enrutado, no solo la reconexión inicial al inicio.
- Si comparte la computadora entre varias estaciones o cambia de radio con frecuencia, dejar esto desmarcado evita conectarse accidentalmente al radio equivocado.

### Solución de problemas

- **AetherSDR aún se reconecta automáticamente después de desmarcar la casilla** — Confirme que desmarcó la casilla dentro de **Settings > Connect to Radio...** y no en otro diálogo. La etiqueta de la casilla es exactamente "Connect to last radio on start up". Cierre y reinicie AetherSDR para verificar que el cambio surta efecto.

## Resumen de todos los controles

| Control | Valor predeterminado | Configuración persistente | Comportamiento |
|---|---|---|---|
| Botones de modo Local / SmartLink / Manual | Local | `ConnectionMode` | Cambia entre los tres modos de conexión. |
| Lista de radios disponibles | — | — | Muestra los radios LAN descubiertos mediante mDNS/Flex discovery. |
| Connect Selected Radio | — | — | Se conecta al radio LAN resaltado. |
| No local radios found yet | — | — | Aviso que se muestra cuando el descubrimiento está vacío. |
| Retry Discovery | — | — | Vuelve a ejecutar el descubrimiento en LAN. |
| Remote with SmartLink | — | — | Acceso directo a la página SmartLink. |
| Connect by IP | — | — | Acceso directo a la página Manual. |
| Open Network Diagnostics | — | — | Abre NetworkDiagnosticsDialog. |
| Cuenta SmartLink: Email | — | `SmartLinkEmail` | Correo electrónico de la cuenta SmartLink. |
| Cuenta SmartLink: Password | — | — | Contraseña SmartLink (no se persiste). |
| Sign In | — | — | Autentica con SmartLink. |
| Sign Out | — | — | Cierra sesión en SmartLink. |
| Lista de radios remotos | — | — | Enumera los radios SmartLink WAN disponibles para la cuenta. |
| Connect Remote Radio | — | — | Inicia una conexión WAN al radio seleccionado. |
| Radio IP address | — | `ManualRadioIp` | IP manual a la que conectarse. |
| Advanced: Source path | — | `ManualBindSource` | Selecciona la NIC local utilizada para la conexión manual. |
| Connect by IP (manual) | — | — | Inicia la conexión manual/VPN. |
| Use low bandwidth mode | — | `LowBandwidthMode` | Habilita flujos de tasa reducida para enlaces lentos. |
| Enable adaptive frame-rate throttle | Sin marcar (False) | `AdaptiveThrottleEnabled` | Reduce automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. |
| Connect to last radio on start up | Marcada (True) | `AutoConnectToLastRadio` | Cuando está marcada, AetherSDR se reconecta automáticamente al último radio usado al inicio y durante el descubrimiento por difusión / sondeo de radio enrutado. Cuando no está marcada, se abre el diálogo de conexión y debe seleccionar un radio manualmente cada sesión. |
| Disconnect | — | — | Desconecta del radio actual. |

## Indicadores

| Etiqueta | Significado |
|---|---|
| Status label | Estado actual de la conexión (buscando / conectando / conectado / con error). |
| Manual result label | Texto de resultado después de sondear una IP manual (éxito o error). |
| Source warning label | Advierte cuando la NIC de origen seleccionada está desactualizada o es inalcanzable. |

## Relacionados

- [Connect to a local LAN radio](connect-to-a-local-lan-radio.md)
- [Connect to a remote radio through SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Disconnect from the current radio](disconnect-from-the-current-radio.md)
