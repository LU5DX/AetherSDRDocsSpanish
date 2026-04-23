# Inicio automático de TCI al arrancar

Configure AetherSDR para iniciar el servidor TCI automáticamente cada vez que la aplicación se inicia, de modo que programas de terceros como Log4OM o las herramientas de SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el elemento de menú `Settings > Autostart TCI with AetherSDR` no aparece, su compilación no incluye TCI.
- Confirme que el servidor TCI funciona manualmente antes de habilitar el inicio automático. Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- Se requiere una conexión de radio para que el servidor TCI funcione tras el arranque.

## Pasos

1. Abra el menú `Settings`.
2. Haga clic en `Autostart TCI with AetherSDR`. Aparece una marca de verificación junto al elemento cuando está activo.
3. Reinicie AetherSDR. El servidor TCI se inicia automáticamente en el puerto almacenado en `TciPort` (predeterminado `50001`).

Para deshabilitar el inicio automático, repita los pasos 1–2. La marca de verificación se elimina y el servidor ya no se iniciará al arrancar.

## Función de cada control

| Control | Predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Elemento de menú `Autostart TCI with AetherSDR` | Desactivado (sin marcar) | Activado / Desactivado | `AutoStartTCI` |
| Campo de puerto | `50001` | 1024–65535 | `TciPort` |
| Ganancia RX1 | 0.5 | 0.0–1.0 | `TciRxGain1` |
| Ganancia RX2 | 0.5 | 0.0–1.0 | `TciRxGain2` |
| Ganancia RX3 | 0.5 | 0.0–1.0 | `TciRxGain3` |
| Ganancia RX4 | 0.5 | 0.0–1.0 | `TciRxGain4` |
| Ganancia TX | 0.5 | 0.0–1.0 | `TciTxGain` |

## Consejos

- El inicio automático utiliza el puerto guardado en `TciPort` en el momento del arranque. Establezca el puerto correcto antes de habilitar el inicio automático para evitar tener que cambiarlo después. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- Si el puerto guardado ya está en uso cuando AetherSDR se inicia, el servidor no podrá vincularse. El indicador de estado del applet TCI mostrará `(port in use)` en rojo y el botón `Enable` estará desactivado. Cambie el puerto y haga clic en `Enable` manualmente.
- Los valores de ganancia (`TciRxGain1`–`TciRxGain4`, `TciTxGain`) se guardan de forma independiente del inicio automático. Persisten entre reinicios independientemente de si el inicio automático está habilitado.

## Solución de problemas

- **`Autostart TCI with AetherSDR` no aparece en el menú Settings** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El servidor no se inicia tras el arranque a pesar de tener el inicio automático habilitado** — La conexión de radio no se había establecido antes del intento de inicio automático, o el puerto configurado estaba en uso. Abra el applet TCI mediante el botón de bandeja `TCI` y revise el indicador de estado. Corrija el puerto si es necesario y haga clic en `Enable`.
- **El estado muestra `(port in use)` al arrancar** — Otra aplicación está vinculada a `TciPort`. Cambie el puerto en el campo Port del applet TCI a un puerto libre en el rango 1024–65535 y haga clic en `Enable`. Actualice `TciPort` antes del próximo reinicio.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
