# Applet del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket TCI estilo Expert para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar la radio mediante el protocolo TCI. El audio de TX por TCI se recibe a través del WebSocket y se introduce en una ranura dedicada de flujo dax_tx que es independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows, por lo que la TX por TCI funciona en todas las plataformas, incluidas Windows y Linux, sin PipeWire (v0.9.5.1, #2276).

En la v0.9.7 se corrigió un cierre con bloqueo: TciServer ahora se cierra explícitamente en `~MainWindow()` después de que el hilo de audio se detiene, pero mientras RadioModel sigue activo, lo que evita un uso después de liberación mediante `releaseDaxForTci()`. Se añadió un `QPointer<RadioModel>` como refuerzo adicional para que las comprobaciones de nulidad existentes detecten automáticamente cualquier regresión futura.

En la v26.5.1 se añadieron tres comandos TCI v2.0 (volume, drive, rx_volume) a la tabla de despacho con sincronización de estado bidireccional (#1764, #2463). En la v26.5.3 se exponen el reenvío del espectro del panadapter (#2841) y tx_gain / ALC (#2950); haga clic derecho en el control deslizante de TX para elegir el manejo de desbordamiento de TX (Clip / NaNGuard / Measure) para una fidelidad de tono bit-exacta en modos digitales (#3065).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para revelarla.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.

## Función de cada control

| Control                          | Valor predeterminado                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Clave de ajuste             |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------|
| Ganancia+medidor RX1..RX8        | 0.5                                                                                                                      | 0.0–1.0 (un control deslizante por canal)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | `TciRxGain1`..`TciRxGain8` |
| Ganancia+medidor TX              | Los arrastres establecen la ganancia de TX por TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio de TX por TCI siempre se permite independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, valor predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf), o Measure (derivación real con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). | `TciTxGain`                 |
| Modo de desbordamiento de TX (clic derecho) | Clip (0)                                                                                                                 | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `TciTxOverflowMode`         |
| Puerto                          | 50001                                                                                                                    | 1024–65535 (los valores fuera de rango se ajustan a 50001)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `TciPort`                   |
| Habilitar                        | desactivado                                                                                                              | —                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | —                           |

### Controles deslizantes de ganancia+medidor RX (RX1..RX8)

Cada fila de RX tiene un medidor y un control deslizante combinados para los canales RX1 a RX8. La porción del medidor refleja el nivel de audio de recepción en vivo de la rebanada asignada. La posición del control deslizante establece la ganancia de RX por TCI para el canal y emite `tciRxGainChanged` al arrastrarlo. Cada canal tiene su propia clave de ajuste (`TciRxGain1` hasta `TciRxGain8`); el valor predeterminado para cada uno es 0.5 con un rango válido de 0.0–1.0.

El número de filas de RX visibles coincide con la capacidad de rebanadas de la radio (hasta 8 en una FLEX-6700). Las filas por encima del número máximo de rebanadas de la radio se ocultan automáticamente. En radios con menos rebanadas (por ejemplo, una FLEX-6600 con 4 rebanadas), solo se muestran las filas de RX correspondientes.

### Control deslizante de ganancia+medidor TX

El **control deslizante de ganancia+medidor TX** es un medidor y control deslizante combinados. La porción del medidor refleja el nivel de audio de TX en vivo de la rebanada de TX activa. La posición del control deslizante establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

El control deslizante **ganancia+medidor TX** tiene un nombre accesible "TCI TX gain" establecido en la v26.6.3, lo que mejora la compatibilidad con lectores de pantalla.

#### Ajustar la ganancia de TX

1. Localice la fila **TX:**. El indicador de rebanada a la derecha de la etiqueta muestra qué rebanada impulsa actualmente el canal de TX (por ejemplo, `Slice A`), o `—` si no se ha asignado ninguna rebanada de TX.
2. Arrastre el control deslizante **ganancia+medidor TX** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es `0.0` a `1.0`; el valor predeterminado es `0.5`.
3. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain` y surte efecto en el servidor en ejecución.

#### Elegir el modo de manejo de desbordamiento de TX

1. Haga clic derecho en el control deslizante **ganancia+medidor TX** para abrir el menú contextual.
2. Seleccione uno de los siguientes modos:
   - **Clip (saturación ±1.0)** — Limita bruscamente los excesos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los excesos pero protege la conversión a int16 posterior.
   - **Protección NaN (solo pone a cero NaN/Inf)** — Pasa las muestras bit-exactas; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad de tono de los modos digitales; los flotantes fuera de rango llegan a la radio.
   - **Solo medición (derivación real)** — Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión a int16 posterior aún limita en la ruta DAX nativa de la radio.
3. La selección se guarda inmediatamente en `TciTxOverflowMode` y surte efecto en el servidor en ejecución.

### Campo de puerto

El campo **Puerto** establece el puerto TCP en el que escucha el servidor TCI. El valor predeterminado es 50001. Los valores válidos son 1024–65535; los valores fuera de rango vuelven a 50001. Cambiar el puerto reinicia el servidor si está habilitado actualmente.

### Botón Habilitar

El botón **Habilitar** activa o desactiva el servidor TCI. Al hacer clic se inicia o detiene el servidor y se emite `tciToggled`. Si el servidor no puede vincularse al puerto configurado, el botón vuelve a la posición de desactivado y el estado muestra "(puerto en uso)".

En la v26.7.4, el texto del botón cambia dinámicamente:

- **Disabled** (estado desactivado) — El servidor TCI está detenido. La etiqueta usa el texto "Disabled" cuando no está marcado.
- **Enabled** (estado activado) — El servidor TCI está en ejecución. La etiqueta usa el texto "Enabled" cuando está marcado.

El botón se inicia en el estado determinado por `AutoStartTCI`. Si `AutoStartTCI` está establecido en `True`, el botón se inicializa marcado con el texto "Enabled". Si `AutoStartTCI` es `False` (el valor predeterminado), el botón se inicializa sin marcar con el texto "Disabled".

Al hacer clic, el botón cambia de estado y su texto se actualiza inmediatamente para reflejar el nuevo estado. Si el servidor no puede iniciarse (por ejemplo, porque el puerto está en uso), el botón vuelve al estado sin marcar y muestra "Disabled" con la etiqueta de estado mostrando "(puerto en uso)" en rojo.

El botón Habilitar tiene un nombre accesible "TCI server enable" y una descripción accesible "Start or stop the TCI server" (v26.7.4).

### Etiquetas de asignación de rebanadas

Las filas de RX y la fila de TX muestran cada una una etiqueta de asignación de rebanada de solo lectura a la derecha del control. Esta etiqueta muestra qué rebanada impulsa actualmente ese canal (por ejemplo, `Slice A`) o `—` si no se ha asignado ninguna rebanada. Las etiquetas comparten la misma asignación de rebanada a canal DAX que el applet DAX y se actualizan automáticamente cuando cambian las asignaciones de rebanadas.

El índice del receptor TCI (trx) no está limitado a 4: trx es un índice posicional de rebanada acotado por `slices.size()` (hasta 8 en una FLEX-6700), por lo que los canales DAX 5–8 tienen representación TCI.

## Indicador de estado del servidor

El applet del servidor TCI muestra una etiqueta de estado junto al botón Habilitar. Esta etiqueta muestra uno de tres estados:

| Estado                        | Significado                                                                                   |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| `(stopped)`                   | El servidor no está en ejecución. La etiqueta usa el color de tema `{{color.background.3}}` para el texto. |
| `:<puerto> (N clientes)`      | El servidor está en ejecución en el puerto especificado con el número indicado de clientes conectados. |
| `(puerto en uso)`             | El servidor no pudo iniciarse porque el puerto ya está en uso. La etiqueta se vuelve roja.     |

En la v26.6.1, el estilo de la etiqueta de estado se actualizó para usar el color de tema `{{color.background.3}}` en lugar de un color fijo, lo que garantiza una apariencia adecuada con todos los temas de AetherSDR.

## Consejos

- Si no aparece ninguna etiqueta de rebanada junto a **TX:** (muestra `—`), no se ha asignado ninguna rebanada de TX. Asigne una rebanada de TX en la radio antes de ajustar la ganancia de TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y establece el control deslizante al valor almacenado.
- Use **NaN guard** o **Measure only** al ejecutar modos digitales que requieran fidelidad de tono bit-exacta. El modo **Clip** puede introducir distorsión armónica en los excesos.
- El modo **Measure only** es una derivación real y solo cuenta los excesos para telemetría sin modificar el flujo de audio.
- El texto del botón Habilitar ("Enabled"/"Disabled") proporciona retroalimentación visual clara sobre el estado del servidor, complementando la etiqueta de estado.

## Relacionados

- [Ajustar la ganancia de RX por TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del servidor TCI](overview.md)
