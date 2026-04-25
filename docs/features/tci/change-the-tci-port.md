# Cambiar el puerto TCI

Cambie el puerto en el que escucha el servidor WebSocket de TCI. Haga esto cuando el puerto predeterminado entre en conflicto con otra aplicación o cuando su software de registro o de modos digitales requiera un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600. El applet de TCI no está disponible sin una conexión de radio.
- Abra el applet de TCI haciendo clic en el botón TCI de la bandeja en la barra lateral derecha, si no está visible todavía.

## Pasos

1. En el applet de TCI, ubique el campo Port junto a la etiqueta "Port:".
2. Haga clic en el campo Port y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango vuelven automáticamente a `50001`.
3. Presione Enter o Tab para confirmar el cambio. La configuración se guarda inmediatamente en `TciPort`.
4. Si el servidor está habilitado en ese momento, se reinicia automáticamente en el nuevo puerto. El indicador de estado se actualiza para mostrar el nuevo número de puerto y la cantidad de clientes conectados.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Port | `50001` | 1024–65535 | `TciPort` | Establece el puerto WebSocket. Si el servidor está en ejecución cuando se cambia el valor, el servidor se reinicia en el nuevo puerto. Los valores fuera de rango vuelven a `50001`. |
| Enable | Off | On / Off | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el botón vuelve a Off y el estado muestra `(port in use)`. |

## Consejos

- Si cambia el puerto mientras el servidor está detenido, el nuevo valor se guarda y se utiliza la próxima vez que haga clic en Enable.
- Informe al software cliente de TCI (Log4OM, herramientas SunSDR, etc.) el nuevo número de puerto antes de reiniciar el servidor; de lo contrario, los clientes no podrán conectarse.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a Off** — Otra aplicación ya está vinculada a ese puerto. Elija un número de puerto diferente y haga clic en Enable nuevamente.
- **Los clientes no pueden conectarse tras un cambio de puerto** — El software cliente todavía tiene configurado el puerto anterior. Actualice el puerto en el cliente y vuelva a conectarse.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
