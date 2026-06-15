# Ajustar la ganancia de TX del TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares). También configure cómo se manejan las muestras fuera de rango provenientes de clientes de modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- El servidor TCI debe estar visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para mostrarla.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Localice la fila **TX:**. El indicador de slice a la derecha de la etiqueta muestra qué slice impulsa actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ningún slice TX asignado.
3. Arrastre el deslizador **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el deslizador. El nuevo valor se guarda inmediatamente en `TciTxGain` y se aplica en el servidor en ejecución.

## Elegir el modo de manejo de desbordamiento de TX

1. Haga clic derecho en el deslizador **TX gain+meter** para abrir el menú contextual.
2. Seleccione uno de los siguientes modos:
   - **Clip (saturating ±1.0)** — Recorta forzosamente los excesos a ±1.0. Valor defensivo predeterminado; introduce armónicos en los excesos pero protege la conversión downstream a int16.
   - **NaN guard (zero NaN/Inf only)** — Pasa las muestras sin cambios; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los flotantes fuera de rango llegan a la radio.
   - **Measure only (true bypass)** — Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión downstream a int16 aún recorta en la ruta DAX nativa de la radio.
3. La selección se guarda inmediatamente en `TciTxOverflowMode` y se aplica en el servidor en ejecución.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX gain+meter                  | Los arrastres establecen la ganancia TX del TCI y emiten tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure).                                                                                                                                                                                                                                                                                                                                                                                                         | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX del TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, valor predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf) o Measure (bypass verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento de TX (clic derecho) | Clip (0)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

El control **TX gain+meter** es un medidor y deslizador combinados. La parte del medidor refleja el nivel de audio TX en vivo del slice TX activo. La posición del deslizador establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

El deslizador **TX gain+meter** tiene un nombre accesible "TCI TX gain" establecido en v26.6.3, lo que mejora la compatibilidad con lectores de pantalla.

La etiqueta de slice junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Indica qué slice está asignado actualmente como slice TX y se actualiza automáticamente cuando cambia el slice TX. A partir de la v26.5.2.1, la etiqueta de slice usa formato de texto enriquecido para que las letras de slice renderizadas como HTML se muestren correctamente (#2606).

## Indicador de estado del servidor

El applet del servidor TCI muestra una etiqueta de estado junto al botón Enable. Esta etiqueta muestra uno de tres estados:

| Estado                         | Significado                                                                                   |
|-------------------------------|----------------------------------------------------------------------------------------------|
| `(stopped)`                   | El servidor no se está ejecutando. La etiqueta usa el color del tema `{{color.background.3}}` para el texto. |
| `:<puerto> (N clients)`      | El servidor se está ejecutando en el puerto especificado con el número indicado de clientes conectados. |
| `(port in use)`               | El servidor no pudo iniciarse porque el puerto ya está en uso. La etiqueta se vuelve roja.   |

En la v26.6.1, el estilo de la etiqueta de estado se actualizó para usar el color del tema `{{color.background.3}}` en lugar de un color fijo, lo que garantiza una apariencia adecuada con todos los temas de AetherSDR.

## Consejos

- Si no aparece ninguna etiqueta de slice junto a **TX:** (muestra `—`), no hay ningún slice TX asignado. Asigne un slice TX en la radio antes de ajustar la ganancia de TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y coloca el deslizador en el valor almacenado.
- Use **NaN guard** o **Measure only** cuando ejecute modos digitales que requieran fidelidad tonal bit a bit. El modo **Clip** puede introducir distorsión armónica en los excesos.
- El modo **Measure only** es un bypass verdadero y solo cuenta los excesos para telemetría sin modificar el flujo de audio.

## Relacionados

- [Ajustar la ganancia de RX del TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Visión general del servidor TCI](overview.md)
