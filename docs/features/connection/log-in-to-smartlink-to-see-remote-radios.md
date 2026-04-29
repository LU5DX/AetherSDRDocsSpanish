# Iniciar sesión en SmartLink para ver radios remotas

SmartLink permite acceder a un FLEX-8600 en una ubicación remota a través de internet. Esta página explica cómo iniciar sesión en su cuenta FlexRadio SmartLink para que AetherSDR pueda mostrar las radios disponibles.

## Antes de comenzar

- Debe tener una cuenta FlexRadio con acceso a SmartLink. Si no la tiene, créela en el sitio web de FlexRadio antes de continuar.
- La radio remota debe estar registrada en SmartLink y encendida.
- AetherSDR no debe estar conectado a ninguna radio. El panel de conexión aparece automáticamente cuando no hay ninguna radio conectada.

## Pasos

1. Abra el panel de conexión. Si AetherSDR ya muestra la interfaz principal, vaya a `Settings > Connect to Radio...`.
2. Haga clic en `Remote with SmartLink`. El panel cambia a la página de SmartLink.
3. En **SmartLink account**, introduzca el correo electrónico de su cuenta FlexRadio en el campo `SmartLink account: Email`.
4. Introduzca su contraseña en el campo `SmartLink account: Password`. La contraseña no se guarda entre sesiones.
5. Haga clic en `Sign In`. AetherSDR se autentica con SmartLink y, si tiene éxito, rellena la lista `Remote radios` con las radios disponibles para su cuenta.

## Qué hace cada control

| Control | Función | Ajuste persistente |
|---|---|---|
| Botón de modo `Remote with SmartLink` | Cambia el panel a la página de SmartLink. | `ConnectionMode` |
| `SmartLink account: Email` | Dirección de correo electrónico de su cuenta FlexRadio. | `SmartLinkEmail` |
| `SmartLink account: Password` | Su contraseña de SmartLink. No se guarda al finalizar la sesión. | — |
| `Sign In` | Se autentica con SmartLink y recupera la lista de radios remotas. | — |
| `Remote radios` | Muestra las radios WAN disponibles para su cuenta tras iniciar sesión. La lista tiene una altura de visualización fija; si tiene muchas radios remotas, desplácese dentro de la lista para verlas todas. | — |
| `Connect Remote Radio` | Inicia una conexión WAN a la radio seleccionada en la lista `Remote radios`. | — |
| `Sign Out` | Finaliza la sesión actual de SmartLink. | — |

## Consejos

- `SmartLinkEmail` es persistente, por lo que su dirección de correo electrónico aparece precargada en el próximo inicio. Su contraseña nunca se almacena.
- Después de iniciar sesión, la etiqueta de estado debajo del grupo de cuenta muestra su nombre, indicativo o una confirmación de que ha iniciado sesión, según el contenido de su perfil de cuenta.
- La lista `Remote radios` está dimensionada para mostrar una vista compacta de las radios disponibles. Desplácese dentro de la lista si la entrada que busca no es visible de inmediato.

## Solución de problemas

- **La lista `Remote radios` está vacía después de iniciar sesión** — Es posible que la radio remota esté apagada, no registrada en SmartLink o asociada a una cuenta FlexRadio diferente. Confirme que la radio está encendida y registrada en la misma cuenta con la que inició sesión.
- **`Sign In` produce un error** — Verifique que su correo electrónico y contraseña sean correctos. Un error tipográfico en el campo de correo electrónico es una causa frecuente, ya que el campo no tiene corrección automática. Compruebe sus credenciales en el sitio web de FlexRadio.
- **La página de SmartLink no es accesible** — El firewall o el software VPN de este equipo puede estar bloqueando el tráfico saliente de SmartLink. Use `Open Network Diagnostics` (disponible en la página Local) para verificar la conectividad, o consulte [Conectar por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md) si su configuración requiere una ruta IP directa.

## Relacionados

- [Conectar a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectar a una radio de red local LAN](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Activar el modo de bajo ancho de banda para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
