# Solucionar el cierre inesperado de AetherSDR al salir cuando TCI está habilitado y hay una radio conectada

AetherSDR v0.9.6 y versiones anteriores podían cerrarse inesperadamente al salir cuando el servidor TCI estaba ejecutándose y había una radio conectada. La versión 0.9.7 corrige este problema. Si aún experimenta un cierre inesperado al salir, los pasos siguientes confirman que está ejecutando la versión corregida y lo guían a través de una configuración TCI limpia.

## Antes de comenzar

- Está ejecutando AetherSDR v0.9.7 o posterior. Las compilaciones anteriores contienen el defecto de uso después de liberación (use-after-free) que causaba el cierre inesperado; la actualización es la única solución completa.
- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI está visible. Si no lo está, haga clic en el botón de la bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1. Cierre AetherSDR usando `File > Quit` o el atajo de teclado `Ctrl+Q`.
2. Si la aplicación se cierra inesperadamente en este punto, confirme que su versión instalada sea v0.9.7 o posterior. Si no lo es, actualice antes de continuar.
3. Después de actualizar, vuelva a abrir AetherSDR y conéctese a su radio.
4. Abra el applet TCI haciendo clic en el botón de la bandeja `TCI` en la barra lateral derecha si aún no está visible.
5. En el campo `Port`, confirme que el valor del puerto esté entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está vacío o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
6. Haga clic en `Enable` para iniciar el servidor TCI.
7. Confirme que el indicador de estado junto a `Enable` muestre `:<port> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte la sección Solución de problemas a continuación.
8. Use la radio normalmente, luego salga con `File > Quit`. La aplicación debería cerrarse sin problemas.

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

Los valores fuera de rango ingresados en el campo `Port` se ajustan a `50001`. Si el interruptor `Enable` se activa y la vinculación falla, el botón vuelve a apagado y el estado muestra `(port in use)`.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada inicio. Esta configuración existía antes de v0.9.7 y es seguro usarla después de actualizar.
- El cierre inesperado en versiones anteriores ocurría porque el servidor TCI se desmontaba después de que el modelo de radio ya se hubiera liberado. En v0.9.7, el orden de desmontaje se corrigió: el servidor TCI se apaga mientras el modelo de radio sigue activo. Ningún cambio de configuración por su parte provoca o evita esto; la actualización a v0.9.7 es la solución.
- A partir de v26.5.2.1, las etiquetas de asignación de segmento (estado RX1–RX4 y estado TX) pueden representar texto enriquecido. Si una letra de segmento contiene caracteres HTML (como un ampersand o paréntesis angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado en bruto. Esto mejora la compatibilidad con software de terceros que pueda enviar identificadores de segmento inusuales.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Ingrese un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación aún se cierra inesperadamente al salir después de actualizar** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para ver la cadena de versión. Si la versión es correcta y los cierres persisten, desactive `Enable` antes de salir para aislar si TCI sigue involucrado.
- **`Enable` vuelve a apagado inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.
- **La etiqueta de asignación de segmento muestra HTML en bruto** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la última versión para garantizar la representación correcta de los identificadores de segmento.

## Relacionado

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
