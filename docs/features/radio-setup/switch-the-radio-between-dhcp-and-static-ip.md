# Cambiar el radio entre DHCP e IP estática

Use esta página para cambiar la forma en que su FLEX-8600 obtiene su dirección IP: ya sea automáticamente mediante DHCP o con una dirección estática fija que usted especifique. Utilice una IP estática para garantizar que el radio siempre sea accesible en una dirección conocida, por ejemplo en una configuración remota o con VPN.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Network solo está disponible mientras haya conexión.
- Si va a cambiar a IP estática, tenga lista su dirección IP, máscara de subred y dirección de puerta de enlace antes de comenzar.
- Cambiar la dirección IP del radio interrumpirá la conexión actual. Vuelva a conectarse usando la nueva dirección después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Localice el botón de alternancia **DHCP / Static**. Haga clic en él para cambiar entre los modos DHCP e IP estática.
4. Si seleccionó Static: escriba los valores deseados en los campos **IP Address:**, **Mask:** y **Gateway:**.
5. Haga clic en **Apply** para enviar la configuración de red al radio.
6. Vuelva a conectarse al radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **DHCP / Static** | Botón de alternancia | Cambia el radio entre el modo DHCP (dirección asignada por su enrutador) y el modo IP estática (dirección que usted ingresa manualmente). |
| **IP Address:** | Campo de texto | La dirección IPv4 estática que se asignará al radio. Activo solo en modo Static. |
| **Mask:** | Campo de texto | La máscara de subred para la dirección estática. Activo solo en modo Static. |
| **Gateway:** | Campo de texto | La puerta de enlace predeterminada para la dirección estática. Activo solo en modo Static. |
| **Apply** | Botón | Envía la configuración de red actual al radio. |
| **IP Address / Mask / MAC Address** (solo lectura) | Indicador | Muestra las direcciones de red actuales del radio. Son de solo lectura. |

## Consejos

- Los indicadores de solo lectura **IP Address / Mask / MAC Address** en la parte superior de la pestaña Network muestran las direcciones activas actuales del radio. Anótelas antes de realizar cambios para poder recuperarse si es necesario.
- Si se conecta a través de una VPN o enlace remoto, revise también la configuración **Network MTU:** en la misma pestaña. Consulte [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md).

## Solución de problemas

- **No se puede ver la pestaña Network** — La pestaña solo está disponible cuando AetherSDR está conectado al radio. Conéctese primero mediante `Settings > Connect to Radio...` y luego vuelva a abrir Radio Setup.
- **El radio no es accesible después de hacer clic en Apply** — El radio ha adoptado su nueva dirección. Si cambió a IP estática, vuelva a conectarse usando la dirección que ingresó. Si cambió a DHCP, consulte la tabla de concesiones DHCP de su enrutador para encontrar la dirección asignada al radio.
- **Apply no tiene efecto** — Verifique que los campos IP Address:, Mask: y Gateway: contengan valores válidos antes de hacer clic en Apply. Una configuración estática incompleta puede ser rechazada sin notificación.

## Relacionados

- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Verificar número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
