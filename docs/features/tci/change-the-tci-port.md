# Cambiar el puerto TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su software de registro o de modos digitales requiera un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión de radio activa.
- Abra el applet TCI haciendo clic en el botón **TCI** de la barra lateral derecha si no está visible.

## Pasos

1. En el applet TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango vuelven automáticamente a `50001`.
3. Presione **Enter** o mueva el foco fuera del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está en ejecución (Enable está marcado), AetherSDR detiene el servidor y lo reinicia en el nuevo puerto de forma automática. No se requiere ninguna acción adicional.
5. Si el servidor no está en ejecución, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Campo **Port** | `50001` | 1024–65535 | `TciPort` | Establece el puerto WebSocket. Los valores fuera de rango vuelven a `50001`. Si el servidor está habilitado, cambiar el puerto lo reinicia de inmediato. |
| **Enable** | Desactivado | Activado / Desactivado | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor vuelve a desactivado y el estado muestra `(port in use)`. |
| Indicador de estado del servidor | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — | Muestra el estado actual del servidor. Se vuelve rojo si falla el enlace. |

## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados serán desconectados y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(port in use)` después de hacer clic en **Enable**, elija un número de puerto diferente e inténtelo de nuevo.

## Solución de problemas

- **El estado muestra `(port in use)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** de nuevo.
- **El campo Port vuelve a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
