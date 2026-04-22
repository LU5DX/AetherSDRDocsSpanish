# Ajustar la ganancia TX de TCI

Esta página explica cómo configurar la ganancia TX de TCI en el applet TCI Server. Ajustar la ganancia TX controla el nivel del audio de transmisión enviado a los clientes TCI conectados, como Log4OM o las herramientas SunSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El applet TCI Server debe estar visible. Si no lo está, haga clic en el botón TCI del área de notificación en la barra lateral derecha para mostrarlo.
- El servidor TCI debe estar en ejecución (Enable activado) para que los cambios de ganancia surtan efecto en los clientes conectados.

## Pasos

1. Haga clic en el botón TCI del área de notificación en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila TX. La etiqueta a la izquierda muestra "TX:" e indica a su derecha el slice (canal de recepción/transmisión) asignado (ya sea "—" o "Slice \<letter\>").
3. Arrastre el control deslizante TX gain+meter para establecer la ganancia deseada. Arrastre a la derecha para aumentar y a la izquierda para disminuir.
4. Suelte el control deslizante. El valor se guarda automáticamente como `TciTxGain`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el audio TX de TCI. Arrastre para ajustar la ganancia; el medidor refleja el nivel de señal TX en tiempo real. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Indicador de slice TX | Muestra qué slice impulsa actualmente la fila TX (por ejemplo, "Slice A"). Muestra "—" cuando no hay ningún slice TX asignado. | — | "—" o "Slice \<letter\>" | *(ninguna)* |

## Consejos

- El TX gain+meter muestra el nivel de señal de transmisión en tiempo real mientras transmite, lo que le permite verificar la configuración de ganancia en condiciones reales.
- `TciTxGain` se guarda automáticamente cuando mueve el control deslizante. No se requiere ningún paso adicional para guardar.

## Solución de problemas

- **El indicador de slice TX muestra "—"** — Actualmente ningún slice está designado como slice TX en la radio. Asigne un slice TX en los controles de slice de la radio y luego regrese a este applet.
- **La posición del control deslizante no coincide con lo que reportan los clientes TCI** — El servidor TCI lee `TciTxGain` al iniciarse. Si el valor fue modificado externamente, reinicie el servidor TCI haciendo clic en Enable para desactivarlo y luego en Enable para activarlo de nuevo.

## Relacionados

- [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Descripción general de TCI Server](overview.md)
