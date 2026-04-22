# Operación remota mediante SmartLink

SmartLink es el servicio de retransmisión en la nube de FlexRadio que permite conectarse a un FLEX-8600 en una ubicación remota a través de internet. Utilice esta página cuando su radio y su computadora se encuentren en redes distintas y disponga de una cuenta de FlexRadio.

## Antes de comenzar

- El FLEX-8600 debe estar encendido y conectado a internet en el sitio remoto.
- Debe tener una cuenta de FlexRadio (correo electrónico y contraseña) con acceso a SmartLink habilitado en esa cuenta.
- AetherSDR debe estar instalado y en ejecución en su equipo local.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente antes de conectar cualquier radio. Si ya está conectado, vaya a `Settings > Connect to Radio...` para volver a abrirla.
2. Haga clic en **Remote with SmartLink** en la fila de botones de modo en la parte superior del panel. El panel cambia a la página de SmartLink.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta de FlexRadio en el campo **SmartLink account: Email** y su contraseña en el campo **SmartLink account: Password**.
4. Haga clic en **Sign In**. AetherSDR se autentica con SmartLink. La etiqueta de estado se actualiza para reflejar el resultado del inicio de sesión.
5. Tras un inicio de sesión exitoso, la lista **Remote radios** se llena con los radios disponibles para su cuenta.
6. Seleccione el radio que desea usar en la lista **Remote radios**.
7. Haga clic en **Connect Remote Radio**. AetherSDR abre una conexión WAN al radio seleccionado.

## Función de cada control

| Control | Descripción | Clave de configuración persistente |
|---|---|---|
| **Remote with SmartLink** (botón de modo) | Cambia el panel de conexión a la página de SmartLink. | `ConnectionMode` |
| **SmartLink account: Email** | El correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| **SmartLink account: Password** | La contraseña de su cuenta de FlexRadio. No se guarda entre sesiones. | — |
| **Sign In** | Se autentica con SmartLink y obtiene la lista de radios remotos. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios remotos. | — |
| **Remote radios** | Lista los radios WAN disponibles para la cuenta con sesión iniciada. | — |
| **Connect Remote Radio** | Inicia una conexión WAN al radio seleccionado. | — |
| **Use low bandwidth mode** | Reduce las tasas de datos de transmisión para enlaces de internet lentos o congestionados. | `LowBandwidthMode` |

## Consejos

- El campo **SmartLink account: Password** no se guarda. Deberá ingresarlo cada vez que inicie sesión.
- Si la lista **Remote radios** aparece vacía después de iniciar sesión, confirme que el radio en el sitio remoto esté encendido, conectado a internet y que SmartLink esté habilitado en su configuración de SmartSDR.
- En una conexión a internet lenta, active **Use low bandwidth mode** antes de hacer clic en **Connect Remote Radio** para reducir el ancho de banda de los flujos de audio y espectro.

## Solución de problemas

- **Sign In falla o devuelve un error** — Verifique el correo electrónico y la contraseña de su cuenta de FlexRadio. Confirme que su equipo tiene una conexión a internet funcional. Revise la etiqueta de estado debajo del formulario de inicio de sesión para obtener un mensaje de error específico.
- **La lista Remote radios aparece vacía después de iniciar sesión** — Es posible que el radio en el sitio remoto esté fuera de línea, que SmartLink no esté habilitado en él, o que no esté asociado a su cuenta de FlexRadio. Confirme que la estación remota está encendida y accesible; luego haga clic en **Sign Out** e inicie sesión nuevamente para actualizar la lista.
- **La conexión se interrumpe o es lenta** — Active **Use low bandwidth mode** y vuelva a conectarse. Compruebe también que ninguno de los dos sitios tenga un cortafuegos que bloquee los puertos de retransmisión de SmartLink.

## Relacionado

- [Iniciar sesión en SmartLink para ver los radios remotos](../../features/connection/log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a un radio remoto mediante SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Conectarse a un radio en la red LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
