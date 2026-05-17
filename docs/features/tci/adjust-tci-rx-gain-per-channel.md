# Ajustar la ganancia RX de TCI por canal

El applet del Servidor TCI proporciona un control deslizante de ganancia para cada uno de sus cuatro canales RX. Ajustarlos le permite igualar el nivel de audio que los clientes TCI (como Log4OM o herramientas SunSDR) reciben de cada slice.

## Antes de comenzar

- El radio debe estar conectado. El applet TCI requiere una conexión activa con el radio.
- El applet del Servidor TCI debe estar visible. Si el panel del applet no se muestra, haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar. La etiqueta de asignación de slice junto al nombre del canal (por ejemplo, `Slice A`) indica qué slice está manejando ese canal. Un `—` significa que no hay ningún slice asignado actualmente.
3. Arrastre el medidor/deslizante de esa fila hacia la izquierda o derecha para ajustar la ganancia. El valor se guarda inmediatamente.
4. Repita para cualquier otro canal RX que desee ajustar.

## Función de cada control

| Control                          | Predet. | Rango válido       |
|----------------------------------|---------|--------------------|
| Medidor/deslizante de ganancia RX1 | 0.5     | 0.0 – 1.0         |
| Medidor/deslizante de ganancia RX2 | 0.5     | 0.0 – 1.0         |
| Medidor/deslizante de ganancia RX3 | 0.5     | 0.0 – 1.0         |
| Medidor/deslizante de ganancia RX4 | 0.5     | 0.0 – 1.0         |
| Etiqueta de asignación de slice   | —       | — o `Slice <letra>` |

Cada medidor/deslizante también muestra un nivel RX en vivo utilizando suavizado exponencial — ataque rápido, caída lenta — de modo que la barra refleja la actividad de la señal en ese canal mientras que la posición del deslizante establece la ganancia.

Las etiquetas de asignación de slice ahora muestran las letras de los slices con formato de texto enriquecido (#2606). Esto permite que los indicadores externos de slice (por ejemplo, un marcador colorido o estilizado en la letra del slice) se muestren correctamente en la etiqueta de estado. El texto de la etiqueta se genera usando `SliceLabel::richText()` en lugar de una letra plana, asegurando que cualquier formato HTML incrustado en la representación del slice se conserve.

## Consejos

- Las etiquetas de asignación de slice (por ejemplo, `Slice A`) siguen la asignación del canal DAX. Si la asignación del canal DAX de un slice cambia, la etiqueta se actualiza automáticamente.
- Los valores de ganancia se conservan como flotantes de dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que se inicie AetherSDR.

## Solución de problemas

- **Un canal muestra `—` y no pasa audio al cliente TCI** — No hay ningún slice asignado a ese canal DAX. Asigne un slice al canal DAX correspondiente en la configuración de su radio para que el audio RX de TCI se enrute a ese canal.

## Relacionado

- [Descripción general del Servidor TCI](overview.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
