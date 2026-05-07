# Solucionar el cierre inesperado de AetherSDR al salir cuando TCI está habilitado y una radio está conectada

AetherSDR v0.9.6 y versiones anteriores podían cerrarse inesperadamente al salir cuando el servidor TCI estaba en ejecución y una radio estaba conectada. La versión 0.9.7 soluciona este problema. Si aún experimenta un cierre inesperado al salir, los pasos siguientes confirman que está ejecutando la versión corregida y le guían a través de una configuración TCI limpia.

## Antes de comenzar

- Está ejecutando AetherSDR v0.9.7 o posterior. Las versiones anteriores contienen el defecto de uso después de liberación que causaba el cierre inesperado; actualizar es la única solución completa.
- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI está visible. Si no lo está, haga clic en el botón de bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1.  Salga de AetherSDR usando `File > Quit` o el atajo de teclado `Ctrl+Q`.
2.  Si la aplicación se cierra inesperadamente en este punto, confirme que su versión instalada es v0.9.7 o posterior. Si no lo es, actualice antes de continuar.
3.  Después de actualizar, vuelva a abrir AetherSDR y conéctese a su radio.
4.  Abra el applet TCI haciendo clic en el botón de bandeja `TCI` en la barra lateral derecha si aún no está visible.
5.  En el campo `Port`, confirme que el valor del puerto está entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está en blanco o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
6.  Haga clic en `Enable` para iniciar el servidor TCI.
7.  Confirme que el indicador de estado junto a `Enable` muestra `:<port> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte la sección de Solución de problemas a continuación.
8.  Use la radio con normalidad y luego salga con `File > Quit`. La aplicación debería cerrarse sin problemas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Campo `Port` | `50001` | 1024–65535 | `TciPort` |
| Interruptor `Enable` | Apagado | Encendido / Apagado | — |
| Ganancia+medidor RX1 | 0.5 | 0.0–1.0 | `TciRxGain1` |
| Ganancia+medidor RX2 | 0.5 | 0.0–1.0 | `TciRxGain2` |
| Ganancia+medidor RX3 | 0.5 | 0.0–1.0 | `TciRxGain3` |
| Ganancia+medidor RX4 | 0.5 | 0.0–1.0 | `TciRxGain4` |
| Ganancia+medidor TX | 0.5 | 0.0–1.0 | `TciTxGain` |

Los valores fuera de rango ingresados en el campo `Port` se ajustan a `50001`. Si se activa `Enable` y la vinculación falla, el botón vuelve a la posición de apagado y el estado muestra `(port in use)`.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada lanzamiento. Esta configuración existía antes de v0.9.7 y es segura de usar después de la actualización.
- El cierre inesperado en versiones anteriores ocurría porque el servidor TCI se desmontaba después de que el modelo de radio ya se hubiera liberado. En v0.9.7, el orden de desmontaje se corrigió: el servidor TCI se apaga mientras el modelo de radio aún está activo. Ningún cambio de configuración de su parte desencadena o evita esto — actualizar a v0.9.7 es la solución.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Ingrese un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación aún se cierra inesperadamente al salir después de la actualización** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para la cadena de versión. Si la versión es correcta y los cierres inesperados persisten, deshabilite `Enable` antes de salir para aislar si TCI aún está involucrado.
- **`Enable` vuelve a apagarse inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.

## Relacionado

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al lanzar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
