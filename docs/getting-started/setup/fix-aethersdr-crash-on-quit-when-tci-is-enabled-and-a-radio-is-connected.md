# Solución al cierre inesperado de AetherSDR al salir cuando TCI está habilitado y un radio está conectado

AetherSDR v0.9.6 y versiones anteriores podían cerrarse de forma inesperada al salir cuando el servidor TCI estaba en ejecución y un radio estaba conectado. La versión 0.9.7 corrige este problema. Si sigue experimentando un cierre inesperado al salir, los pasos a continuación le permiten confirmar que está ejecutando la versión corregida y le guían para realizar una configuración limpia de TCI.

## Antes de comenzar

- Debe estar ejecutando AetherSDR v0.9.7 o posterior. Las versiones anteriores contienen el defecto de uso tras liberación de memoria que causaba el cierre inesperado; actualizar es la única solución completa.
- Un radio FLEX-8600 debe estar conectado y visible en la aplicación.
- El applet de TCI debe estar visible. Si no lo está, haga clic en el botón `TCI` de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Cierre AetherSDR usando `File > Quit` o el atajo de teclado `Ctrl+Q`.
2. Si la aplicación se cierra de forma inesperada en este punto, confirme que la versión instalada es v0.9.7 o posterior. Si no lo es, actualice antes de continuar.
3. Tras actualizar, vuelva a abrir AetherSDR y conéctese a su radio.
4. Abra el applet de TCI haciendo clic en el botón `TCI` de la bandeja en la barra lateral derecha, si no está visible todavía.
5. En el campo `Port`, confirme que el valor del puerto está entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está vacío o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
6. Haga clic en `Enable` para iniciar el servidor TCI.
7. Confirme que el indicador de estado junto a `Enable` muestra `:<port> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte la sección Solución de problemas a continuación.
8. Use el radio normalmente y luego cierre la aplicación con `File > Quit`. La aplicación debería cerrarse sin problemas.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Campo `Port` | `50001` | 1024–65535 | `TciPort` |
| Interruptor `Enable` | Desactivado | Activado / Desactivado | — |
| Ganancia+medidor RX1 | 0.5 | 0.0–1.0 | `TciRxGain1` |
| Ganancia+medidor RX2 | 0.5 | 0.0–1.0 | `TciRxGain2` |
| Ganancia+medidor RX3 | 0.5 | 0.0–1.0 | `TciRxGain3` |
| Ganancia+medidor RX4 | 0.5 | 0.0–1.0 | `TciRxGain4` |
| Ganancia+medidor TX | 0.5 | 0.0–1.0 | `TciTxGain` |

Los valores fuera de rango ingresados en el campo `Port` se ajustan automáticamente a `50001`. Si `Enable` se activa y el enlace falla, el botón vuelve al estado desactivado y el estado muestra `(port in use)`.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada arranque. Esta configuración existía antes de la v0.9.7 y es segura de usar tras la actualización.
- El cierre inesperado en versiones anteriores ocurría porque el servidor TCI se cerraba después de que el modelo de radio ya había sido liberado. En la v0.9.7 se corrigió el orden de cierre: el servidor TCI se detiene mientras el modelo de radio aún está activo. Ningún cambio de configuración por su parte provoca ni evita este problema — actualizar a la v0.9.7 es la solución.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está enlazado a ese puerto. Ingrese un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación sigue cerrándose de forma inesperada al salir después de actualizar** — Confirme que está ejecutando la v0.9.7 o posterior. Revise la cadena de versión en `Help > About`. Si la versión es correcta y los cierres inesperados persisten, desactive `Enable` antes de salir para determinar si TCI sigue siendo el origen del problema.
- **`Enable` vuelve al estado desactivado de inmediato** — El enlace del puerto falló. La etiqueta de estado se muestra en rojo e indica `(port in use)`. Cambie el valor del puerto e intente nuevamente.

## Relacionados

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
