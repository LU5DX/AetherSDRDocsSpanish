# Ajustar la ganancia RX de TCI por canal

El applet del Servidor TCI proporciona un control deslizante de ganancia para cada uno de sus cuatro canales RX. Ajustarlos permite igualar el nivel de audio que los clientes TCI (como Log4OM o herramientas SunSDR) reciben de cada slice.

## Antes de comenzar

- La radio debe estar conectada. El applet TCI requiere una conexión de radio activa.
- El applet del Servidor TCI debe estar visible. Si el panel del applet no se muestra, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** del canal que desea ajustar. La etiqueta de asignación de slice junto al nombre del canal (por ejemplo, `Slice A`) muestra qué slice está manejando ese canal. Un `—` significa que no hay ningún slice asignado actualmente.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda o derecha para establecer la ganancia. El valor se guarda inmediatamente.
4. Repita para cualquier otro canal RX que desee ajustar.

## Qué hace cada control

| Control                        | Predeterminado | Rango válido |
|--------------------------------|----------------|--------------|
| Medidor/control deslizante de ganancia RX1 | 0.5            | 0.0 – 1.0    |
| Medidor/control deslizante de ganancia RX2 | 0.5            | 0.0 – 1.0    |
| Medidor/control deslizante de ganancia RX3 | 0.5            | 0.0 – 1.0    |
| Medidor/control deslizante de ganancia RX4 | 0.5            | 0.0 – 1.0    |
| Medidor+ganancia TX           | 0.5            | 0.0 – 1.0    |
| Etiqueta de asignación de slice | —              | — o `Slice <letra>` |
| Modo de desbordamiento TX (clic derecho) | Clip           | Clip, NaNGuard, Measure |

Cada medidor/control deslizante también muestra un nivel RX o TX en vivo usando suavizado exponencial — ataque rápido, decaimiento lento — para que la barra refleje la actividad de la señal en ese canal mientras la posición del arrastre establece la ganancia.

Las etiquetas de asignación de slice ahora renderizan las letras de slice con formato de texto enriquecido (#2606). Esto permite que los indicadores de slice externos (por ejemplo, un marcador de color o con estilo en la letra del slice) se muestren correctamente en la etiqueta de estado. El texto de la etiqueta se genera usando `SliceLabel::richText()` en lugar de una letra sin formato, asegurando que cualquier formato HTML incrustado en la representación del slice se conserve.

## Haga clic derecho en la ganancia TX para manejo de desbordamiento

El medidor/control deslizante de ganancia TX tiene un menú contextual con clic derecho que le permite elegir cómo se manejan las muestras de audio fuera de rango (>1.0) de los clientes TCI antes de que lleguen a la radio.

1. Haga clic derecho en cualquier lugar del control deslizante **Ganancia+medidor TX**.
2. Seleccione uno de los tres modos de manejo de desbordamiento:
   - **Clip (saturación ±1.0)** — Recorta forzosamente los excesos a ±1.0. Este es el valor predeterminado heredado e introduce distorsión armónica en los excesos, pero protege la conversión posterior a int16.
   - **NaN guard (solo cero NaN/Inf)** — Pasa las muestras sin cambios; solo pone a cero valores NaN/Inf patológicos. Preserva la fidelidad tonal de los modos digitales; los flotantes fuera de rango aún llegan a la radio.
   - **Measure only (bypass real)** — Nunca muta las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 aún recorta en la ruta DAX nativa de la radio.

El modo seleccionado se persiste como la configuración `TciTxOverflowMode` (valor 0, 1 o 2) y se restaura en el próximo inicio. El valor predeterminado es Clip para que los usuarios existentes no vean cambios en el comportamiento (#3065).

## Qué hace cada modo de desbordamiento TX

| Modo       | Valor | Comportamiento                                                          |
|------------|-------|-------------------------------------------------------------------------|
| Clip       | 0     | Satura las muestras a ±1.0. Valor defensivo predeterminado; introduce armónicos. |
| NaNGuard   | 1     | Pasa las muestras sin cambios excepto poniendo a cero NaN/Inf. Bit- exacto para tonos digitales. |
| Measure    | 2     | Bypass real — nunca muta las muestras. Cuenta los excesos para telemetría. |

## Consejos

- Las etiquetas de asignación de slice (por ejemplo, `Slice A`) siguen el mapeo del canal DAX. Si la asignación del canal DAX de un slice cambia, la etiqueta se actualiza automáticamente.
- Los valores de ganancia se persisten como flotantes de dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que se inicie AetherSDR.
- El modo de desbordamiento TX es particularmente útil para modos digitales donde las muestras fuera de rango deben conservarse sin recorte para la fidelidad tonal bit-exacta. Use **NaN guard** para operación en modo digital y **Measure** para telemetría de diagnóstico.

## Solución de problemas

- **Un canal muestra `—` y no pasa audio al cliente TCI** — No hay ningún slice asignado a ese canal DAX. Asigne un slice al canal DAX correspondiente en la configuración de su radio para que el audio RX de TCI se enrute a ese canal.
- **La selección del modo de desbordamiento TX no persiste** — Verifique que AetherSDR tenga permiso de escritura en su archivo de configuración. La configuración `TciTxOverflowMode` se almacena en la configuración de la aplicación.

## Relacionado

- [Resumen del Servidor TCI](overview.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
