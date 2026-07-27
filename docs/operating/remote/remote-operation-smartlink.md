# Operación remota a través de SmartLink

SmartLink le permite conectarse a un FLEX-8600 que se encuentra en una ubicación diferente a la de su computadora. Esta página cubre cómo iniciar sesión en su cuenta de SmartLink y conectarse a una radio remota desde la pantalla de conexión de AetherSDR.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en su firmware.
- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- AetherSDR no debe estar ya conectado a una radio. Si lo está, desconéctelo primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ninguna radio conectada. También puede acceder a ella a través de `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto selecciona el modo SmartLink y muestra los controles de la cuenta SmartLink y de la radio remota.
3. En el campo **SmartLink account: Email**, introduzca la dirección de correo electrónico de su cuenta FlexRadio.
4. En el campo **SmartLink account: Password**, introduzca su contraseña. La contraseña no se guarda entre sesiones. El campo está etiquetado con nombres de accesibilidad para gestores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet).
5. Haga clic en **Sign In**. La etiqueta de estado se actualiza para mostrar el progreso de la autenticación.
6. Una vez que haya iniciado sesión, la lista **Remote radios** se completa con las radios disponibles para su cuenta. Seleccione la radio que desea utilizar.
7. Si su enlace al sitio remoto es lento (satélite, celular o banda ancha congestionada), marque **Use low bandwidth mode** antes de conectarse.
8. Haga clic en **Connect Remote Radio**. La etiqueta de estado rastrea el progreso de la conexión. Cuando la conexión se realiza correctamente, se abre la interfaz principal de AetherSDR.

## Función de cada control

| Control | Función | Configuración persistida |
|---|---|---|
| **Local / SmartLink / Manual** (botones de modo) | Cambia la pantalla de conexión entre los tres modos de conexión. Cada botón está identificado en el árbol de accesibilidad para admitir pruebas automatizadas. | `ConnectionMode` |
| **Remote with SmartLink** (botón de modo) | Cambia la pantalla de conexión al modo SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | Correo electrónico de su cuenta FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| **Sign In** | Se autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios remotas. | — |
| **Remote radios** | Enumera las radios WAN SmartLink disponibles para la cuenta que ha iniciado sesión. La lista tiene una altura de visualización fija; si tiene muchas radios remotas, desplácese dentro de la lista para verlas todas. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos de transmisión para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Enable adaptive frame-rate throttle** | Reduce automáticamente la velocidad de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. | `AdaptiveThrottleEnabled` |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en **Remote radios**. | — |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio utilizada al iniciar y en el descubrimiento de difusión/sonda de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente cada sesión. Marcado por defecto. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta la radio actual y vuelve a la pantalla de conexión. | — |

## Conexión por IP (Modo manual)

Si su radio está en una VPN o una red enrutada que no es visible a través del descubrimiento LAN, use el modo Manual en lugar de SmartLink.

1. Haga clic en **Connect by IP** en la página Local, o haga clic en el botón de modo **Manual** en la parte superior de la pantalla de conexión.
2. En el campo **Radio IP address**, escriba la dirección IP de la radio. El campo acepta direcciones IPv4 e IPv6. AetherSDR normaliza la dirección cuando se conecta.
3. El control **Radio IP address** es un menú desplegable además de un campo de texto. Almacena hasta tres direcciones utilizadas recientemente (guardadas como `RecentConnectByIpAddresses`). Para reutilizar una dirección anterior, haga clic en la flecha desplegable y selecciónela de la lista.
4. Si es necesario, seleccione la interfaz de red local que se usará en **Advanced: Source path**. Aparece una **Source warning label** debajo del selector si la interfaz elegida está obsoleta o es inalcanzable.
5. Haga clic en **Connect by IP (manual)**. La **Manual result label** muestra si la sonda tuvo éxito o falló.

## Gestión de apodos de radio

Haga clic derecho en cualquier radio de la lista **Available radios** en la página Local para establecer un apodo personalizado. Esto es útil para distinguir entre varias radios que reportan nombres de descubrimiento similares. El apodo se guarda asociado al número de serie y aparece en futuros barridos de descubrimiento. Esta función solo está disponible para radios que no tienen un almacén de nombres en la propia radio (como HL2 o radios simuladas); las radios FlexRadio establecen su nombre desde la configuración de radio mientras están conectadas y no se ven afectadas por los apodos del lado del cliente.

## Consejos

- `SmartLinkEmail` se conserva, por lo que su dirección de correo electrónico se rellena previamente la próxima vez que abra la pantalla de conexión. Su contraseña no se conserva y debe introducirse cada sesión.
- Si la lista **Remote radios** está vacía después de iniciar sesión, es posible que la radio remota no tenga SmartLink habilitado o que esté fuera de línea.
- El menú desplegable **Radio IP address** recuerda hasta tres direcciones recientes entre sesiones. Si usó anteriormente la configuración `LastRoutedRadioIp` (de una versión anterior a v0.9.7), AetherSDR la importa automáticamente a la lista de direcciones recientes en el primer inicio.
- **Connect to last radio on start up** está marcado por defecto. Si trabaja con varias radios y desea elegir explícitamente cada sesión, desmárquelo.
- El formulario de inicio de sesión de SmartLink está identificado en el árbol de accesibilidad como "SmartLink account login", lo que facilita que los gestores de contraseñas asocien los campos de credenciales con este formulario de inicio de sesión específico.
- La casilla de verificación **Enable adaptive frame-rate throttle** no está marcada por defecto. Cuando está habilitada, AetherSDR reduce automáticamente la velocidad de fotogramas de FFT y waterfall cuando la calidad de la red se degrada, lo que ayuda a mantener una conexión estable en enlaces de calidad variable.
- La lista **Available radios** en la página Local tiene una altura máxima fija para que la lista se desplace internamente cuando se descubren muchas radios. En pantallas pequeñas (por ejemplo, un panel de 1024×600), esto evita que el botón Connect y las radios inferiores se vuelvan inalcanzables. La lista muestra una barra de desplazamiento vertical según sea necesario.
- Los menús contextuales con clic derecho en la lista **Available radios** son leídos por los lectores de pantalla y se informan como "available local radios" con una descripción accesible de "Discovered FlexRadio radios on the local network".

## Solución de problemas

- **La lista de radios remotas está vacía después de iniciar sesión** — La radio en la ubicación remota puede estar fuera de línea o SmartLink puede no estar habilitado en ella. Confirme que la radio esté encendida y registrada en la misma cuenta de FlexRadio.
- **El inicio de sesión falla o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Asegúrese de que AetherSDR tenga acceso a internet de salida y que ningún cortafuegos o proxy esté bloqueando la conexión SmartLink.
- **El audio es entrecortado o se corta con frecuencia** — Active **Use low bandwidth mode** antes de conectarse para reducir las tasas de transmisión para el enlace. Para conexiones de calidad variable, active también **Enable adaptive frame-rate throttle** para ajustar automáticamente las tasas de actualización de la pantalla.
- **La conexión manual falla o la etiqueta de resultado manual muestra un error** — Confirme que la dirección IP sea correcta y accesible desde esta máquina. Verifique que la interfaz de origen seleccionada en **Advanced: Source path** esté activa; descarte cualquier **Source warning label** seleccionando una interfaz válida.
- **AetherSDR se conecta a la radio incorrecta al iniciar** — Desmarque **Connect to last radio on start up** para que la pantalla de conexión se abra en cada inicio y pueda seleccionar la radio deseada.
- **El diálogo de conexión aparece con una geometría incorrecta después de salir del modo de pantalla completa o sin bordes** — Si tenía el diálogo de conexión en modo sin bordes y estaba oculto cuando se restauró la ventana, el diálogo conserva su posición solo cuando era visible en el momento de la restauración. Esto evita que el diálogo aparezca fuera de la pantalla.
- **La lista de radios disponibles solo muestra algunas entradas y no se desplaza** — La lista tiene una altura máxima de 240 píxeles. Si se descubren más radios de las que caben, la barra de desplazamiento vertical aparece automáticamente. Use la rueda de desplazamiento o arrastre la barra de desplazamiento para ver el resto de la lista.

## Relacionado

- [Connect to a Radio overview](../../features/connection/overview.md)
- [Log in to SmartLink to see remote radios](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
