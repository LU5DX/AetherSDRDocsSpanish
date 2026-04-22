# Cambiar el puerto TCI

Cambie el puerto en el que escucha el servidor WebSocket TCI. Haga esto cuando el puerto 50001 entre en conflicto con otra aplicación o cuando su software de registro o modos digitales espere un puerto diferente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión activa al radio.
- Tenga el applet TCI abierto. Si no está visible, haga clic en el botón **TCI** de la bandeja en la barra lateral derecha.

## Pasos

1. En el applet TCI, localice el campo **Port** en la parte inferior del panel.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`.
3. Presione **Enter** o haga clic fuera del campo para confirmar. Los valores fuera del rango 1024–65535 vuelven automáticamente a `50001`.
4. Si el servidor ya está en ejecución (Enable activo), AetherSDR detiene y reinicia el servidor en el nuevo puerto de forma automática. No se requiere ningún cambio manual.
5. El indicador de estado del servidor se actualiza para mostrar el nuevo puerto con el formato `:<port> (N clients)`.

El nuevo puerto se guarda en `TciPort` y persiste entre reinicios.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Port** | `50001` | 1024–65535 | `TciPort` | Establece el puerto al que se enlaza el servidor WebSocket TCI. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera de rango vuelven a `50001`. |
| **Enable** | Off | On / Off | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor vuelve a la posición off y el estado muestra `(port in use)`. |

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a off** — Otra aplicación ya está enlazada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en Enable nuevamente.
- **El campo Port vuelve a `50001` después de editar** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
