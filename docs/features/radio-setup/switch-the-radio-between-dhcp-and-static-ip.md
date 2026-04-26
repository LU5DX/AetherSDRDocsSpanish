# Cambiar la Radio entre DHCP e IP Estática

Use esta página para cambiar la forma en que su FLEX-8600 recibe su dirección de red: ya sea automáticamente mediante DHCP o con una IP estática fija que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión de radio activa.
- Si va a cambiar a IP estática, tenga listos la dirección IP, la máscara de subred y la dirección de gateway antes de comenzar.
- Cambiar la dirección IP de la radio interrumpirá la conexión actual. Deberá reconectarse usando la nueva dirección.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Anote la **IP Address**, la **Mask** y la **MAC Address** actuales que se muestran como indicadores de solo lectura. Estos reflejan lo que la radio está usando en ese momento.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. La etiqueta del botón refleja el modo activo en ese momento.
5. Si cambió a **Static**, complete los campos **IP Address:**, **Mask:** y **Gateway:** con los valores que desea asignar.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio usando la nueva dirección IP si la conexión se interrumpe.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador (solo lectura) | Muestra las direcciones de red actuales de la radio. Se actualiza después de establecer una conexión. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre el modo DHCP (dirección asignada por su router) y el modo estático (dirección que usted especifica manualmente). |
| **IP Address:** | Campo de texto | La dirección IPv4 estática que se asignará a la radio. Solo está activo en modo estático. |
| **Mask:** | Campo de texto | La máscara de subred para la configuración estática. Solo está activo en modo estático. |
| **Gateway:** | Campo de texto | El gateway predeterminado para la configuración estática. Solo está activo en modo estático. |
| **Enforce Private IP Connections:** | Botón de alternancia | Cuando está habilitado, la radio rechaza conexiones provenientes de direcciones IP que no sean RFC1918 (no privadas). |
| **Network MTU:** | Cuadro numérico | Establece el MTU de salida en bytes. |
| **Apply** | Botón | Envía la configuración de red actual a la radio. |

## Consejos

- Después de hacer clic en **Apply** con una nueva IP estática, AetherSDR perderá contacto con la radio. Use `Settings > Connect to Radio...` para redescubrirla o ingrese manualmente la nueva dirección.
- Si no está seguro de qué dirección estática usar, consulte la tabla de concesiones DHCP de su router para ver la dirección asignada actualmente a la MAC Address de la radio; luego reserve o asigne esa dirección como entrada estática.

## Solución de problemas

- **Los campos IP Address:, Mask: y Gateway: no son editables** — El botón de alternancia **DHCP / Static** está configurado en DHCP. Cámbielo primero a Static.
- **La radio no aparece después de cambiar a IP estática** — La dirección, la máscara o el gateway ingresados pueden ser incorrectos para su red. Conecte la radio a una pantalla o use los controles del panel frontal para verificar o restablecer la configuración de red, luego vuelva a intentarlo.
- **Apply no tiene ningún efecto visible** — Confirme que AetherSDR sigue conectado a la radio antes de hacer clic en **Apply**. Si la conexión ya se había perdido, reconéctese primero y luego vuelva a aplicar la configuración.

## Relacionados

- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Descripción general de Radio Setup](overview.md)
