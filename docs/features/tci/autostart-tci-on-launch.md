# Inicio automático de TCI al arrancar

Configure AetherSDR para que inicie el servidor WebSocket TCI automáticamente cada vez que la aplicación se ejecute, de modo que programas de terceros como Log4OM o las herramientas de SunSDR se conecten sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar compilado con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de bandeja de TCI no aparece, esta versión no incluye TCI.
- La radio debe estar conectada antes de que el servidor TCI pueda atender clientes, aunque la configuración de inicio automático puede realizarse estando desconectado.
- Decida qué puerto debe usar el servidor. El valor predeterminado es `50001`. Consulte [Cambiar el puerto TCI](change-the-tci-port.md) si necesita un puerto diferente antes de activar el inicio automático.

## Pasos

1. Haga clic en `Settings > Autostart TCI with AetherSDR`.
2. Confirme que el elemento está marcado. AetherSDR iniciará el servidor TCI en cada arranque posterior.
3. Para verificar que la configuración tuvo efecto de inmediato, haga clic en el botón de bandeja TCI en la barra lateral derecha para abrir el applet TCI Server. El estado del servidor debe mostrar `:<port> (0 clients)` en lugar de `(stopped)`.

Para desactivar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para desmarcar la opción.

## Qué hace cada control

| Control                                                          | Valor predeterminado                                                | Rango válido                                                                                                                                                                                                                                                        |
|------------------------------------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Settings > Autostart TCI with AetherSDR` (elemento de menú con casilla) | Desactivado                                              | Activado / Desactivado                                                                                                                                                                                                                                              |
| Puerto                                                           | `50001`                                                             | 1024–65535                                                                                                                                                                                                                                                          |
| Enable (botón de alternancia en el applet TCI Server)            | Desactivado                                                         | Activado / Desactivado                                                                                                                                                                                                                                              |
| Ganancia+medidor RX1–RX4                                         | 0.5                                                                 | 0.0–1.0                                                                                                                                                                                                                                                             |
| Ganancia+medidor TX                                              | Los deslizadores establecen la ganancia TX de TCI y emiten tciTxGainChanged. | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |

## Consejos

- Activar el inicio automático también establece `AutoStartTCI` en `True`. Alternar Enable en el applet TCI Server escribe la misma clave, por lo que ambos controles permanecen sincronizados.
- Si el puerto ya está en uso al arrancar, el servidor no se iniciará: el alternador Enable vuelve automáticamente a desactivado y el estado muestra `(port in use)`. Cambie el puerto y reinicie AetherSDR, o cierre el proceso que genera el conflicto.
- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.

## Solución de problemas

- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta versión de AetherSDR no incluye soporte WebSocket. TCI no está disponible.
- **El estado del servidor muestra `(port in use)` tras el arranque** — Otro proceso ya está vinculado al puerto configurado. Cambie el puerto en el campo Port del applet TCI Server, guarde los cambios y reinicie AetherSDR. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El estado permanece en `(stopped)` aunque el inicio automático esté activado** — La radio aún no está conectada. El servidor TCI requiere una conexión de radio. Conéctese a la radio; el servidor se iniciará una vez que se establezca la conexión.

## Relacionado

- [Descripción general del servidor TCI](overview.md)
- [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
