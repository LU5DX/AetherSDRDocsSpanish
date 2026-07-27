# Servidor TCI (Applet TCI)

AetherSDR puede ejecutar un servidor WebSocket TCI de estilo Expert para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar la radio a través del protocolo TCI. El audio de TX de TCI se recibe a través del WebSocket y se introduce en una ranura de flujo dax_tx dedicada, independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows, por lo que la TX de TCI funciona en todas las plataformas, incluyendo Windows y Linux, sin PipeWire.

## Antes de comenzar

- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI está visible. Si no lo está, haga clic en el botón de la bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1.  Abra el applet TCI haciendo clic en el botón de la bandeja `TCI` en la barra lateral derecha si aún no está visible.
2.  En el campo `Port`, introduzca un valor de puerto entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está en blanco o fuera de rango, escriba `50001` y presione Enter; el campo se ajusta automáticamente a `50001` para valores fuera de rango.
3.  Haga clic en `Enable` para iniciar el servidor TCI. El texto del botón cambia a `Enabled` cuando el servidor está en ejecución. Si `Settings > Autostart TCI with AetherSDR` estaba habilitado, el botón comienza como `Enabled` y el servidor se inicia automáticamente.
4.  Confirme que el indicador de estado junto a `Enable` muestre `:<puerto> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte la sección de Solución de problemas a continuación.
5.  Configure su software de terceros para conectarse al servidor TCI en `localhost:<puerto>`.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                         | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo `Port`                   | `50001`                                                                                                                      | 1024–65535                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Alternador `Enable`            | Apagado (o Encendido si el inicio automático está configurado)                                                                | Encendido / Apagado. El texto del botón muestra `Enabled` o `Disabled`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor RX1           | 0.5                                                                                                                          | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX2           | 0.5                                                                                                                          | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX3           | 0.5                                                                                                                          | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor RX4           | 0.5                                                                                                                          | 0.0–1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Ganancia+medidor TX            | Arrastrar establece la ganancia de TX de TCI y emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio de TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital: Clip (saturación ±1.0, valor predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf), o Measure (bypass real con recuento de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento TX (clic derecho) | Clip (0)                                                                                                                     | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### Detalles del alternador Enable

El botón `Enable` es un alternador que inicia o detiene el servidor TCI. El texto del botón cambia a `Enabled` cuando el servidor está en ejecución y a `Disabled` cuando está detenido. Si `Settings > Autostart TCI with AetherSDR` está habilitado, el botón se inicializa como `Enabled` y el servidor se inicia automáticamente al lanzar la aplicación. Si falla la vinculación del puerto, el botón vuelve a `Disabled` y el estado muestra `(port in use)` en rojo.

### Detalles de ganancia+medidor RX

Cada canal RX (1–4) tiene un medidor y un deslizador combinados. Arrastre el deslizador para establecer la ganancia de RX de TCI para ese canal. El valor de ganancia se persiste por separado para cada canal como `TciRxGain1` a `TciRxGain4`. Cada deslizador tiene un nombre accesible ("TCI RX 1 gain", "TCI RX 2 gain", etc.) para compatibilidad con lectores de pantalla.

### Detalles de ganancia+medidor TX

Arrastrar establece la ganancia de TX de TCI y emite `tciTxGainChanged`. El audio de TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado.

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú contextual del modo de desbordamiento de TX. Esto le permite elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:

- **Clip (saturación ±1.0)** — Limita forzosamente los picos a ±1.0. Este es el valor predeterminado heredado; protege la conversión descendente a int16 pero introduce armónicos en los picos.
- **NaN guard (solo pone a cero NaN/Inf)** — Pasa las muestras sin cambios, bit a bit; solo pone a cero los valores NaN/Inf patológicos. Preserva la fidelidad del tono del modo digital. Los valores de punto flotante fuera de rango llegan a la radio.
- **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los picos solo para telemetría. La conversión descendente a int16 aún limita en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es `Clip` para que los usuarios existentes no vean cambios de comportamiento.

### Etiquetas de asignación de slices

Las filas RX1–RX4 y TX muestran una etiqueta que indica qué slice está manejando actualmente ese canal. La etiqueta muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando hay un slice activo. Estas etiquetas comparten la asignación del canal DAX.

### Indicador de estado del servidor

La etiqueta de estado junto a `Enable` muestra el estado del servidor y el número de clientes conectados:

- `(stopped)` — El servidor no está en ejecución.
- `:<puerto> (N clients)` — El servidor se está ejecutando en el puerto especificado con N clientes conectados.
- `(port in use)` — El servidor no pudo iniciarse porque otro proceso está vinculado al puerto.

La etiqueta tiene el estilo del tema de la aplicación. En versiones anteriores, la etiqueta usaba un color fijo; en v26.6.1, el color se deriva del color `background.3` del tema para una apariencia consistente en temas claros y oscuros.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada lanzamiento. El texto del botón muestra `Enabled` en este caso.
- El bloqueo al salir que afectaba a v0.9.6 y anteriores se solucionó en v0.9.7. La corrección asegura que el servidor TCI se detenga después de que el hilo de audio se detenga pero mientras el modelo de radio aún está activo, evitando un uso después de liberación (use-after-free).
- A partir de v26.5.2.1, las etiquetas de asignación de slices (estado RX1–RX4 y estado TX) pueden mostrar texto enriquecido. Si una letra de slice contiene caracteres HTML (como un ampersand o paréntesis angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado sin procesar.
- A partir de v26.5.1, se admiten tres comandos TCI v2.0 (volume, drive, rx_volume) con sincronización de estado bidireccional.
- A partir de v26.5.3, se exponen el reenvío de espectro del panadaptador y tx_gain / ALC.
- El campo Port, el alternador Enable y el indicador de estado tienen nombres y descripciones accesibles para compatibilidad con lectores de pantalla. El campo Port está etiquetado como "TCI port" y el botón Enable está etiquetado como "TCI server enable".

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Introduzca un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente. El botón vuelve a `Disabled` y el estado se vuelve rojo.
- **La aplicación se bloquea al salir** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para la cadena de versión. Si la versión es correcta y los bloqueos persisten, deshabilite `Enable` antes de salir para aislar si TCI sigue siendo el causante.
- **`Enable` vuelve a apagado inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente nuevamente.
- **La etiqueta de asignación de slice muestra HTML sin procesar** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la última versión para asegurar una representación correcta de los identificadores de slice.

## Relacionados

- [Descripción general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
