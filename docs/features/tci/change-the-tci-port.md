# Cambiar el puerto TCI

Cambie el puerto en el que escucha el servidor WebSocket TCI para evitar conflictos con otros programas de su sistema.

## Antes de comenzar

- La radio debe estar conectada. El applet TCI no está disponible sin una conexión de radio.
- Abra el applet TCI haciendo clic en el botón TCI del área de notificación en la barra lateral derecha, si no está visible todavía.

## Pasos

1. En el applet TCI, localice el campo Port junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo Port y escriba el nuevo número de puerto. Rango válido: 1024–65535. Valor predeterminado: `50001`. Los valores fuera de este rango vuelven automáticamente a `50001`.
3. Presione Enter o Tab para confirmar el cambio. AetherSDR guarda el valor en `TciPort` de inmediato.
4. Si el servidor ya está en ejecución (Enable está activado), AetherSDR detiene y reinicia el servidor en el nuevo puerto de forma automática. No es necesario reiniciarlo manualmente.
5. Confirme que el nuevo puerto está activo revisando el indicador de estado junto al campo Port. Muestra `:<port> (N clients)` cuando el servidor está funcionando correctamente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Port | `50001` | 1024–65535 | `TciPort` | Establece el puerto TCP al que se enlaza el servidor WebSocket TCI. Los valores fuera de rango vuelven a `50001`. Si el servidor está en ejecución cuando se confirma el valor, se reinicia en el nuevo puerto. |
| Enable | Off | On / Off | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor vuelve a off y el estado muestra `(port in use)` en rojo. |

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a off** — Otro proceso ya está enlazado al puerto ingresado. Elija un número de puerto diferente, presione Enter para confirmarlo y luego haga clic en Enable nuevamente.
- **El campo Port vuelve a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
