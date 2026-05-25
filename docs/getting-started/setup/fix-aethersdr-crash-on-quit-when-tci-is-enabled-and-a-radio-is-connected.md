# Solucionar el cierre inesperado de AetherSDR al salir cuando TCI está habilitado y hay una radio conectada

AetherSDR v0.9.6 y versiones anteriores podían cerrarse inesperadamente al salir cuando el servidor TCI estaba en ejecución y había una radio conectada. La versión 0.9.7 soluciona este problema. Si aún experimenta un cierre inesperado al salir, los siguientes pasos confirman que está ejecutando la versión corregida y lo guían a través de una configuración TCI limpia.

## Antes de comenzar

- Está ejecutando AetherSDR v0.9.7 o posterior. Las compilaciones anteriores contienen el defecto de uso después de liberación que causaba el cierre inesperado; actualizar es la única solución completa.
- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI es visible. Si no lo está, haga clic en el botón de la bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1. Salga de AetherSDR usando `File > Quit` o el atajo de teclado `Ctrl+Q`.
2. Si la aplicación se cierra inesperadamente en este punto, confirme que su versión instalada sea v0.9.7 o posterior. Si no lo es, actualice antes de continuar.
3. Después de actualizar, vuelva a abrir AetherSDR y conéctese a su radio.
4. Abra el applet TCI haciendo clic en el botón de la bandeja `TCI` en la barra lateral derecha si aún no es visible.
5. En el campo `Port`, confirme que el valor del puerto esté entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está en blanco o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
6. Haga clic en `Enable` para iniciar el servidor TCI.
7. Confirme que el indicador de estado junto a `Enable` muestre `:<port> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte Solución de problemas más abajo.
8. Use la radio normalmente y luego salga con `File > Quit`. La aplicación debería cerrarse correctamente.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                                 | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo `Port`                   | `50001`                                                                                                                              | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Alternador `Enable`            | Apagado                                                                                                                              | Encendido / Apagado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Ganancia+medidor RX1           | 0.5                                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX2           | 0.5                                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX3           | 0.5                                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX4           | 0.5                                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX            | 0.5                                                                                                                                  | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Modo de desbordamiento TX (clic derecho) | Clip (0)                                                                                                                             | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

Los valores fuera de rango ingresados en el campo `Port` se ajustan a `50001`. Si `Enable` se activa y la vinculación falla, el botón vuelve a apagado y el estado muestra `(port in use)`.

### Detalles de ganancia+medidor TX

Los arrastres establecen la ganancia TX de TCI y emiten `tciTxGainChanged`. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado.

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú contextual del modo de desbordamiento TX. Esto le permite elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:

- **Clip (saturación ±1.0)** — Recorta forzosamente los excesos a ±1.0. Este es el valor predeterminado heredado; protege la conversión a int16 aguas abajo pero introduce armónicos en los excesos.
- **NaN guard (solo cero NaN/Inf)** — Pasa las muestras bit a bit exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad del tono del modo digital. Los valores flotantes fuera de rango llegan a la radio.
- **Measure only (bypass verdadero)** — Nunca modifica las muestras. Cuenta los excesos solo para telemetría. La conversión a int16 aguas abajo aún recorta en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es `Clip` para que los usuarios existentes no vean cambios en el comportamiento.

### Etiquetas de asignación de slices

Las filas RX1–RX4 y TX muestran una etiqueta que indica qué slice está manejando actualmente ese canal. La etiqueta muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando un slice está activo. Estas etiquetas comparten la asignación del canal DAX.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada ejecución. Esta configuración existía antes de v0.9.7 y es segura de usar después de actualizar.
- El cierre inesperado en versiones anteriores ocurría porque el servidor TCI se desmontaba después de que el modelo de radio ya se hubiera liberado. En v0.9.7, el orden de desmontaje se corrigió: el servidor TCI se apaga mientras el modelo de radio aún está activo. Ningún cambio de configuración de su parte desencadena o evita esto — actualizar a v0.9.7 es la solución.
- A partir de v26.5.2.1, las etiquetas de asignación de slices (estado RX1–RX4 y estado TX) pueden representar texto enriquecido. Si una letra de slice contiene caracteres HTML (como un ampersand o corchetes angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado sin procesar. Esto mejora la compatibilidad con software de terceros que pueda enviar identificadores de slice inusuales.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Ingrese un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación aún se cierra inesperadamente al salir después de actualizar** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para ver la cadena de versión. Si la versión es correcta y los cierres inesperados persisten, desactive `Enable` antes de salir para aislar si TCI sigue involucrado.
- **`Enable` vuelve a apagado inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.
- **La etiqueta de asignación de slice muestra HTML sin procesar** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la versión más reciente para garantizar la representación adecuada de los identificadores de slice.

## Relacionado

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
