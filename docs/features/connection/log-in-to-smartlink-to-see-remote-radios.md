# Iniciar sesión en SmartLink para ver radios remotos

SmartLink le permite acceder a un FLEX-8600 en una ubicación remota a través de internet. Esta página explica cómo iniciar sesión en su cuenta de FlexRadio SmartLink para que AetherSDR pueda mostrar los radios disponibles.

## Antes de comenzar

- Debe tener una cuenta de FlexRadio con acceso a SmartLink. Si no la tiene, créela en el sitio web de FlexRadio antes de continuar.
- El radio remoto debe estar registrado en SmartLink y encendido.
- AetherSDR no debe estar conectado a ningún radio. El panel de conexión aparece automáticamente cuando no hay ningún radio conectado.

## Pasos

1. Abra el panel de conexión. Si AetherSDR ya muestra la interfaz principal, vaya a `Settings > Connect to Radio...`.
2. Haga clic en `Remote with SmartLink`. El panel cambia a la página de SmartLink.
3. En **SmartLink account**, ingrese el correo electrónico de su cuenta de FlexRadio en el campo `SmartLink account: Email`.
4. Ingrese su contraseña en el campo `SmartLink account: Password`. La contraseña no se guarda entre sesiones.
5. Haga clic en `Sign In`. AetherSDR se autentica con SmartLink y, si tiene éxito, llena la lista `Remote radios` con los radios disponibles para su cuenta.

## Qué hace cada control

| Control | Función | Configuración persistente |
|---|---|---|
| Botón de modo `Remote with SmartLink` | Cambia el panel a la página de SmartLink. | `ConnectionMode` |
| `SmartLink account: Email` | El correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| `SmartLink account: Password` | Su contraseña de SmartLink. No se guarda al finalizar la sesión. | — |
| `Sign In` | Se autentica con SmartLink y recupera la lista de radios remotos. | — |
| `Remote radios` | Muestra los radios WAN disponibles para su cuenta después de iniciar sesión. | — |
| `Sign Out` | Finaliza la sesión actual de SmartLink. | — |

## Consejos

- `SmartLinkEmail` es persistente, por lo que su dirección de correo electrónico aparece completada automáticamente en el próximo inicio. La contraseña nunca se almacena.
- Después de iniciar sesión, la etiqueta de estado debajo del grupo de cuenta muestra su nombre, indicativo de llamada o una confirmación de que ha iniciado sesión, según el contenido de su perfil de cuenta.

## Solución de problemas

- **La lista `Remote radios` está vacía después de iniciar sesión** — Es posible que el radio remoto esté apagado, no registrado en SmartLink o asociado a una cuenta de FlexRadio diferente. Confirme que el radio esté encendido y registrado bajo la misma cuenta que utilizó para iniciar sesión.
- **`Sign In` produce un error** — Verifique que su correo electrónico y contraseña sean correctos. Un error tipográfico en el campo de correo electrónico es una causa frecuente, ya que el campo no tiene corrección automática. Compruebe sus credenciales en el sitio web de FlexRadio.
- **La página de SmartLink no es accesible** — El software de cortafuegos o VPN en este equipo puede estar bloqueando el tráfico saliente de SmartLink. Use `Open Network Diagnostics` (disponible en la página Local) para verificar la conectividad, o consulte [Conectar por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md) si su configuración requiere una ruta IP directa.

## Relacionado

- [Conectarse a un radio remoto a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse a un radio local en LAN](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Activar el modo de bajo ancho de banda para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Operar en remoto a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
