# Servidor TCI (Applet TCI)

AetherSDR puede ejecutar un servidor WebSocket TCI estilo Expert para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar la radio mediante el protocolo TCI. El audio TX de TCI se recibe a través del WebSocket y se introduce en una ranura de flujo `dax_tx` dedicada, independiente de la ruta de audio del dispositivo DAX2 del SmartSDR de Windows, por lo que la transmisión TCI funciona en todas las plataformas, incluyendo Windows y Linux sin PipeWire.

## Antes de comenzar

- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI es visible. Si no lo está, haga clic en el botón `TCI` de la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet TCI haciendo clic en el botón `TCI` de la barra lateral derecha si aún no es visible.
2. En el campo `Port`, escriba un valor de puerto entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está vacío o fuera de rango, escriba `50001` y presione Enter — el campo se ajusta automáticamente a `50001` para valores fuera de rango.
3. Haga clic en `Enable` para iniciar el servidor TCI. El texto del botón cambia a `Enabled` cuando el servidor está en ejecución. Si se habilitó `Settings > Autostart TCI with AetherSDR`, el botón comienza como `Enabled` y el servidor se inicia automáticamente.
4. Confirme que el indicador de estado junto a `Enable` muestra `:<puerto> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte Solución de problemas más abajo.
5. Configure su software de terceros para conectarse al servidor TCI en `localhost:<puerto>`.

## Qué hace cada control

| Control                        | Predeterminado                                                                                                             | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo `Port`                   | `50001`                                                                                                                     | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Alternancia `Enable`           | Desactivado (o Activado si el autoinicio está configurado)                                                                   | Activado / Desactivado. El texto del botón muestra `Enabled` o `Disabled`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Ganancia+medidor RX1           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX2           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX3           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX4           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX5           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX6           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX7           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX8           | 0.5                                                                                                                         | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX            | Arrastrar establece la ganancia TX de TCI y emite `tciTxGainChanged`. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | `TciServer::setTxGain` persiste `TciTxGain` internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre se permite independientemente de la plataforma o la disponibilidad de DAX alojado (`evaluateDaxTxPolicy` ahora permite incondicionalmente `DaxTxRequestReason::TciTxAudio`, v0.9.5.1, #2276). El menú de clic derecho permite elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf), o Measure (derivación verdadera con conteo de clips). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho) | Clip (0)                                                                                                                    | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Detalles de la alternancia Enable

El botón `Enable` es una alternancia que inicia o detiene el servidor TCI. El texto del botón cambia a `Enabled` cuando el servidor está en ejecución y a `Disabled` cuando se detiene. Si `Settings > Autostart TCI with AetherSDR` está habilitado, el botón se inicializa como `Enabled` y el servidor se inicia automáticamente al abrir la aplicación. Si falla la vinculación del puerto, el botón vuelve a `Disabled` y el estado muestra `(port in use)` en rojo.

### Detalles de ganancia+medidor RX

Cada canal RX (1–8) tiene un medidor y control deslizante combinados. Arrastre el control para establecer la ganancia RX de TCI para ese canal. El valor de ganancia se persiste por separado por canal como `TciRxGain1` hasta `TciRxGain8`. Cada control tiene un nombre accesible ("TCI RX 1 gain", "TCI RX 2 gain", etc.) para compatibilidad con lectores de pantalla.

El número de filas RX visibles está limitado por la capacidad de slices de la radio. En radios con menos de 8 slices, las filas RX por encima del número de slices están ocultas. Esto refleja el comportamiento del applet DAX. El índice del receptor TCI (trx) no está limitado a 4; es un índice posicional de slice limitado por el número de slices (hasta 8 en una FLEX-6700). Los canales DAX 5–8 tienen representación TCI.

### Detalles de ganancia+medidor TX

Arrastrar establece la ganancia TX de TCI y emite `tciTxGainChanged`. El audio TX de TCI siempre se permite independientemente de la plataforma o la disponibilidad de DAX alojado.

Haga clic derecho en el medidor/control de ganancia TX para abrir el menú contextual de modo de desbordamiento TX. Esto le permite elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales:

- **Clip (saturación ±1.0)** — Recorta los excesos a ±1.0. Este es el predeterminado heredado; protege la conversión posterior a int16 pero introduce armónicos en los excesos.
- **NaN guard (solo anula NaN/Inf)** — Pasa las muestras sin cambios bit exacto; solo anula valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales. Los valores flotantes fuera de rango llegan a la radio.
- **Measure only (derivación verdadera)** — Nunca modifica las muestras. Cuenta los excesos solo para telemetría. La conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es `Clip` para que los usuarios existentes no vean cambios de comportamiento.

### Etiquetas de asignación de slices

Las filas RX1–RX8 y TX muestran una etiqueta que indica qué slice impulsa actualmente ese canal. La etiqueta muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando hay un slice activo. Estas etiquetas comparten el mapeo de canales DAX.

### Indicador de estado del servidor

La etiqueta de estado junto a `Enable` muestra el estado del servidor y el número de clientes conectados:

- `(stopped)` — El servidor no está en ejecución.
- `:<puerto> (N clients)` — El servidor está en ejecución en el puerto especificado con N clientes conectados.
- `(port in use)` — El servidor no pudo iniciarse porque otro proceso está vinculado al puerto.

La etiqueta está diseñada con el tema de la aplicación. En versiones anteriores la etiqueta usaba un color fijo; en v26.6.1 el color se deriva del color `background.3` del tema para una apariencia consistente en temas claros y oscuros.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada inicio. El texto del botón muestra `Enabled` en este caso.
- El fallo al salir que afectaba a v0.9.6 y anteriores se corrigió en v0.9.7. La corrección garantiza que el servidor TCI se detenga después de que el hilo de audio se detenga pero mientras el modelo de radio aún está activo, evitando un uso después de liberación.
- A partir de v26.5.2.1, las etiquetas de asignación de slices (estado RX1–RX8 y estado TX) pueden mostrar texto enriquecido. Si una letra de slice contiene caracteres HTML (como un ampersand o corchetes angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado sin procesar.
- A partir de v26.5.1, se admiten tres comandos TCI v2.0 (volume, drive, rx_volume) con sincronización de estado bidireccional.
- A partir de v26.5.3, se exponen el reenvío de espectro del panadapter y tx_gain / ALC.
- El campo Port, la alternancia Enable y el indicador de estado tienen nombres y descripciones accesibles para compatibilidad con lectores de pantalla. El campo Port está etiquetado como "TCI port" y el botón Enable está etiquetado como "TCI server enable".

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Escriba un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente. El botón vuelve a `Disabled` y el estado se vuelve rojo.
- **La aplicación falla al salir** — Confirme que está ejecutando v0.9.7 o posterior. Consulte `Help > About` para ver la cadena de versión. Si la versión es correcta y los fallos persisten, desactive `Enable` antes de salir para aislar si TCI sigue involucrado.
- **`Enable` vuelve a desactivado inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.
- **La etiqueta de asignación de slices muestra HTML sin procesar** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la versión más reciente para garantizar la representación correcta de los identificadores de slices.
- **Las filas RX5–RX8 están ocultas** — La capacidad de slices de la radio es inferior a 8. Las filas por encima del número de slices están ocultas para reflejar las capacidades reales de la radio. Este es un comportamiento esperado; el applet DAX se comporta de la misma manera.

## Relacionado

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Autoiniciar TCI al inicio](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
