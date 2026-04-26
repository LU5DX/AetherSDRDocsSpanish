# Conectar TGXL, PGXL o Antenna Genius por dirección IP

Esta página explica cómo conectar manualmente un periférico TGXL, PGXL o Antenna Genius a AetherSDR usando su dirección IP. Use este método cuando el dispositivo no se detecte automáticamente en su red.

## Antes de comenzar

- AetherSDR debe estar ya conectado a una radio FLEX-8600. La pestaña **Peripherals** solo está disponible cuando hay una conexión de radio activa.
- Debe conocer la dirección IP del dispositivo TGXL, PGXL o Antenna Genius.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila correspondiente al dispositivo que desea conectar (TGXL, PGXL o Antenna Genius).
4. Ingrese la dirección IP del dispositivo en el campo de dirección correspondiente.
5. Haga clic en **Connect** junto a ese dispositivo.

Para desconectar un dispositivo, haga clic en **Disconnect** junto a él.

## Consejos

- Si su periférico se encuentra en una subred diferente o solo es accesible a través de una VPN, ingrese su dirección IP enrutable directamente en el campo de dirección antes de hacer clic en **Connect**.
- Cada dispositivo (TGXL, PGXL, Antenna Genius) tiene su propio control independiente **Connect** / **Disconnect**. Puede conectarlos de forma individual.

## Solución de problemas

- **El botón Connect no responde o el dispositivo no muestra conexión** — Verifique que la dirección IP sea correcta y que el dispositivo esté encendido y sea accesible desde su equipo. Intente hacer ping a la dirección IP del dispositivo desde una terminal antes de volver a intentarlo.
- **La pestaña Peripherals no aparece o está desactivada** — La pestaña requiere una conexión de radio activa. Conéctese al FLEX-8600 primero y luego vuelva a abrir `Settings > Radio Setup...`.

## Relacionado

- [Descripción general de Radio Setup](../../features/radio-setup/overview.md)
- [Conectar manualmente un AG a través de una red remota](manually-connect-to-an-ag-over-a-remote-network.md)
- [Cambiar el MTU de red para configuraciones VPN o remotas](../../features/radio-setup/change-network-mtu-for-vpn-remote-setups.md)
- [Conectar por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
