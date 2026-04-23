# Conectar TGXL, PGXL o Antenna Genius por dirección IP

Esta página explica cómo conectar manualmente un periférico TGXL, PGXL o Antenna Genius a AetherSDR mediante una dirección IP. Realice este procedimiento cuando el dispositivo no sea detectado automáticamente en su red.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio Flex.
- Debe conocer la dirección IP del dispositivo TGXL, PGXL o Antenna Genius.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila correspondiente al dispositivo que desea conectar (TGXL, PGXL o Antenna Genius).
4. Ingrese la dirección IP del dispositivo en el campo de dirección de ese dispositivo.
5. Haga clic en **Connect** junto a ese dispositivo.
6. Verifique que el estado de la conexión cambie para indicar que el dispositivo está conectado. Para desconectarlo en cualquier momento, haga clic en **Disconnect** junto al dispositivo.

## Solución de problemas

- **Connect no hace nada o el dispositivo no muestra conexión** — Confirme que la dirección IP es correcta y que el dispositivo está encendido y es accesible desde el equipo donde se ejecuta AetherSDR. Verifique que ningún cortafuegos esté bloqueando el tráfico entre el equipo y la dirección IP del periférico.
- **El dispositivo se desconecta inmediatamente después de conectarse** — Verifique que el firmware de su radio sea la versión 4.1.5 y que el firmware del periférico sea compatible con el protocolo SmartSDR v1.4.0.0.

## Relacionados

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)
- [Conectar manualmente un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
