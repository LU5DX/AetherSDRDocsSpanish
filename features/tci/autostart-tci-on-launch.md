# Inicio automático de TCI al lanzar la aplicación

Active la opción de inicio automático para que AetherSDR inicie el servidor WebSocket de TCI automáticamente cada vez que se lance la aplicación, sin necesidad de abrir el applet de TCI y hacer clic en Enable manualmente.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el elemento de menú `Settings > Autostart TCI with AetherSDR` no aparece, su compilación no incluye TCI.
- Confirme que el servidor TCI funciona manualmente al menos una vez antes de activar el inicio automático. Consulte [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- Decida qué puerto desea que utilice el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).

## Pasos

1. Abra `Settings > Autostart TCI with AetherSDR`.
2. Haga clic en el elemento de menú para colocar una marca de verificación junto a él. El ajuste se guarda inmediatamente.
3. Reinicie AetherSDR. El servidor TCI se inicia automáticamente al lanzar la aplicación y el indicador de estado del servidor en el applet de TCI cambia de `(stopped)` a `:<port> (N clients)`.

Para desactivar el inicio automático, repita el paso 1 para quitar la marca de verificación.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|
| `Settings > Autostart TCI with AetherSDR` | Elemento de menú con marca de verificación. Cuando está marcado, el servidor TCI se inicia en cada lanzamiento sin intervención manual. | Desactivado (sin marcar) | Marcado / sin marcar | `AutoStartTCI` |
| Puerto | El puerto al que se enlaza el servidor TCI en el inicio automático. Configúrelo en el applet de TCI antes de depender del inicio automático. | `50001` | 1024–65535 | `TciPort` |
| Ganancia RX1–RX4 | Ganancia de recepción TCI para cada canal, aplicada cuando se inicia el servidor. | `0.5` | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| Ganancia TX | Ganancia de transmisión TCI, aplicada cuando se inicia el servidor. | `0.5` | 0.0–1.0 | `TciTxGain` |

## Consejos

- El applet de TCI está oculto de forma predeterminada. Ábralo con el botón `TCI` de la bandeja en la barra lateral derecha para verificar el estado del servidor después de que AetherSDR se lance.
- Los valores de ganancia (`TciRxGain1`–`TciRxGain4`, `TciTxGain`) y el puerto (`TciPort`) se guardan de forma independiente. Configúrelos antes de activar el inicio automático para que sean correctos desde el primer inicio automático.

## Solución de problemas

- **El elemento de menú `Autostart TCI with AetherSDR` no aparece** — Esta compilación de AetherSDR fue compilada sin soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(port in use)` después del inicio automático** — Otra aplicación ocupó el puerto `TciPort` antes de que AetherSDR terminara de iniciarse. Cambie el puerto en el applet de TCI a un puerto libre en el rango 1024–65535 y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El botón Enable del applet de TCI aparece desactivado después del inicio automático** — Un fallo de enlace provocó que el interruptor volviera a la posición desactivada. Compruebe el indicador de estado del servidor para ver si muestra `(port in use)` y resuelva el conflicto de puertos como se indica arriba.

## Relacionados

- [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Descripción general del servidor TCI](overview.md)
