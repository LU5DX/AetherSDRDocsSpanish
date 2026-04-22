# Cambiar el radio entre DHCP e IP estática

Use esta página para cambiar cómo su FLEX-8600 recibe su dirección IP — ya sea automáticamente desde un servidor DHCP o desde una dirección estática fija que usted ingresa manualmente. Una IP estática es útil cuando necesita una dirección predecible para acceso remoto o integraciones de red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Network solo está disponible mientras haya conexión activa.
- Tenga a mano la dirección IP estática deseada, la máscara de subred y la dirección de puerta de enlace antes de comenzar.
- Si va a cambiar a IP estática, confirme que la dirección que planea usar no esté ya en uso en su red y que esté fuera del rango de asignación DHCP de su router.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Localice el botón de alternancia **DHCP / Static**.
4. Haga clic en **DHCP / Static** para cambiar entre modos. El botón refleja el modo activo actualmente.
5. Si cambió a Static, ingrese valores en los campos **IP Address:**, **Mask:** y **Gateway:**.
6. Haga clic en **Apply** para enviar la configuración de red al radio.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador (solo lectura) | Muestra las direcciones de red actuales del radio. Se actualizan después de que Apply surte efecto. |
| **DHCP / Static** | Botón de alternancia | Cambia el radio entre asignación DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática que se asignará al radio. Activo solo en modo Static. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo Static. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo Static. |
| **Apply** | Botón | Envía la configuración de red al radio. |
| **Enforce Private IP Connections:** | Botón de alternancia | Cuando está habilitado, rechaza conexiones provenientes de direcciones IP que no sean RFC1918 (no privadas). |
| **Network MTU:** | Spinbox | Establece el MTU de salida en bytes. |

## Consejos

- Después de hacer clic en **Apply** con una nueva IP estática, el radio dejará de ser accesible en su dirección anterior. Reconéctese usando la nueva IP mediante `Settings > Connect to Radio...`.
- Si va a volver a DHCP, no es necesario completar los campos de dirección — haga clic en **Apply** inmediatamente después de alternar a DHCP.

## Solución de problemas

- **El radio no es accesible después de aplicar una IP estática** — La dirección, la máscara o la puerta de enlace pueden ser incorrectas para su red. Conéctese al radio mediante la pantalla del panel frontal o la consola para verificar la configuración, luego corrija los valores en AetherSDR.
- **Apply no tiene efecto** — Confirme que el radio sigue conectado (la pestaña Network requiere una conexión activa). Si la conexión se interrumpió, reconéctese y vuelva a ingresar la configuración antes de hacer clic en **Apply**.

## Relacionado

- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Descripción general de Radio Setup](overview.md)
