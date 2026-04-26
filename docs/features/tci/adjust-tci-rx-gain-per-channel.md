# Ajustar la ganancia de RX de TCI por canal

El applet TCI Server proporciona cuatro controles deslizantes de ganancia de RX independientes — uno por canal — para controlar el nivel de audio que los clientes TCI reciben de cada slice activo.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe estar en ejecución (Enable activado). Consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- Cada canal de RX que desee ajustar debe tener un slice asignado. Los canales sin asignar muestran `—` en el indicador de slice.

## Pasos

1. Haga clic en el botón de bandeja TCI en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila **RX1**, **RX2**, **RX3** o **RX4** correspondiente al canal que desea ajustar. La etiqueta a la derecha del nombre del canal indica qué slice está asignado (por ejemplo, `Slice A`), o `—` si no hay ningún slice asignado.
3. Arrastre el medidor/control deslizante de esa fila hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de 0.0 a 1.0. El valor predeterminado es 0.5.
4. Suelte el arrastre. El nuevo valor se guarda inmediatamente en el ajuste correspondiente (`TciRxGain1`, `TciRxGain2`, `TciRxGain3` o `TciRxGain4`).

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste guardado |
|---|---|---|---|
| Medidor/control deslizante de ganancia RX1 | 0.5 | 0.0 – 1.0 | `TciRxGain1` |
| Medidor/control deslizante de ganancia RX2 | 0.5 | 0.0 – 1.0 | `TciRxGain2` |
| Medidor/control deslizante de ganancia RX3 | 0.5 | 0.0 – 1.0 | `TciRxGain3` |
| Medidor/control deslizante de ganancia RX4 | 0.5 | 0.0 – 1.0 | `TciRxGain4` |
| Indicador de slice | `—` | `—` o `Slice <letra>` | — |

La parte de medidor de cada fila de RX muestra un nivel de señal en tiempo real mediante suavizado exponencial — ataque rápido, decaimiento lento — de modo que los picos breves sean visibles sin que la lectura sea errática.

El indicador de slice de cada canal de RX sigue la asignación del canal DAX. Si reasigna un slice a un canal DAX diferente, el indicador de RX se actualiza automáticamente.

## Sugerencias

- Los canales sin slice asignado (`—`) no transportan audio. Ajustar la ganancia de un canal sin asignar no tiene efecto audible hasta que se asigne un slice a ese canal DAX.
- Los valores de ganancia se almacenan con dos decimales (por ejemplo, `0.75`). Persisten entre reinicios; no es necesario volver a introducirlos en cada sesión.

## Temas relacionados

- [Ajustar la ganancia de TX de TCI](adjust-tci-tx-gain.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general de TCI Server](overview.md)
