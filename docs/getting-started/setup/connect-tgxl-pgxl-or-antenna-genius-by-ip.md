# Conectar TGXL, PGXL o Antenna Genius por dirección IP

Esta página explica cómo conectar manualmente un periférico TGXL, PGXL o Antenna Genius a AetherSDR mediante una dirección IP. Use este método cuando el dispositivo no sea descubierto automáticamente en su red.

## Antes de comenzar

- AetherSDR debe estar ya conectado a su radio FLEX-8600.
- Debe conocer la dirección IP del dispositivo TGXL, PGXL o Antenna Genius.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila correspondiente al dispositivo que desea conectar (TGXL, PGXL o Antenna Genius).
4. Ingrese la dirección IP del dispositivo en el campo de dirección para ese dispositivo.
5. Haga clic en **Connect** junto a ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** junto a él.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Connect** (por dispositivo) | Abre una conexión con el dispositivo en la dirección IP ingresada. |
| **Disconnect** (por dispositivo) | Cierra la conexión actual con ese dispositivo. |

## Solución de problemas

- **Connect no hace nada o el dispositivo aparece como no disponible** — Confirme que la dirección IP es correcta y que el dispositivo está encendido y accesible desde su equipo host. Si la radio y el dispositivo se encuentran en subredes diferentes, asegúrese de que el enrutamiento entre ellas esté configurado. Consulte [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md).
- **Antenna Genius no aparece en la pestaña Peripherals** — La pestaña Peripherals solo se construye la primera vez que se selecciona. Haga clic en la pestaña una vez para activar la construcción de la interfaz y vuelva a intentarlo.

## Relacionados

- [Cambiar el MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectar manualmente un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
