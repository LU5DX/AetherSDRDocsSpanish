# Inicio automático de TCI al arrancar

Esta página explica cómo hacer que AetherSDR inicie el servidor TCI automáticamente cada vez que se abre la aplicación, de modo que no sea necesario habilitarlo manualmente tras cada reinicio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio activa.
- Decida qué puerto debe usar el servidor TCI. El valor predeterminado es `50001`. Si necesita un puerto diferente, configúrelo antes de habilitar el inicio automático. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).

## Pasos

1. Abra el applet TCI haciendo clic en el botón de bandeja **TCI** en la barra lateral derecha. Si el panel del applet no es visible, habilítelo mediante `View > Applet Panel`.
2. Haga clic en `Settings > Autostart TCI with AetherSDR`.
   Aparece una marca de verificación junto al elemento del menú. AetherSDR guarda `AutoStartTCI` = `True` e iniciará el servidor TCI en cada arranque posterior.
3. Para confirmar que la configuración está activa, cierre y vuelva a abrir AetherSDR. El indicador de estado del servidor TCI en el applet debe mostrar `:<puerto> (0 clients)` en lugar de `(stopped)`.

Para desactivar el inicio automático, haga clic nuevamente en `Settings > Autostart TCI with AetherSDR` para quitar la marca de verificación.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| `Settings > Autostart TCI with AetherSDR` | Desactivado (sin marcar) | Activado / Desactivado | `AutoStartTCI` | Cuando está marcado, inicia el servidor TCI al arrancar en el puerto guardado. |
| Campo de puerto | `50001` | 1024–65535 | `TciPort` | Define el puerto al que se enlaza el servidor. Los valores fuera del rango válido se ajustan a `50001`. Cambiar el puerto mientras el servidor está en ejecución lo reinicia automáticamente. |
| Enable | Desactivado | Activado / Desactivado | — | Inicia o detiene el servidor TCI de inmediato. Al activar o desactivar este control también se actualiza `AutoStartTCI`. Si el puerto ya está en uso, el botón vuelve a la posición de desactivado y el estado muestra `(port in use)`. |

## Consejos

- Habilitar el inicio automático mediante el menú y hacer clic en Enable en el applet escriben igualmente `AutoStartTCI`. Si habilita el servidor haciendo clic en Enable en el applet, el inicio automático también queda configurado, lo que significa que el próximo arranque iniciará el servidor automáticamente.
- Si el servidor no puede enlazarse al arrancar (puerto en uso), el indicador de estado se pone en rojo y muestra `(port in use)`. Cambie el puerto y vuelva a habilitarlo.

## Solución de problemas

- **El estado muestra `(stopped)` tras el rearranque aunque el inicio automático esté marcado** — Es posible que otra aplicación haya tomado el puerto antes de que AetherSDR iniciara. Cambie el puerto en el campo de puerto a uno libre (1024–65535) y vuelva a habilitar el inicio automático.
- **`Settings > Autostart TCI with AetherSDR` no aparece en el menú** — Esta versión de AetherSDR fue compilada sin soporte de WebSocket. Las funciones TCI no están disponibles.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Descripción general del servidor TCI](overview.md)
