# Ajustar la ganancia TCI RX por canal

El applet TCI Server proporciona un control deslizante de ganancia para cada uno de sus cuatro canales RX. Ajustarlos permite igualar el nivel de audio que los clientes TCI (como Log4OM o las herramientas SunSDR) reciben de cada slice (receptor independiente).

## Antes de comenzar

- El radio debe estar conectado. El applet TCI requiere una conexión de radio activa.
- El applet TCI Server debe estar visible. Si el panel del applet no se muestra, haga clic en el botón **TCI** de la barra lateral derecha para revelarlo.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar. La etiqueta de asignación de slice junto al nombre del canal (por ejemplo, `Slice A`) indica qué slice está enviando señal a ese canal. Un `—` significa que no hay ningún slice asignado actualmente.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda o la derecha para establecer la ganancia. El valor se guarda de inmediato.
4. Repita el procedimiento para cualquier otro canal RX que desee ajustar.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Medidor/control deslizante de ganancia RX1 | 0.5 | 0.0 – 1.0 | `TciRxGain1` |
| Medidor/control deslizante de ganancia RX2 | 0.5 | 0.0 – 1.0 | `TciRxGain2` |
| Medidor/control deslizante de ganancia RX3 | 0.5 | 0.0 – 1.0 | `TciRxGain3` |
| Medidor/control deslizante de ganancia RX4 | 0.5 | 0.0 – 1.0 | `TciRxGain4` |
| Etiqueta de asignación de slice | — | — o `Slice <letra>` | *(no se persiste)* |

Cada medidor/control deslizante también muestra un nivel RX en tiempo real mediante suavizado exponencial — ataque rápido, decaimiento lento — de modo que la barra refleja la actividad de la señal en ese canal mientras que la posición de arrastre establece la ganancia.

## Consejos

- Las etiquetas de asignación de slice (por ejemplo, `Slice A`) siguen la asignación de canales DAX. Si cambia la asignación del canal DAX de un slice, la etiqueta se actualiza automáticamente.
- Los valores de ganancia se persisten como números de punto flotante con dos decimales (por ejemplo, `0.75`). Se restauran la próxima vez que AetherSDR inicia.

## Solución de problemas

- **Un canal muestra `—` y no envía audio al cliente TCI** — Ningún slice está asignado a ese canal DAX. Asigne un slice al canal DAX correspondiente en la configuración de su radio para que el audio TCI RX se enrute hacia ese canal.

## Relacionados

- [Descripción general del TCI Server](overview.md)
- [Ajustar la ganancia TCI TX](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
