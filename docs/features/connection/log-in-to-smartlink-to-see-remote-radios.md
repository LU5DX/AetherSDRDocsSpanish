# Iniciar sesión en SmartLink para ver radios remotos

SmartLink le permite ver y conectarse a una radio Flex que se encuentra en una ubicación diferente a la de su computadora. Esta página explica cómo iniciar sesión en su cuenta de SmartLink para que los radios remotos aparezcan en la lista.

## Antes de comenzar

- Tiene una cuenta de FlexRadio SmartLink (correo electrónico y contraseña).
- La computadora que ejecuta AetherSDR tiene acceso a internet.
- AetherSDR está abierto y no hay ninguna radio conectada actualmente (el panel de conexión está visible).

## Pasos

1. Abra el panel de conexión. Si no está visible, vaya a `Settings > Connect to Radio...`.
2. Haga clic en **Remote with SmartLink**. Esto cambia el panel a la página de SmartLink.
3. En el grupo **SmartLink account**, ingrese el correo electrónico de su cuenta de FlexRadio en el campo **Email**.
4. Ingrese su contraseña en el campo **Password**. La contraseña no se guarda entre sesiones.
5. Haga clic en **Sign In**.
6. Espere a que la etiqueta de estado se actualice. Cuando la autenticación es exitosa, su nombre, indicativo o "Signed in to SmartLink" aparece sobre la lista de radios.
7. La lista **Remote radios** se llena con los radios disponibles para su cuenta.

Para finalizar la sesión, haga clic en **Sign Out**.

## Qué hace cada control

| Control | Qué hace | Configuración persistente |
|---|---|---|
| Botón de modo **Remote with SmartLink** | Cambia el panel a la página de SmartLink. | `ConnectionMode` |
| Campo **Email** | El correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| Campo **Password** | La contraseña de su cuenta de FlexRadio. No se guarda entre sesiones. | — |
| **Sign In** | Se autentica con SmartLink y solicita la lista de radios. | — |
| **Sign Out** | Cierra la sesión de SmartLink y borra la lista de radios. | — |
| Lista **Remote radios** | Muestra los radios SmartLink WAN disponibles para su cuenta después de iniciar sesión. | — |

## Consejos

- Su dirección de correo electrónico se guarda en `SmartLinkEmail` y se completa automáticamente en el siguiente inicio. Su contraseña nunca se conserva; debe ingresarla de nuevo en cada sesión.
- Si ve su nombre e indicativo en la etiqueta de estado pero la lista **Remote radios** está vacía, es posible que la radio en la estación remota esté desconectada o no esté registrada en su cuenta.

## Solución de problemas

- **Sign In no responde o la etiqueta de estado muestra un error** — Verifique que su correo electrónico y contraseña sean correctos. Compruebe que la computadora tenga acceso a internet. El servicio SmartLink requiere conectividad HTTPS saliente.
- **La lista Remote radios está vacía después de iniciar sesión** — Es posible que la radio remota esté apagada o que su conexión a internet esté interrumpida. Confirme que la radio está en línea en la ubicación remota.
- **El campo Email aparece en blanco al iniciar** — `SmartLinkEmail` no fue guardado. Ingrese la dirección e inicie sesión; quedará guardado para sesiones futuras tras una interacción exitosa con el panel.

## Relacionados

- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse a una radio local por LAN](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Activar el modo de bajo ancho de banda para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Operación remota a través de SmartLink](../../operating/remote/remote-operation-smartlink.md)
