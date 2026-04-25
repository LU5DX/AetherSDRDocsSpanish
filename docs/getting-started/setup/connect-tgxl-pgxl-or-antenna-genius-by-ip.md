# Conectar TGXL, PGXL o Antenna Genius por IP

Esta página explica cómo conectar manualmente un dispositivo TGXL, PGXL o Antenna Genius a AetherSDR ingresando su dirección IP. Use este método cuando el dispositivo no se detecte automáticamente en su red.

## Antes de comenzar

- AetherSDR debe estar ya conectado a una radio FLEX-8600. La pestaña Peripherals no está disponible sin una conexión de radio activa.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL o Antenna Genius.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila correspondiente al dispositivo que desea conectar (TGXL, PGXL o Antenna Genius).
4. Ingrese la dirección IP del dispositivo en el campo de dirección de ese dispositivo.
5. Haga clic en **Connect** para ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** en su fila.

## Solución de problemas

- **Connect no tiene efecto o el dispositivo aparece como inalcanzable** — Confirme que la dirección IP es correcta y que el dispositivo está encendido y accesible desde la misma red que la radio. Si la radio y el dispositivo se encuentran en subredes separadas, asegúrese de que el enrutamiento esté configurado.
- **La pestaña Peripherals no aparece o está desactivada** — AetherSDR requiere una conexión de radio activa para mostrar esta pestaña. Conéctese a la radio antes de abrir Radio Setup.

## Relacionado

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
