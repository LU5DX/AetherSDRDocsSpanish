# Operación remota a través de SmartLink

SmartLink le permite conectarse a un FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Esta página explica cómo iniciar sesión en su cuenta de SmartLink y conectarse a una radio remota desde la pantalla de conexión de AetherSDR.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en su firmware.
- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- AetherSDR no debe estar ya conectado a una radio. Si lo está, desconéctese primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ninguna radio conectada. También puede acceder a ella mediante `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto selecciona el modo SmartLink y muestra los controles de la cuenta SmartLink y la radio remota.
3. En el campo **SmartLink account: Email**, ingrese la dirección de correo electrónico de su cuenta FlexRadio.
4. En el campo **SmartLink account: Password**, ingrese su contraseña. La contraseña no se guarda entre sesiones.
5. Haga clic en **Sign In**. La etiqueta de estado se actualiza para mostrar el progreso de la autenticación.
6. Una vez que haya iniciado sesión, la lista **Remote radios** se completa con las radios disponibles para su cuenta. Seleccione la radio que desea utilizar.
7. Si su enlace al sitio remoto es lento (satélite, celular o banda ancha congestionada), marque **Use low bandwidth mode** antes de conectarse.
8. Haga clic en **Connect Remote Radio**. La etiqueta de estado rastrea el progreso de la conexión. Cuando la conexión sea exitosa, se abrirá la interfaz principal de AetherSDR.

## Función de cada control

| Control | Función | Configuración persistente |
|---|---|---|
| **Remote with SmartLink** (botón de modo) | Cambia la pantalla de conexión al modo SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | Correo electrónico de su cuenta FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| **Sign In** | Autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y limpia la lista de radios remotas. | — |
| **Remote radios** | Enumera las radios WAN SmartLink disponibles para la cuenta con sesión iniciada. La lista tiene una altura de visualización fija; si tiene muchas radios remotas, desplácese dentro de la lista para verlas todas. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos de transmisión para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en **Remote radios**. | — |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al inicio y durante el sondeo de descubrimiento por difusión / radio enrutada. Cuando no está marcado, se abre el cuadro de diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. El valor predeterminado es marcado. | `AutoConnectToLastRadio` |

## Conexión por IP (modo manual)

Si su radio está en una VPN o en una red enrutada que no es visible mediante el descubrimiento LAN, utilice el modo Manual en lugar de SmartLink.

1. Haga clic en **Connect by IP** en la página Local, o haga clic en el botón de modo **Manual** en la parte superior de la pantalla de conexión.
2. En el campo **Radio IP address**, escriba la dirección IP de la radio. El campo acepta direcciones IPv4 e IPv6. AetherSDR normaliza la dirección cuando se conecta.
3. El control **Radio IP address** es tanto un menú desplegable como un campo de texto. Almacena hasta tres direcciones de uso reciente (guardadas como `RecentConnectByIpAddresses`). Para reutilizar una dirección anterior, haga clic en la flecha desplegable y selecciónela de la lista.
4. Si es necesario, seleccione la interfaz de red local a utilizar en **Advanced: Source path**. Aparece una **Source warning label** debajo del selector si la interfaz elegida está obsoleta o es inaccesible.
5. Haga clic en **Connect by IP (manual)**. La **Manual result label** muestra si el sondeo fue exitoso o falló.

## Consejos

- `SmartLinkEmail` es persistente, por lo que su dirección de correo electrónico se completa previamente la próxima vez que abra la pantalla de conexión. Su contraseña no es persistente y debe ingresarse cada sesión.
- Si la lista **Remote radios** está vacía después de iniciar sesión, es posible que la radio remota no tenga SmartLink habilitado o que esté fuera de línea.
- El menú desplegable **Radio IP address** recuerda hasta tres direcciones recientes entre sesiones. Si anteriormente usó la configuración `LastRoutedRadioIp` (de una versión anterior a v0.9.7), AetherSDR la importa automáticamente a la lista de direcciones recientes en el primer inicio.
- **Connect to last radio on start up** está marcado de forma predeterminada. Si trabaja con múltiples radios y desea elegir explícitamente cada sesión, desmárquelo.

## Solución de problemas

- **La lista de radios remotas está vacía después de iniciar sesión** — Es posible que la radio en la ubicación remota esté fuera de línea o que SmartLink no esté habilitado en ella. Confirme que la radio esté encendida y registrada en la misma cuenta de FlexRadio.
- **El inicio de sesión falla o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Asegúrese de que AetherSDR tenga acceso a internet saliente y que ningún cortafuegos o proxy esté bloqueando la conexión SmartLink.
- **El audio se entrecorta o se cae con frecuencia** — Active **Use low bandwidth mode** antes de conectarse para reducir las tasas de transmisión para el enlace.
- **La conexión manual falla o la etiqueta de resultado manual muestra un error** — Confirme que la dirección IP sea correcta y accesible desde esta máquina. Verifique que la interfaz de origen seleccionada en **Advanced: Source path** esté activa; descarte cualquier **Source warning label** seleccionando una interfaz válida.
- **AetherSDR se conecta a la radio equivocada al iniciar** — Desmarque **Connect to last radio on start up** para que la pantalla de conexión se abra en cada inicio y pueda seleccionar la radio deseada.

## Relacionado

- [Connect to a Radio overview](../../features/connection/overview.md)
- [Log in to SmartLink to see remote radios](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
