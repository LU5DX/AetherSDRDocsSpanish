# Ajustar la ganancia TX de TCI

Esta página explica cómo establecer la ganancia TX para el audio enviado a los clientes TCI. Ajustar este valor permite igualar el nivel de audio de transmisión que el software de terceros recibe a través de la conexión TCI.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El servidor TCI debe estar habilitado. Si no lo está, consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).
- El applet TCI debe estar visible. Si no lo está, haga clic en el botón TCI de la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón TCI de la barra lateral derecha para abrir el applet TCI.
2. Localice la fila TX. Muestra una etiqueta de asignación de slice (como `Slice A`) o `—` si no hay ningún slice TX asignado, seguida del medidor+ganancia TX.
3. Arrastre el control deslizante del medidor+ganancia TX hacia la izquierda para disminuir la ganancia o hacia la derecha para aumentarla.
4. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Medidor+ganancia TX | Medidor de nivel y control deslizante de ganancia combinados para el audio TX de TCI. Arrastre para ajustar la ganancia. El medidor muestra el nivel TX en tiempo real. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiqueta de asignación de slice RX/TX | Indicador que muestra qué slice controla actualmente la fila TX. Muestra `—` cuando no hay ningún slice TX asignado. | `—` | `—` o `Slice <letter>` | — |

## Consejos

- El medidor+ganancia TX muestra el nivel de audio de transmisión en tiempo real mientras transmite, lo que permite confirmar el nivel antes de establecerlo de forma definitiva.
- La posición del control deslizante se restaura desde `TciTxGain` cada vez que AetherSDR se inicia, por lo que su configuración se mantiene entre sesiones.

## Relacionado

- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del servidor TCI](overview.md)
