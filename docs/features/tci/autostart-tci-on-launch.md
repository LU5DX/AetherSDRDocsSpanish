# Inicio automático de TCI al lanzar la aplicación

Configure AetherSDR para iniciar el servidor WebSocket de TCI automáticamente cada vez que se inicia la aplicación, de modo que software de terceros como Log4OM o las herramientas SunSDR se conecte sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de bandeja de TCI no aparece, esta compilación no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede establecerse mientras está desconectada.
- Decida qué puerto debe utilizar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de habilitar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento está marcado. AetherSDR iniciará el servidor TCI en cada arranque posterior.
3. Para verificar que la configuración surtió efecto de inmediato, haga clic en el botón de bandeja de TCI en la barra lateral derecha para abrir el applet TCI Server. El estado del servidor debe mostrar `:<port> (0 clients)` en lugar de `(stopped)`.

Para deshabilitar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcarlo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida |
|---|---|---|---|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú con marca) | Desactivado | Activado / Desactivado | `AutoStartTCI` |
| Puerto | `50001` | 1024–65535 | `TciPort` |
| Enable (botón de alternancia en el applet TCI Server) | Desactivado | Activado / Desactivado | — |
| Ganancia+medidor RX1–RX4 | 0.5 | 0.0–1.0 | `TciRxGain1` – `TciRxGain4` |
| Ganancia+medidor TX | 0.5 | 0.0–1.0 | `TciTxGain` |

## Consejos

- Habilitar el inicio automático también establece `AutoStartTCI` en `True`. Al alternar Enable en el applet TCI Server se escribe la misma clave, por lo que ambos controles permanecen sincronizados.
- Si el puerto ya está en uso al iniciar, el servidor no arrancará: el botón Enable vuelve a desactivado y el estado muestra `(port in use)`. Cambie el puerto y reinicie AetherSDR, o cierre el proceso que genera el conflicto.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta compilación de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(port in use)` después del inicio** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Port del applet TCI Server, guarde y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece en `(stopped)` aunque el inicio automático esté habilitado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
