# Ajustar la ganancia de transmisión TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares). También configure cómo se manejan las muestras fuera de rango provenientes de clientes de modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- El servidor TCI debe estar visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **TX:**. El indicador de segmento a la derecha de la etiqueta muestra qué segmento impulsa actualmente el canal de TX (por ejemplo, `Slice A`), o `—` si no hay ningún segmento de TX asignado.
3. Arrastre el control deslizante **Ganancia TX+medidor** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain` y se aplica en el servidor en ejecución.

## Elegir el modo de manejo de desbordamiento de TX

1. Haga clic derecho en el control deslizante **Ganancia TX+medidor** para abrir el menú contextual.
2. Seleccione uno de los siguientes modos:
   - **Clip (saturación ±1.0)** — Recorta forzosamente los picos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos pero protege la conversión posterior a int16.
   - **NaN guard (solo cero para NaN/Inf)** — Pasa las muestras sin cambios; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los valores flotantes fuera de rango llegan a la radio.
   - **Measure only (bypass verdadero)** — Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio.
3. La selección se guarda inmediatamente en `TciTxOverflowMode` y se aplica en el servidor en ejecución.

## Qué hace cada control

| Control                             | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ganancia TX+medidor                 | Arrastrar establece la ganancia TX de TCI y emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure).                                                                                                                                                                                                                                                                                                                                                                                                                | TciServer::setTxGain persiste TciTxGain internamente; la UI refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf) o Measure (bypass verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Modo de desbordamiento de TX (clic derecho) | Clip (0)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

La **Ganancia TX+medidor** es un medidor y control deslizante combinados. La parte del medidor refleja el nivel de audio TX en vivo del segmento de TX activo. La posición del control deslizante establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

La etiqueta de segmento junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Muestra qué segmento está asignado actualmente como segmento de TX y se actualiza automáticamente cuando cambia el segmento de TX. A partir de la v26.5.2.1, la etiqueta de segmento utiliza formato de texto enriquecido para que las letras de segmento representadas como HTML se muestren correctamente (#2606).

## Indicador de estado del servidor

El applet del Servidor TCI muestra una etiqueta de estado junto al botón Habilitar. Esta etiqueta muestra uno de tres estados:

| Estado                         | Significado                                                                                               |
|-------------------------------|-----------------------------------------------------------------------------------------------------------|
| `(detenido)`                   | El servidor no está en ejecución. La etiqueta utiliza el color del tema `{{color.background.3}}` para el texto. |
| `:<puerto> (N clientes)`       | El servidor se está ejecutando en el puerto especificado con el número indicado de clientes conectados.   |
| `(puerto en uso)`              | El servidor no pudo iniciarse porque el puerto ya está en uso. La etiqueta se vuelve roja.                |

En la v26.6.1, el estilo de la etiqueta de estado se actualizó para usar el color del tema `{{color.background.3}}` en lugar de un color fijo, lo que garantiza una apariencia adecuada con todos los temas de AetherSDR.

## Consejos

- Si no aparece ninguna etiqueta de segmento junto a **TX:** (muestra `—`), no hay ningún segmento de TX asignado. Asigne un segmento de TX en la radio antes de ajustar la ganancia de TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y establece el control deslizante al valor almacenado.
- Use **NaN guard** o **Measure only** cuando ejecute modos digitales que requieran fidelidad tonal bit exacta. El modo **Clip** puede introducir distorsión armónica en los picos.
- El modo **Measure only** es un bypass verdadero y solo cuenta los picos para telemetría sin modificar el flujo de audio.

## Relacionados

- [Ajustar la ganancia de recepción TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Visión general del Servidor TCI](overview.md)
