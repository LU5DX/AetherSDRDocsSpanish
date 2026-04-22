# Cambiar el radio entre DHCP e IP estática

Use esta página para cambiar la forma en que el FLEX-8600 obtiene su dirección IP: ya sea automáticamente mediante DHCP o con una dirección estática fija que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Network** solo está disponible cuando hay una conexión activa.
- Si va a cambiar a IP estática, tenga listos la dirección IP de destino, la máscara de subred y la dirección de puerta de enlace antes de comenzar.
- Tenga en cuenta que cambiar la configuración IP hará que el radio use una nueva dirección. Es posible que deba reconectar AetherSDR después de aplicar los cambios.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Tome nota de la **IP Address**, la **Mask** y la **MAC Address** actuales, que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo.
   - En modo DHCP, el radio solicita una dirección al servidor DHCP de la red.
   - En modo Static, los campos de texto **IP Address:**, **Mask:** y **Gateway:** quedan habilitados para edición.
5. Si seleccionó el modo estático, ingrese los valores en los campos **IP Address:**, **Mask:** y **Gateway:**.
6. Haga clic en **Apply** para enviar la configuración de red al radio.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestran las direcciones de red actuales del radio. |
| **DHCP / Static** | Botón de alternancia | Cambia el radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática que se asignará al radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activa solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activa solo en modo estático. |
| **Apply** | Botón de acción | Envía la configuración de red actual al radio. |

## Sugerencias

- El indicador de solo lectura **IP Address** refleja la dirección actual del radio antes de que se aplique cualquier cambio. Úselo para confirmar a qué dirección deberá reconectarse AetherSDR después del cambio.
- Si cambia a DHCP y su red no tiene un servidor DHCP, el radio puede quedar inaccesible. Asegúrese de que haya un servidor DHCP disponible antes de cambiar.

## Solución de problemas

- **El radio queda inaccesible después de hacer clic en Apply** — El radio ahora tiene una nueva dirección IP. Use `Settings > Connect to Radio...` para redescubrirlo en la red. Si asignó una IP estática fuera de su subred, es posible que deba conectar una pantalla directamente al radio para corregir la dirección.
- **Los campos IP Address:, Mask: y Gateway: aparecen en gris** — El botón de alternancia está en modo DHCP. Haga clic en **DHCP / Static** para cambiar a modo estático antes de editar los campos.

## Relacionados

- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Descripción general de Radio Setup](overview.md)
