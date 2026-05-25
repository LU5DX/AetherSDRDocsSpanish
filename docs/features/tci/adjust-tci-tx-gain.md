# Ajustar la ganancia de TX del TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares). También configure cómo se manejan las muestras fuera de rango de los clientes de modo digital.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para revelarla.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Localice la fila **TX:**. El indicador de segmento a la derecha de la etiqueta muestra qué segmento impulsa actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ningún segmento TX asignado.
3. Arrastre el deslizador **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el deslizador. El nuevo valor se guarda inmediatamente en `TciTxGain` y entra en vigencia en el servidor en ejecución.

## Elegir el modo de manejo de desbordamiento de TX

1. Haga clic derecho en el deslizador **TX gain+meter** para abrir el menú contextual.
2. Seleccione uno de los siguientes modos:
   - **Clip (saturating ±1.0)** — Recorta forzosamente los picos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos pero protege la conversión descendente a int16.
   - **NaN guard (zero NaN/Inf only)** — Pasa las muestras sin cambios; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los valores flotantes fuera de rango llegan a la radio.
   - **Measure only (true bypass)** — Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión descendente a int16 aún recorta en la ruta DAX nativa de la radio.
3. La selección se guarda inmediatamente en `TciTxOverflowMode` y entra en vigencia en el servidor en ejecución.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Comportamiento | Notas |
|---------|----------------|--------------|----------------|-------|
| TX gain+meter | 0.5 | 0.0–1.0 | Arrastrar establece la ganancia TX del TCI y emite tciTxGainChanged. Clic derecho abre el selector de modo de desbordamiento de TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX del TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado. |
| Modo de desbordamiento de TX (clic derecho) | Clip (0) | Clip (0), NaNGuard (1), Measure (2) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento de TX. Emite tciTxOverflowModeChanged. | Nuevo en v26.5.3. Clip recorta los picos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales exactos solo poniendo a cero NaN/Inf; Measure cuenta los picos para telemetría sin modificación. Se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |

El **TX gain+meter** es un medidor y deslizador combinados. La parte del medidor refleja el nivel de audio TX en vivo del segmento TX activo. La posición del deslizador establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

La etiqueta de segmento junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Muestra qué segmento está asignado actualmente como segmento TX y se actualiza automáticamente cuando cambia el segmento TX. A partir de v26.5.2.1, la etiqueta de segmento usa formato de texto enriquecido para que las letras de segmento renderizadas como HTML se muestren correctamente (#2606).

## Consejos

- Si no aparece ninguna etiqueta de segmento junto a **TX:** (muestra `—`), no hay ningún segmento TX asignado. Asigne un segmento TX en la radio antes de ajustar la ganancia de TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y establece el deslizador al valor almacenado.
- Utilice **NaN guard** o **Measure only** cuando ejecute modos digitales que requieran fidelidad tonal exacta. El modo **Clip** puede introducir distorsión armónica en los picos.
- El modo **Measure only** es un bypass real y solo cuenta los picos para telemetría sin modificar el flujo de audio.

## Relacionados

- [Ajustar la ganancia de RX del TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del servidor TCI](overview.md)
