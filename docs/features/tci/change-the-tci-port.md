# Cambiar el puerto TCI

El servidor TCI escucha en un puerto configurable para que el software de terceros pueda conectarse a él. Cambie el puerto si el predeterminado entra en conflicto con otra aplicación o si su software de registro o de modos digitales requiere un número de puerto específico.

## Antes de comenzar

- El applet TCI debe estar visible. Si no lo está, haga clic en el botón TCI del área de notificación en la barra lateral derecha para mostrarlo.
- Debe haber una conexión de radio activa.

## Pasos

1. Abra el applet TCI haciendo clic en el botón TCI del área de notificación en la barra lateral derecha.
2. Haga clic en el campo Port (predeterminado: `50001`) y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. Los valores fuera de este rango vuelven automáticamente a `50001`.
3. Presione Enter o Tab para confirmar. AetherSDR guarda el valor en `TciPort` de inmediato.
4. Si el servidor ya está en ejecución (Enable está marcado), AetherSDR reinicia el servidor en el nuevo puerto de forma automática. No se requiere ninguna acción adicional.
5. Si el servidor aún no está en ejecución, haga clic en Enable para iniciarlo en el nuevo puerto.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Port | `50001` | 1024–65535 | `TciPort` | Establece el puerto WebSocket al que se vincula el servidor TCI. Los valores fuera de rango vuelven a `50001`. Cambiar el puerto mientras el servidor está en ejecución lo reinicia. |
| Enable | Off | On / Off | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor vuelve a la posición off y el indicador de estado muestra `(port in use)` en rojo. |

## Consejos

- El indicador de estado junto a Enable muestra `:<port> (N clients)` cuando el servidor está en ejecución, lo que permite confirmar que el nuevo puerto surtió efecto sin necesidad de abrir una terminal.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a off** — Otra aplicación está vinculada a ese puerto. Elija un número de puerto diferente y haga clic en Enable nuevamente.
- **El campo Port vuelve a `50001` después de escribir un número** — El valor introducido estaba fuera del rango 1024–65535. Introduzca un valor dentro de ese rango.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
