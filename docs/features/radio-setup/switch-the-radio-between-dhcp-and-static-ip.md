# Cambiar el radio entre DHCP e IP estática

Use esta página para configurar el modo de direccionamiento de red del radio Flex. Cambie a IP estática cuando necesite que el radio tenga una dirección fija en su LAN, o vuelva a DHCP para que el router asigne una dirección automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Network solo está disponible mientras haya conexión.
- Si va a asignar una IP estática, tenga listos la dirección IP deseada, la máscara de subred y la dirección de gateway antes de empezar.
- Cambiar la dirección IP desconectará AetherSDR del radio. Esté preparado para volver a conectarse con la nueva dirección.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el botón de alternancia **DHCP / Static**. Haga clic en él para cambiar entre modos.
   - Cuando está en DHCP, los campos de dirección estática no son necesarios.
   - Cuando está en Static, los campos **IP Address:**, **Mask:** y **Gateway:** se activan.
4. Si seleccionó Static, ingrese los valores deseados en los campos **IP Address:**, **Mask:** y **Gateway:**.
5. Haga clic en **Apply** para enviar la configuración de red al radio.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **DHCP / Static** | Botón de alternancia | Cambia el radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | La dirección IPv4 estática que se asignará al radio. Activo solo en modo Static. |
| **Mask:** | Campo de texto | La máscara de subred para la configuración estática. Activa solo en modo Static. |
| **Gateway:** | Campo de texto | El gateway predeterminado para la configuración estática. Activo solo en modo Static. |
| **Apply** | Botón | Envía la configuración de red actual al radio. |

## Consejos

- Los indicadores **IP Address / Mask / MAC Address** que aparecen sobre el botón de alternancia muestran las direcciones de red actuales del radio y son de solo lectura. Úselos para confirmar que la nueva configuración surtió efecto después de reconectarse.
- Tras hacer clic en **Apply** en modo Static, AetherSDR perderá la conexión. Vuelva a conectarse mediante `Settings > Connect to Radio...` usando la nueva dirección estática.

## Solución de problemas

- **El radio no aparece tras cambiar a IP estática** — La dirección ingresada puede entrar en conflicto con otro dispositivo o puede estar fuera de la subred de su LAN. Verifique que la dirección IP, la máscara y el gateway sean correctos para su red. Si el radio queda inaccesible, puede ser necesario un restablecimiento de hardware para restaurar DHCP; consulte la documentación de hardware del radio Flex.
- **Apply no parece surtir efecto** — Asegúrese de que sigue conectado al radio en el momento en que hace clic en **Apply**. Si la conexión se interrumpió antes de hacer clic, vuelva a abrir `Settings > Radio Setup...`, reingrese los valores estáticos y haga clic en **Apply** sin demora.

## Relacionado

- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Descripción general de Radio Setup](overview.md)
