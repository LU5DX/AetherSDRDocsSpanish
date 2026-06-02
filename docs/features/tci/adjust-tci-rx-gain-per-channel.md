# Ajuste de ganancia RX de TCI por canal

El applet del Servidor TCI proporciona un control deslizante de ganancia para cada uno de sus cuatro canales RX. Ajustarlos permite igualar el nivel de audio que los clientes TCI (como Log4OM o herramientas SunSDR) reciben de cada slice.

## Antes de comenzar

- El radio debe estar conectado. El applet TCI requiere una conexión activa al radio.
- El applet del Servidor TCI debe estar visible. Si el panel del applet no se muestra, haga clic en el botón **TCI** de la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** para el canal que desea ajustar. La etiqueta de asignación de slice junto al nombre del canal (por ejemplo, `Slice A`) muestra qué slice está conduciendo ese canal. Un `—` indica que actualmente no hay ningún slice asignado.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda o derecha para establecer la ganancia. El valor se guarda de inmediato.
4. Repita para cualquier otro canal RX que desee ajustar.

## Qué hace cada control

| Control                                    | Valor predeterminado                                                                                                     | Rango válido                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medidor/control deslizante de ganancia RX1 | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Medidor/control deslizante de ganancia RX2 | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Medidor/control deslizante de ganancia RX3 | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Medidor/control deslizante de ganancia RX4 | 0.5                                                                                                                      | 0.0 – 1.0                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Ganancia+medidor TX                        | Al arrastrar se establece la ganancia TX de TCI y se emite tciTxGainChanged. Clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la UI refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) provenientes de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (pasante, solo pone a cero NaN/Inf), o Measure (bypass real con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Etiqueta de asignación de slice            | —                                                                                                                        | — o `Slice <letra>`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Modo de desbordamiento TX (clic derecho)   | Clip                                                                                                                     | Clip, NaNGuard, Measure                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Indicador de estado del servidor           | (detenido)                                                                                                               | (detenido), `:<puerto> (N clientes)` o (puerto en uso)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

Cada medidor/control deslizante también muestra un nivel RX o TX en vivo utilizando suavizado exponencial — ataque rápido, decaimiento lento — de modo que la barra refleje la actividad de la señal en ese canal mientras la posición del arrastre establece la ganancia.

Las etiquetas de asignación de slice ahora muestran las letras de los slices con formato de texto enriquecido (#2606). Esto permite que indicadores externos de slice (por ejemplo, un marcador de color o estilo en la letra del slice) se muestren correctamente en la etiqueta de estado. El texto de la etiqueta se genera usando `SliceLabel::richText()` en lugar de una letra sin formato, asegurando que cualquier formato HTML incrustado en la representación del slice se conserve.

## Clic derecho en la ganancia TX para manejo de desbordamiento

El medidor/control deslizante de ganancia TX tiene un menú contextual con clic derecho que permite elegir cómo se manejan las muestras de audio fuera de rango (>1.0) provenientes de clientes TCI antes de que lleguen al radio.

1. Haga clic derecho en cualquier lugar del control deslizante **ganancia+medidor TX**.
2. Seleccione uno de los tres modos de manejo de desbordamiento:
   - **Clip (saturación ±1.0)** — Sujeta firmemente los picos a ±1.0. Este es el valor predeterminado heredado e introduce distorsión armónica en los picos, pero protege la conversión a int16 posterior.
   - **NaN guard (solo poner a cero NaN/Inf)** — Pasa las muestras sin cambios exactos en bits; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad tonal de los modos digitales; los flotantes fuera de rango aún llegan al radio.
   - **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 posterior aún sujeta en la ruta DAX nativa del radio.

El modo seleccionado se conserva como la configuración `TciTxOverflowMode` (valor 0, 1 o 2) y se restaura en el siguiente inicio. El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065).

## Qué hace cada modo de desbordamiento TX

| Modo      | Valor | Comportamiento                                                                                  |
|-----------|-------|-------------------------------------------------------------------------------------------------|
| Clip      | 0     | Satura las muestras en ±1.0. Predeterminado defensivo; introduce armónicos.                      |
| NaNGuard  | 1     | Pasa las muestras sin cambios excepto poner a cero NaN/Inf. Exacto en bits para tonos digitales. |
| Measure   | 2     | Bypass real — nunca modifica las muestras. Cuenta los picos para telemetría.                     |

## Indicador de estado del servidor

El indicador de estado del servidor muestra el estado actual del servidor TCI:

- **(detenido)** — El servidor no está en ejecución.
- **:<puerto> (N clientes)** — El servidor se está ejecutando en el puerto especificado con N clientes conectados.
- **(puerto en uso)** — El puerto seleccionado ya está siendo utilizado por otra aplicación. El texto de estado aparece en rojo.

## Consejos

- Las etiquetas de asignación de slice (por ejemplo, `Slice A`) siguen el mapeo del canal DAX. Si cambia la asignación del canal DAX de un slice, la etiqueta se actualiza automáticamente.
- Los valores de ganancia se conservan como flotantes de dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que se inicie AetherSDR.
- El modo de desbordamiento TX es particularmente útil para modos digitales donde las muestras fuera de rango deben conservarse sin recorte para mantener la fidelidad tonal exacta en bits. Use **NaN guard** para operación en modo digital y **Measure** para telemetría de diagnóstico.

## Solución de problemas

- **Un canal muestra `—` y no pasa audio al cliente TCI** — No hay ningún slice asignado a ese canal DAX. Asigne un slice al canal DAX correspondiente en la configuración de su radio para que el audio RX de TCI se enrute a ese canal.
- **La selección del modo de desbordamiento TX no persiste** — Verifique que AetherSDR tenga permiso de escritura en su archivo de configuración. La configuración `TciTxOverflowMode` se almacena en la configuración de la aplicación.
- **El estado del servidor muestra (puerto en uso)** — El puerto seleccionado está ocupado por otra aplicación. Elija un número de puerto diferente en el campo Port.

## Relacionados

- [Descripción general del Servidor TCI](overview.md)
- [Ajuste de ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
