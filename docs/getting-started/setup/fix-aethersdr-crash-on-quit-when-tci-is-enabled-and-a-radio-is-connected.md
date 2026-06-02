# Solucionar el bloqueo de AetherSDR al salir cuando TCI está habilitado y hay una radio conectada

AetherSDR v0.9.6 y versiones anteriores podían bloquearse al salir cuando el servidor TCI estaba en ejecución y había una radio conectada. La versión 0.9.7 corrige este problema. Si aún experimenta un bloqueo al salir, los pasos a continuación confirman que está usando la versión corregida y lo guían a través de una configuración TCI limpia.

## Antes de comenzar

- Está ejecutando AetherSDR v0.9.7 o posterior. Las compilaciones anteriores contienen el defecto de use-after-free que causaba el bloqueo; la actualización es la única solución completa.
- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI está visible. Si no lo está, haga clic en el botón de la bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1. Salga de AetherSDR usando `File > Quit` o el atajo de teclado `Ctrl+Q`.
2. Si la aplicación se bloquea en este punto, confirme que su versión instalada es v0.9.7 o posterior. Si no lo es, actualice antes de continuar.
3. Después de actualizar, vuelva a abrir AetherSDR y conéctese a su radio.
4. Abra el applet TCI haciendo clic en el botón de la bandeja `TCI` en la barra lateral derecha si aún no está visible.
5. En el campo `Port`, confirme que el valor del puerto esté entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está vacío o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
6. Haga clic en `Enable` para iniciar el servidor TCI.
7. Confirme que el indicador de estado junto a `Enable` muestre `:<puerto> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte Solución de problemas a continuación.
8. Use la radio normalmente, luego salga con `File > Quit`. La aplicación debería cerrarse sin problemas.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                         | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo `Port`                   | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
 | Alternar `Enable`              | Desactivado                                                                                                                 | Activado / Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Ganancia+medidor RX1           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX2           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX3           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX4           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX            | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste `TciTxGain` internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo cero NaN/Inf) o Measure (bypass real con conteo de clips). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho) | Clip (0)                                                                                                                    | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

Los valores fuera de rango ingresados en el campo `Port` se ajustan a `50001`. Si `Enable` se activa y la vinculación falla, el botón vuelve a desactivarse y el estado muestra `(port in use)`.

### Detalles de ganancia+medidor TX

Los arrastres establecen la ganancia TX de TCI y emiten `tciTxGainChanged`. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado.

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú contextual de modo de desbordamiento TX. Esto le permite elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modo digital:

- **Clip (saturación ±1.0)** — Sujeta firmemente los picos a ±1.0. Este es el valor predeterminado heredado; protege la conversión int16 posterior pero introduce armónicos en los picos.
- **NaN guard (solo cero NaN/Inf)** — Pasa las muestras de forma idéntica al bit; solo pone a cero los valores patológicos NaN/Inf. Conserva la fidelidad del tono en modo digital. Los valores flotantes fuera de rango llegan a la radio.
- **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los picos solo para telemetría. La conversión int16 posterior aún sujeta en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es `Clip` para que los usuarios existentes no vean cambios de comportamiento.

### Etiquetas de asignación de slice

Las filas RX1–RX4 y TX muestran una etiqueta que indica qué slice está utilizando actualmente ese canal. La etiqueta muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando hay un slice activo. Estas etiquetas comparten la asignación del canal DAX.

### Indicador de estado del servidor

La etiqueta de estado junto a `Enable` muestra el estado del servidor y el número de clientes conectados:

- `(stopped)` — El servidor no está en ejecución.
- `:<puerto> (N clients)` — El servidor se está ejecutando en el puerto especificado con N clientes conectados.
- `(port in use)` — El servidor no pudo iniciarse porque otro proceso está vinculado al puerto.

La etiqueta se estiliza usando el tema de la aplicación. En versiones anteriores, la etiqueta usaba un color fijo; en v26.6.1, el color se deriva del color `background.3` del tema para una apariencia coherente en temas claro y oscuro.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada inicio. Esta configuración existía antes de v0.9.7 y es segura de usar después de la actualización.
- El bloqueo en versiones anteriores ocurría porque el servidor TCI se cerraba después de que el modelo de radio ya se había liberado. En v0.9.7, se corrigió el orden de cierre: el servidor TCI se apaga mientras el modelo de radio aún está activo. Ningún cambio de configuración de su parte provoca o evita esto: la actualización a v0.9.7 es la solución.
- A partir de v26.5.2.1, las etiquetas de asignación de slice (estado RX1–RX4 y estado TX) pueden representar texto enriquecido. Si una letra de slice contiene caracteres HTML (como un ampersand o corchetes angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado sin procesar. Esto mejora la compatibilidad con software de terceros que puede enviar identificadores de slice inusuales.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Ingrese un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación aún se bloquea al salir después de la actualización** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para la cadena de versión. Si la versión es correcta y los bloqueos persisten, desactive `Enable` antes de salir para aislar si TCI todavía está involucrado.
- **`Enable` se desactiva inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.
- **La etiqueta de asignación de slice muestra HTML sin procesar** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la última versión para garantizar una representación correcta de los identificadores de slice.

## Relacionado

- [Resumen del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
