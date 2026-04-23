# Cambiar el puerto TCI

El servidor TCI escucha en un puerto TCP configurable. Cambie el puerto si el valor predeterminado entra en conflicto con otra aplicación o si su software de registro o de modos digitales requiere un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión activa con el radio.
- Abra el applet TCI haciendo clic en el botón **TCI** de la bandeja en la barra lateral derecha, si no está visible todavía.

## Pasos

1. Localice el campo **Port** en la parte inferior del applet TCI, a la derecha de la etiqueta "Port:".
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`.
3. Presione **Enter** o haga clic fuera del campo para confirmar. Si ingresa un valor fuera del rango 1024–65535, el campo se restablece a `50001` y guarda ese valor.
4. Si el servidor ya está en ejecución (Enable está marcado), se reinicia automáticamente en el nuevo puerto. No se requiere ninguna acción adicional.

El nuevo puerto se guarda en `TciPort` y persiste entre sesiones.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Configuración guardada |
|---|---|---|---|
| Campo **Port** | `50001` | 1024–65535 | `TciPort` |
| Interruptor **Enable** | Desactivado | Activado / Desactivado | — |
| Indicador de estado del servidor | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — |

## Consejos

- El indicador de estado del servidor se actualiza inmediatamente después de un cambio de puerto. Si el estado muestra `(port in use)` y **Enable** vuelve a aparecer desmarcado, otro proceso ya está enlazado a ese puerto. Elija un número de puerto diferente.
- Si tiene habilitada la opción `Settings > Autostart TCI with AetherSDR`, el valor guardado en `TciPort` se utiliza en el siguiente inicio sin necesidad de ninguna acción adicional.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — El puerto ya está en uso por otra aplicación. Ingrese un número de puerto diferente y haga clic en **Enable** nuevamente.
- **El campo Port se restablece a 50001** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro de ese rango.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
