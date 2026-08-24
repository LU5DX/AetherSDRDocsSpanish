# Operación remota a través de SmartLink

SmartLink le permite conectarse a un FLEX-8600 que se encuentra en una ubicación distinta a la de su computadora. Esta página cubre cómo iniciar sesión en su cuenta de SmartLink y conectarse a una radio remota desde la pantalla de conexión de AetherSDR.

## Antes de comenzar

- Su FLEX-8600 debe estar encendido y conectado a internet en la ubicación remota, con SmartLink habilitado en su firmware.
- Debe tener una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- AetherSDR no debe estar ya conectado a una radio. Si lo está, desconéctelo primero.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente cuando no hay ninguna radio conectada. También puede acceder a ella mediante `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto selecciona el modo SmartLink y muestra los controles de cuenta de SmartLink y de radio remota.
3. En el campo **SmartLink account: Email**, ingrese la dirección de correo electrónico de su cuenta FlexRadio.
4. En el campo **SmartLink account: Password**, ingrese su contraseña. La contraseña no se guarda entre sesiones. El campo está etiquetado con nombres de accesibilidad para administradores de contraseñas (macOS Passwords, Windows Authenticator, KDE Wallet).
5. Haga clic en **Sign In**. La etiqueta de estado se actualiza para mostrar el progreso de la autenticación.
6. Una vez que haya iniciado sesión, la lista **Remote radios** se completará con las radios disponibles para su cuenta. Seleccione la radio que desea usar.
7. Si su enlace al sitio remoto es lento (satelital, celular o banda ancha congestionada), marque **Use low bandwidth mode** antes de conectarse.
8. Haga clic en **Connect Remote Radio**. La etiqueta de estado sigue el progreso de la conexión. Cuando la conexión se establece correctamente, se abre la interfaz principal de AetherSDR.

## Qué hace cada control

| Control | Qué hace | Configuración persistida |
|---|---|---|
| **Local / SmartLink / Manual** (botones de modo) | Cambia la pantalla de conexión entre los tres modos de conexión. Cada botón está identificado en el árbol de accesibilidad para admitir pruebas automatizadas. | `ConnectionMode` |
| **Remote with SmartLink** (botón de modo) | Cambia la pantalla de conexión al modo SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | El correo electrónico de su cuenta FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | Su contraseña de SmartLink. No se guarda después de que finaliza la sesión. | — |
| **Sign In** | Autentica con SmartLink y completa la lista **Remote radios**. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios remotas. | — |
| **Remote radios** | Enumera las radios WAN de SmartLink disponibles para la cuenta con sesión iniciada. La lista tiene una altura de visualización fija; si tiene muchas radios remotas, desplácese dentro de la lista para verlas todas. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos de transmisión para enlaces lentos o medidos. | `LowBandwidthMode` |
| **Enable adaptive frame-rate throttle** | Reduce automáticamente la tasa de fotogramas de FFT/waterfall cuando la calidad de la red se degrada. | `AdaptiveThrottleEnabled` |
| **Connect Remote Radio** | Inicia una conexión WAN a la radio seleccionada en **Remote radios**. | — |
| **Connect to last radio on start up** | Cuando está marcado, AetherSDR se conecta automáticamente a la última radio usada al iniciar y en la detección por difusión / prueba de radio enrutada. Cuando no está marcado, se abre el diálogo de conexión y el usuario debe elegir una radio manualmente en cada sesión. Está marcado por defecto. | `AutoConnectToLastRadio` |
| **Disconnect** | Desconecta de la radio actual y regresa a la pantalla de conexión. | — |

## Conexión por IP (modo Manual)

Si su radio está en una VPN o en una red enrutada que no es visible mediante la detección LAN, use el modo Manual en lugar de SmartLink.

1. Haga clic en **Connect by IP** en la página Local, o haga clic en el botón de modo **Manual** en la parte superior de la pantalla de conexión.
2. En el campo **Radio IP address**, escriba la dirección IP de la radio. El campo acepta direcciones IPv4 e IPv6, así como nombres de host. AetherSDR normaliza la dirección cuando se conecta.
3. El control **Radio IP address** es tanto un menú desplegable como un campo de texto. Almacena hasta tres direcciones usadas recientemente (guardadas como `RecentConnectByIpAddresses`). Para reutilizar una dirección anterior, haga clic en la flecha del menú desplegable y selecciónela de la lista.
4. Si es necesario, seleccione la interfaz de red local que desea usar en **Advanced: Source path**. Aparece una **Source warning label** debajo del selector si la interfaz elegida está obsoleta o es inalcanzable.
5. Haga clic en **Connect by IP (manual)**. La **Manual result label** muestra si la prueba tuvo éxito o falló.

### Nombres de host en el campo de IP Manual

El campo **Radio IP address** acepta nombres de host además de direcciones IP numéricas. Esto es especialmente útil para radios Icom cuya dirección predeterminada documentada es un nombre de host (por ejemplo, `ic-705.local`). El menú desplegable de direcciones recientes recuerda los nombres de host que ingresa entre sesiones, igual que con las direcciones numéricas. Los nombres de host se validan con un conjunto de caracteres conservador (letras, dígitos, punto, guion, guion bajo, con extremos alfanuméricos) antes de guardarse y se limitan a 253 caracteres.

## Gestión de apodos de radios

Haga clic derecho en cualquier radio de la lista **Available radios** en la página Local para establecer un apodo personalizado. Esto es útil para distinguir entre varias radios que informan nombres de detección similares. El apodo se guarda con la clave del número de serie y aparece en futuros barridos de detección. Esta función está disponible solo para radios que no tienen un almacén de nombres en la propia radio (como HL2 o radios simuladoras); las radios FlexRadio establecen su nombre desde Radio Setup mientras están conectadas y no se ven afectadas por apodos del lado del cliente.

## Consejos

- `SmartLinkEmail` se persiste, por lo que su dirección de correo electrónico se rellena previamente la próxima vez que abra la pantalla de conexión. Su contraseña no se persiste y debe ingresarse en cada sesión.
- Si la lista **Remote radios** está vacía después de iniciar sesión, la radio remota puede no tener SmartLink habilitado o puede estar fuera de línea.
- El menú desplegable **Radio IP address** recuerda hasta tres direcciones recientes entre sesiones. Si anteriormente usó la configuración `LastRoutedRadioIp` (de una versión anterior a v0.9.7), AetherSDR la importa automáticamente a la lista de direcciones recientes en el primer inicio.
- **Connect to last radio on start up** está marcado por defecto. Si trabaja con varias radios y desea elegir explícitamente en cada sesión, desmárquelo.
- El formulario de inicio de sesión de SmartLink está identificado en el árbol de accesibilidad como "SmartLink account login", lo que facilita que los administradores de contraseñas asocien los campos de credenciales con este formulario de inicio de sesión específico.
- La casilla **Enable adaptive frame-rate throttle** no está marcada por defecto. Cuando está habilitada, AetherSDR reduce automáticamente la tasa de fotogramas de FFT y waterfall cuando la calidad de la red se degrada, lo que ayuda a mantener una conexión estable en enlaces de calidad variable.
- La lista **Available radios** en la página Local tiene una altura máxima fija para que la lista se desplace internamente cuando se detectan muchas radios. En pantallas pequeñas (por ejemplo, un panel de 1024×600), esto evita que el botón Connect y las radios inferiores queden inaccesibles. La lista muestra una barra de desplazamiento vertical según sea necesario.
- Los menús contextuales de clic derecho en la lista **Available radios** son leídos por los lectores de pantalla y se informan como "available local radios" con una descripción accesible de "Discovered FlexRadio radios on the local network".
- Los nombres de host en el campo **Radio IP address** usan un conjunto de caracteres conservador (letras, dígitos, punto, guion, guion bajo, con extremos alfanuméricos) y se limitan a 253 caracteres. Las direcciones que no coinciden con este patrón no se recuerdan en la lista reciente.
- El botón **Network Diagnostics** aparece tanto en la página Local como en la página Manual. Úselo para verificar la accesibilidad de la red antes de intentar una conexión.

## Solución de problemas

- **La lista de radios remotas está vacía después de Sign In** — La radio en la ubicación remota puede estar fuera de línea o SmartLink puede no estar habilitado en ella. Confirme que la radio esté encendida y registrada con la misma cuenta de FlexRadio.
- **Sign In falla o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Confirme que AetherSDR tenga acceso a internet saliente y que ningún firewall o proxy esté bloqueando la conexión SmartLink.
- **El audio es entrecortado o se corta con frecuencia** — Habilite **Use low bandwidth mode** antes de conectarse para reducir las tasas de transmisión del enlace. Para conexiones de calidad variable, también habilite **Enable adaptive frame-rate throttle** para ajustar automáticamente las tasas de actualización de visualización.
- **La conexión Manual falla o la Manual result label muestra un error** — Confirme que la dirección IP o el nombre de host sean correctos y accesibles desde esta máquina. Verifique que la interfaz de origen seleccionada en **Advanced: Source path** esté activa; descarte cualquier **Source warning label** seleccionando una interfaz válida.
- **Un nombre de host ingresado en el campo de IP Manual no se recuerda** — El nombre de host puede contener caracteres fuera del conjunto aceptado (letras, dígitos, punto, guion, guion bajo, con extremos alfanuméricos) o superar los 253 caracteres. Las direcciones IP numéricas se canonizan y siempre se aceptan.
- **AetherSDR se conecta a la radio equivocada al iniciar** — Desmarque **Connect to last radio on start up** para que la pantalla de conexión se abra en cada inicio y pueda seleccionar la radio deseada.
- **El diálogo de conexión aparece con geometría incorrecta después de salir del modo de pantalla completa o sin bordes** — Si tenía el diálogo de conexión en modo sin bordes y estaba oculto cuando se restauró la ventana, el diálogo conserva su posición solo si estaba visible en el momento de la restauración. Esto evita que el diálogo aparezca fuera de la pantalla.
- **La lista de radios disponibles solo muestra unas pocas entradas y no se desplaza** — La lista tiene una altura máxima de 240 píxeles. Si se detectan más radios de las que caben, la barra de desplazamiento vertical aparece automáticamente. Use la rueda del ratón o arrastre la barra de desplazamiento para ver el resto de la lista.

## Relacionado

- [Connect to a Radio overview](../../features/connection/overview.md)
- [Log in to SmartLink to see remote radios](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Connect to a remote radio through SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Enable low-bandwidth mode for slow links](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Disconnect from the current radio](../../getting-started/setup/disconnect-from-the-current-radio.md)
- [Connect by IP across a VPN or routed network](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
