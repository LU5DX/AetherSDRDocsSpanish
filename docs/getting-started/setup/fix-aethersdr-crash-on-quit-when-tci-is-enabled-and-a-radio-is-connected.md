# Servidor TCI (Applet TCI)

AetherSDR puede ejecutar un servidor WebSocket TCI estilo Expert para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) pueda leer y controlar la radio mediante el protocolo TCI. El audio TX de TCI se recibe a través del WebSocket y se envía a una ranura de flujo dax_tx dedicada que es independiente de la ruta del dispositivo de audio DAX2 de Windows SmartSDR, por lo que el TX de TCI funciona en todas las plataformas, incluyendo Windows y Linux, sin PipeWire.

## Antes de comenzar

- Una radio FLEX-8600 está conectada y visible en la aplicación.
- El applet TCI es visible. Si no lo está, haga clic en el botón de la bandeja `TCI` en la barra lateral derecha para mostrarlo.

## Pasos

1. Abra el applet TCI haciendo clic en el botón de la bandeja `TCI` en la barra lateral derecha si aún no está visible.
2. En el campo `Port`, introduzca un valor de puerto entre 1024 y 65535. El valor predeterminado es `50001`. Si el campo está vacío o fuera de rango, escriba `50001` y presione Enter; el campo se ajusta automáticamente a `50001` para valores fuera de rango.
3. Haga clic en `Enable` para iniciar el servidor TCI.
4. Confirme que el indicador de estado junto a `Enable` muestra `:<puerto> (0 clients)` en lugar de `(port in use)`. Si muestra `(port in use)`, consulte la sección de Solución de problemas más abajo.
5. Configure su software de terceros para conectarse al servidor TCI en `localhost:<puerto>`.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---------|---------|-------------|-------------|----------|
| Campo `Port` | `50001` | 1024–65535 | `TciPort` | Cambiar el puerto reinicia el servidor si está habilitado. Los valores fuera de rango se ajustan a 50001. |
| Interruptor `Enable` | Apagado | Encendido / Apagado | Ninguno | Inicia o detiene el servidor TCI; emite `tciToggled`. Si falla la vinculación, el interruptor vuelve a apagado y el estado muestra `(port in use)`. |
| Ganancia+medidor RX1 | 0.5 | 0.0–1.0 | `TciRxGain1` | Medidor/deslizador combinado; al arrastrar se establece la ganancia RX de TCI para el canal y emite `tciRxGainChanged`. |
| Ganancia+medidor RX2 | 0.5 | 0.0–1.0 | `TciRxGain2` | Medidor/deslizador combinado; al arrastrar se establece la ganancia RX de TCI para el canal y emite `tciRxGainChanged`. |
| Ganancia+medidor RX3 | 0.5 | 0.0–1.0 | `TciRxGain3` | Medidor/deslizador combinado; al arrastrar se establece la ganancia RX de TCI para el canal y emite `tciRxGainChanged`. |
| Ganancia+medidor RX4 | 0.5 | 0.0–1.0 | `TciRxGain4` | Medidor/deslizador combinado; al arrastrar se establece la ganancia RX de TCI para el canal y emite `tciRxGainChanged`. |
| Ganancia+medidor TX | 0.5 | 0.0–1.0 | `TciTxGain` | Al arrastrar se establece la ganancia TX de TCI y emite `tciTxGainChanged`. Clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). |
| Modo de desbordamiento TX (clic derecho) | Clip (0) | Clip (0), NaNGuard (1), Measure (2) | `TciTxOverflowMode` | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. |

### Detalles de ganancia+medidor RX

Cada canal RX (1–4) tiene un medidor y un deslizador combinados. Arrastre el deslizador para establecer la ganancia RX de TCI para ese canal. El valor de ganancia se conserva por separado para cada canal como `TciRxGain1` a `TciRxGain4`. Cada deslizador tiene un nombre accesible ("ganancia TCI RX 1", "ganancia TCI RX 2", etc.) para compatibilidad con lectores de pantalla.

### Detalles de ganancia+medidor TX

Al arrastrar se establece la ganancia TX de TCI y emite `tciTxGainChanged`. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado.

Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el menú contextual del modo de desbordamiento TX. Esto le permite elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:

- **Clip (saturado ±1.0)** — Limita bruscamente los excesos a ±1.0. Este es el valor predeterminado heredado; protege la conversión int16 aguas abajo pero introduce armónicos en los excesos.
- **NaN guard (solo cero NaN/Inf)** — Pasa las muestras bit exacto; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad del tono del modo digital. Los valores flotantes fuera de rango llegan a la radio.
- **Measure only (bypass verdadero)** — Nunca muta las muestras. Cuenta los excesos solo para telemetría. La conversión int16 aguas abajo aún limita en la ruta DAX nativa de la radio.

El modo seleccionado se conserva como `TciTxOverflowMode` (0/1/2). El valor predeterminado es `Clip` para que los usuarios existentes no vean ningún cambio de comportamiento.

### Etiquetas de asignación de slice

Las filas RX1–RX4 y TX muestran una etiqueta que indica qué slice está manejando actualmente ese canal. La etiqueta muestra `—` cuando no hay ningún slice asignado, o `Slice <letra>` cuando un slice está activo. Estas etiquetas comparten la asignación del canal DAX.

### Indicador de estado del servidor

La etiqueta de estado junto a `Enable` muestra el estado del servidor y el número de clientes conectados:

- `(stopped)` — El servidor no está en ejecución.
- `:<puerto> (N clients)` — El servidor se está ejecutando en el puerto especificado con N clientes conectados.
- `(port in use)` — El servidor no pudo iniciarse porque otro proceso está vinculado al puerto.

La etiqueta se estiliza usando el tema de la aplicación. En versiones anteriores, la etiqueta usaba un color fijo; en v26.6.1, el color se deriva del color `background.3` del tema para una apariencia consistente en temas claros y oscuros.

## Consejos

- Si usa `Settings > Autostart TCI with AetherSDR`, el servidor TCI se inicia automáticamente en cada lanzamiento.
- El fallo al salir que afectaba a v0.9.6 y anteriores se corrigió en v0.9.7. La corrección asegura que el servidor TCI se destruya después de que el hilo de audio se detenga pero mientras el modelo de radio aún esté activo, evitando un uso después de liberación.
- A partir de v26.5.2.1, las etiquetas de asignación de slice (estado RX1–RX4 y estado TX) pueden renderizar texto enriquecido. Si una letra de slice contiene caracteres HTML (como un ampersand o paréntesis angulares), la etiqueta se muestra correctamente en lugar de mostrar marcado sin procesar.
- A partir de v26.5.1, se admiten tres comandos TCI v2.0 (volume, drive, rx_volume) con sincronización de estado bidireccional.
- A partir de v26.5.3, se exponen el reenvío de espectro del panadapter y tx_gain / ALC.

## Solución de problemas

- **El estado muestra `(port in use)` después de hacer clic en `Enable`** — Otro proceso ya está vinculado a ese puerto. Introduzca un número de puerto diferente en el campo `Port` y presione Enter, luego haga clic en `Enable` nuevamente.
- **La aplicación falla al salir** — Confirme que está ejecutando v0.9.7 o posterior. Verifique `Help > About` para la cadena de versión. Si la versión es correcta y los fallos persisten, deshabilite `Enable` antes de salir para aislar si TCI sigue involucrado.
- **`Enable` se apaga inmediatamente** — La vinculación del puerto falló. La etiqueta de estado se vuelve roja y muestra `(port in use)`. Cambie el valor del puerto e intente de nuevo.
- **La etiqueta de asignación de slice muestra HTML sin procesar** — Esto indica que está ejecutando una versión anterior a v26.5.2.1. Actualice a la última versión para asegurar el renderizado correcto de los identificadores de slice.

## Relacionado

- [Visión general del servidor TCI](../../features/tci/overview.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](../../features/tci/enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al lanzar](../../features/tci/autostart-tci-on-launch.md)
- [Cambiar el puerto TCI](../../features/tci/change-the-tci-port.md)
- [Ver cuántos clientes TCI están conectados](see-how-many-tci-clients-are-connected.md)
