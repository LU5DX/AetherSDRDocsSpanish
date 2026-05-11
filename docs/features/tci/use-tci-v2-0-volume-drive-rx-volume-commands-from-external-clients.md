# Uso de comandos volume/drive/rx_volume de TCI v2.0 desde clientes externos

Los clientes externos (software de registro, software de modos digitales, programas SDR) pueden controlar AetherSDR mediante los comandos `volume`, `drive` y `rx_volume` de TCI v2.0 cuando el servidor TCI está habilitado y la radio está conectada.

## Antes de comenzar

- Habilite el servidor TCI (haga clic en el botón TCI de la bandeja en la barra lateral derecha, luego haga clic en Enable).
- Conéctese a una radio.
- Configure su cliente externo para conectarse al servidor TCI de AetherSDR en el puerto que se muestra en el applet TCI (predeterminado: 50001).

## Pasos

1. En el applet TCI, anote el número de puerto o cámbielo editando el campo de texto y presionando Enter. Rango válido: 1024–65535.
2. Configure su cliente externo para conectarse a la dirección IP de AetherSDR y a ese puerto.
3. Envíe los comandos TCI v2.0 desde su cliente:

   - **`volume`** — Establece el volumen RX maestro. AetherSDR asigna esto a la ganancia RX del slice activo actualmente.
   - **`drive`** — Establece el nivel de excitación TX. AetherSDR asigna esto a `TciTxGain`.
   - **`rx_volume <channel>`** — Establece la ganancia RX para un canal DAX específico (1–4). AetherSDR asigna esto a `TciRxGain1` a `TciRxGain4`.

4. El servidor TCI recibe estos comandos y actualiza las configuraciones de ganancia correspondientes. Los cambios se reflejan en los controles de medidor/deslizador del applet TCI y se guardan en la configuración.

## Qué hace cada control

| Comando | Configuración asignada | Predeterminado | Rango válido |
|---------|------------------------|----------------|--------------|
| `volume` | Ganancia RX del slice activo | 0.5 | 0.0–1.0 |
| `drive` | `TciTxGain` | 0.5 | 0.0–1.0 |
| `rx_volume <channel>` | `TciRxGain1`–`TciRxGain4` | 0.5 | 0.0–1.0 |

## Consejos

- El servidor TCI admite sincronización de estado bidireccional: los cambios realizados localmente mediante los deslizadores del applet TCI también se envían de vuelta a los clientes externos que se suscriben a las actualizaciones de ganancia.
- El comando `rx_volume` acepta un número de canal (1–4). Los números de canal corresponden a los canales DAX mostrados en las filas RX1–RX4 del applet TCI.

## Relacionados

- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
