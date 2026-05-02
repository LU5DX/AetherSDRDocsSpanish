# Applet Phone

El applet Phone proporciona controles de TX de voz para el nivel de portadora AM, VOX, puerta de ruido DEXP y frecuencias de corte del filtro de TX. Esta página describe cada control del applet y cómo utilizarlos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Todos los controles del applet Phone están inactivos sin una conexión de radio.
- El applet Phone debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja PHNE en la barra lateral derecha.

## Abrir el applet Phone

Haga clic en el botón de bandeja PHNE en la barra lateral derecha. El applet Phone se abre en el Panel de Applets.

## Qué hace cada control

| Control | Tipo | Función | Notas |
|---|---|---|---|
| AM Carrier | Deslizador (0–100) | Establece el nivel de potencia de la portadora AM. El valor actual se muestra como un número junto al deslizador (por ejemplo, `48`). | — |
| VOX | Botón de alternancia | Activa o desactiva la transmisión controlada por voz. El botón se ilumina en verde cuando está activo. | — |
| VOX level | Deslizador (0–100) | Establece el umbral de audio necesario para activar la transmisión. Muévalo a la derecha para requerir una señal más fuerte; muévalo a la izquierda para activar con audio más bajo. | — |
| Delay | Deslizador (0–100) | Establece el tiempo de retención del VOX antes de que la radio vuelva a recepción tras caer el audio por debajo del umbral. | — |
| DEXP | Botón de alternancia | Activa o desactiva el expansor descendente (puerta de ruido). Se guarda en `DexpEnabled`. | No funcional en el firmware v1.4.0.0 — la radio devuelve el error `0x5000002D`. |
| DEXP threshold | Deslizador (0–100, valor predeterminado 0) | Establece el umbral de la puerta DEXP. Se guarda en `DexpLevel`. | Sujeto a la misma limitación de firmware que el botón de alternancia DEXP. |
| Low Cut < / > | Cuadro de giro | Ajusta la frecuencia de corte inferior del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Incremento del corte de filtro](#filter-cut-stepping)). Rango válido: 0 Hz hasta (corte superior − 50 Hz). | — |
| High Cut < / > | Cuadro de giro | Ajusta la frecuencia de corte superior del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Incremento del corte de filtro](#filter-cut-stepping)). Rango válido: (corte inferior + 50 Hz) hasta 10000 Hz. | — |

## Activar VOX y establecer el umbral de activación

1. Abra el applet Phone haciendo clic en el botón de bandeja PHNE en la barra lateral derecha.
2. Haga clic en **VOX** para activar la transmisión controlada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador **VOX level** para establecer el umbral de activación. Muévalo a la derecha para requerir una señal de audio más fuerte antes de que la radio transmita; muévalo a la izquierda para activar con audio más bajo. Rango válido: 0–100.
4. Ajuste el deslizador **Delay** para establecer cuánto tiempo permanece la radio en transmisión tras caer el audio por debajo del umbral antes de volver a recepción.

## Activar DEXP

> **Nota:** DEXP no es funcional en el firmware v1.4.0.0. La radio devuelve el error `0x5000002D` cuando se utiliza esta función en esa versión de firmware.

1. Abra el applet Phone.
2. Haga clic en **DEXP** para activar la puerta de ruido del expansor descendente.
3. Ajuste el deslizador **DEXP threshold** para establecer el umbral de la puerta. El valor se almacena en `DexpLevel` y se conserva entre sesiones.

## Establecer las frecuencias de corte del filtro de TX

Use **Low Cut < / >** y **High Cut < / >** para dar forma al ancho de banda de audio transmitido.

- Haga clic en `<` para disminuir el valor; haga clic en `>` para aumentarlo. La rueda del ratón también ajusta el valor.
- El corte inferior predeterminado es 50 Hz. El corte superior predeterminado es 3300 Hz.

### Incremento del corte de filtro

A partir de la versión v0.9.5.1, los botones `<` y `>` se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

**Ejemplo:** Si el corte inferior es actualmente 87 Hz:
- Presionar `>` (aumentar) ajusta a **100 Hz** (siguiente múltiplo de 50 por encima de 87).
- Presionar `<` (disminuir) ajusta a **50 Hz** (siguiente múltiplo de 50 por debajo de 87).

Esto significa que el valor siempre queda en un límite exacto de 50 Hz independientemente de su punto de partida. La radio acepta cualquier valor entero en Hz; esto es únicamente una conveniencia de la interfaz.

## Consejos

- Si la radio transmite con el ruido de fondo, aumente el valor del deslizador **VOX level** para que se requiera una señal más fuerte para activar la transmisión.
- Si el VOX se corta a mitad de una sílaba, aumente el deslizador **Delay** para extender el tiempo de retención.
- Si DEXP está activado y la puerta de ruido está cortando su audio, disminuya el valor del deslizador **DEXP threshold**.

## Solución de problemas

- **La radio no transmite cuando habla** — El nivel de VOX puede estar demasiado alto. Disminuya el deslizador **VOX level** para que el audio más bajo active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el deslizador **Delay** para acortar el tiempo de retención.
- **El botón de alternancia DEXP no tiene efecto** — Esta es una limitación conocida del firmware en v1.4.0.0. La radio devuelve el error `0x5000002D`. No hay solución alternativa disponible a nivel de firmware.

## Relacionados

- [Ajustar el tiempo de retención del VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
