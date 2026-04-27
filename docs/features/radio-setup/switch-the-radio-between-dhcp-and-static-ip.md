# Cambiar la radio entre DHCP e IP estática

Use esta página para cambiar la forma en que el FLEX-8600 obtiene su dirección de red: de manera automática mediante DHCP o con una IP estática fija, máscara de subred y puerta de enlace que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión de radio activa.
- Si va a cambiar a IP estática, tenga listos los valores de dirección IP, máscara de subred y puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá reconectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Anote la **IP Address**, la **Mask** y la **MAC Address** actuales que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic se cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores correspondientes a su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio en su nueva dirección mediante `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática que se asignará a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón de acción | Envía la configuración de red a la radio. |

## Consejos

- Los indicadores **IP Address / Mask / MAC Address** muestran lo que la radio está usando actualmente. Registre estos valores antes de realizar cambios para poder revertirlos si es necesario.
- El botón de alternancia **Enforce Private IP Connections:** en la misma pestaña rechaza conexiones provenientes de direcciones que no sean RFC1918. Si asigna una IP estática, confirme que se encuentre dentro de un rango privado (p. ej., 192.168.x.x, 10.x.x.x) si dicho botón está habilitado.

## Solución de problemas

- **No se encuentra la radio después de hacer clic en Apply** — La radio se ha movido a su nueva dirección. Use `Settings > Connect to Radio...` para detectarla y reconectarse a ella en la dirección actualizada.
- **Los campos IP Address:, Mask: y Gateway: no son editables** — El botón de alternancia está configurado en DHCP. Haga clic en **DHCP / Static** para cambiar primero al modo estático.

## Relacionados

- [Cambiar la MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Consultar el número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
