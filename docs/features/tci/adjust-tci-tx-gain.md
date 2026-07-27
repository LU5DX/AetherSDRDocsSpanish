# Ajustar la ganancia TX de TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares). También configure cómo se manejan las muestras fuera de rango provenientes de clientes de modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de la bandeja **TCI** en la barra lateral derecha para mostrarla.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **TX:**. El indicador de slice a la derecha de la etiqueta muestra qué slice impulsa actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ningún slice TX asignado.
3. Arrastre el control deslizante **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain` y entra en vigor en el servidor en ejecución.

## Elegir el modo de manejo de desbordamiento TX

1. Haga clic derecho en el control deslizante **TX gain+meter** para abrir el menú contextual.
2. Seleccione uno de los siguientes modos:
   - **Clip (saturating ±1.0)** — Limita los picos excesivos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos excesivos pero protege la conversión int16 aguas abajo.
   - **NaN guard (zero NaN/Inf only)** — Pasa las muestras sin cambios; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los valores flotantes fuera de rango llegan a la radio.
   - **Measure only (true bypass)** — Nunca modifica las muestras. Cuenta los picos excesivos para telemetría; la conversión int16 aguas abajo aún limita en la ruta DAX nativa de la radio.
3. La selección se guarda inmediatamente en `TciTxOverflowMode` y entra en vigor en el servidor en ejecución.

## Qué hace cada control

| Control                        | Valor predeterminado                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX gain+meter                  | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. Clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite a los usuarios elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo pone a cero NaN/Inf) o Measure (bypass verdadero con conteo de clips). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| TX overflow mode (clic derecho) | Clip (0)                                                                                                                 | Clip (0), NaNGuard (1), Measure (2)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

El **TX gain+meter** es un medidor y un control deslizante combinados. La parte del medidor refleja el nivel de audio TX en vivo del slice TX activo. La posición del control deslizante establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

El control deslizante **TX gain+meter** tiene un nombre accesible "TCI TX gain" establecido en v26.6.3, lo que mejora la compatibilidad con lectores de pantalla.

La etiqueta del slice junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Muestra qué slice está asignado actualmente como slice TX y se actualiza automáticamente cuando cambia el slice TX. A partir de v26.5.2.1, la etiqueta del slice usa formato de texto enriquecido para que las letras del slice renderizadas como HTML se muestren correctamente (#2606).

## Indicador de estado del servidor

El applet del Servidor TCI muestra una etiqueta de estado junto al botón Enable. Esta etiqueta muestra uno de los tres estados:

| Estado                         | Significado                                                                                     |
|--------------------------------|-------------------------------------------------------------------------------------------------|
| `(stopped)`                    | El servidor no se está ejecutando. La etiqueta usa el color del tema `{{color.background.3}}` para el texto. |
| `:<port> (N clients)`          | El servidor se está ejecutando en el puerto especificado con el número de clientes conectados.   |
| `(port in use)`                | El servidor no pudo iniciar porque el puerto ya está en uso. La etiqueta se vuelve roja.         |

En v26.6.1, el estilo de la etiqueta de estado se actualizó para usar el color del tema `{{color.background.3}}` en lugar de un color fijo, lo que garantiza una apariencia adecuada con todos los temas de AetherSDR.

## Comportamiento del botón Enable/Disable

El botón **Enable** activa o desactiva el servidor TCI. En v26.7.4, el texto del botón cambia dinámicamente:

- **Disabled** (estado apagado) — El servidor TCI está detenido. La etiqueta usa el texto "Disabled" cuando no está marcado.
- **Enabled** (estado encendido) — El servidor TCI se está ejecutando. La etiqueta usa el texto "Enabled" cuando está marcado.

El botón comienza en el estado determinado por `AutoStartTCI`. Si `AutoStartTCI` está establecido en `True`, el botón se inicializa marcado con el texto "Enabled". Si `AutoStartTCI` es `False` (el valor predeterminado), el botón se inicializa sin marcar con el texto "Disabled".

Al hacer clic, el botón cambia de estado y su texto se actualiza inmediatamente para reflejar el nuevo estado. Si el servidor no puede iniciarse (por ejemplo, porque el puerto está en uso), el botón vuelve al estado no marcado y muestra "Disabled" con la etiqueta de estado mostrando "(port in use)" en rojo.

El botón Enable tiene un nombre accesible "TCI server enable" y una descripción accesible "Start or stop the TCI server" (v26.7.4).

## Consejos

- Si no aparece ninguna etiqueta de slice junto a **TX:** (muestra `—`), no hay ningún slice TX asignado. Asigne un slice TX en la radio antes de ajustar la ganancia TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y coloca el control deslizante en el valor almacenado.
- Utilice **NaN guard** o **Measure only** cuando ejecute modos digitales que requieran fidelidad tonal bit a bit. El modo **Clip** puede introducir distorsión armónica en los picos excesivos.
- El modo **Measure only** es un bypass verdadero y solo cuenta los picos excesivos para telemetría sin modificar el flujo de audio.
- El texto del botón Enable ("Enabled"/"Disabled") proporciona una retroalimentación visual clara sobre el estado del servidor, complementando la etiqueta de estado.

## Relacionados

- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [TCI Server overview](overview.md)
