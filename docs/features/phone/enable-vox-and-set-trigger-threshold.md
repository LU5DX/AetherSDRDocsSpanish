# Applet de Phone

El applet de Phone proporciona controles de transmisión de voz para el nivel de portadora AM, VOX, compuerta de ruido DEXP y frecuencias de corte del filtro de TX. Esta página describe cada control del applet y cómo utilizarlos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Todos los controles del applet de Phone están inactivos sin una conexión a la radio.
- El applet de Phone debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja PHNE en la barra lateral derecha.

## Cómo abrir el applet de Phone

Haga clic en el botón de la bandeja PHNE en la barra lateral derecha. El applet de Phone se abre en el Panel de Applets.

## Función de cada control

| Control | Tipo | Función | Notas |
|---|---|---|---|
| AM Carrier | Deslizador (0–100) | Ajusta el nivel de potencia de la portadora AM. El valor actual se muestra como un número junto al deslizador (por ejemplo, `48`). | — |
| VOX | Botón de alternancia | Activa o desactiva la transmisión por voz. El botón se ilumina en verde cuando está activo. | — |
| VOX level | Deslizador (0–100) | Ajusta el umbral de audio necesario para activar la transmisión. Muévalo a la derecha para requerir una señal más fuerte; muévalo a la izquierda para activarse con audio más bajo. | — |
| Delay | Deslizador (0–100) | Ajusta el tiempo de retención de VOX antes de que la radio vuelva a recepción después de que el audio caiga por debajo del umbral. | — |
| DEXP | Botón de alternancia | Activa o desactiva el expansor descendente (compuerta de ruido). Se persiste en `DexpEnabled`. | No funcional en firmware v1.4.0.0 — la radio devuelve el error `0x5000002D`. |
| DEXP threshold | Deslizador (0–100, valor predeterminado 0) | Ajusta el umbral de la compuerta DEXP. Se persiste en `DexpLevel`. | Sujeto a la misma limitación de firmware que la alternancia DEXP. |
| Low Cut < / > | Cuadro de incremento | Ajusta la frecuencia de corte bajo del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para escalonar el valor. Los escalones se fijan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Escalonado del corte del filtro](#escalonado-del-corte-del-filtro)). Rango válido: 0 Hz hasta (corte alto − 50 Hz). | — |
| High Cut < / > | Cuadro de incremento | Ajusta la frecuencia de corte alto del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para escalonar el valor. Los escalones se fijan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Escalonado del corte del filtro](#escalonado-del-corte-del-filtro)). Rango válido: (corte bajo + 50 Hz) hasta 10000 Hz. | — |

## Activar VOX y ajustar el umbral de disparo

1. Abra el applet de Phone haciendo clic en el botón de la bandeja PHNE en la barra lateral derecha.
2. Haga clic en **VOX** para activar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador **VOX level** para definir el umbral de activación. Muévalo a la derecha para requerir una señal de audio más fuerte antes de que la radio transmita; muévalo a la izquierda para activarse con audio más bajo. Rango válido: 0–100.
4. Ajuste el deslizador **Delay** para definir cuánto tiempo permanece la radio en transmisión después de que el audio caiga por debajo del umbral antes de volver a recepción.

## Activar DEXP

> **Nota:** DEXP no es funcional en firmware v1.4.0.0. La radio devuelve el error `0x5000002D` cuando se usa esta función en esa versión de firmware.

1. Abra el applet de Phone.
2. Haga clic en **DEXP** para activar la compuerta de ruido del expansor descendente.
3. Ajuste el deslizador **DEXP threshold** para definir el umbral de la compuerta. El valor se almacena en `DexpLevel` y persiste entre sesiones.

## Ajustar las frecuencias de corte del filtro de TX

Use **Low Cut < / >** y **High Cut < / >** para dar forma al ancho de banda del audio transmitido.

- Haga clic en `<` para disminuir el valor, haga clic en `>` para aumentarlo. La rueda del ratón también ajusta el valor.
- El corte bajo predeterminado es 50 Hz. El corte alto predeterminado es 3300 Hz.

### Escalonado del corte del filtro

A partir de v0.9.5.1, los botones `<` y `>` se fijan al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz del valor actual.

**Ejemplo:** Si el corte bajo es actualmente 87 Hz:
- Presionar `>` (aumentar) se fija en **100 Hz** (siguiente múltiplo de 50 por encima de 87).
- Presionar `<` (disminuir) se fija en **50 Hz** (siguiente múltiplo de 50 por debajo de 87).

Esto significa que el valor siempre aterriza en un límite limpio de 50 Hz independientemente de su punto de partida. La radio acepta cualquier valor entero en Hz; esto es solo una conveniencia de la interfaz de usuario.

## Consejos

- Si la radio se activa con ruido de fondo, aumente el valor del deslizador **VOX level** para que se requiera una señal más fuerte para activar la transmisión.
- Si VOX se corta a media sílaba, aumente el deslizador **Delay** para extender el tiempo de retención.
- Si DEXP está activado y la compuerta de ruido corta su audio, reduzca el valor del deslizador **DEXP threshold**.

## Solución de problemas

- **La radio no transmite cuando habla** — El nivel de VOX puede estar demasiado alto. Reduzca el deslizador **VOX level** para que el audio más bajo active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el deslizador **Delay** para acortar el tiempo de retención.
- **La alternancia DEXP no tiene efecto** — Esta es una limitación conocida del firmware en v1.4.0.0. La radio devuelve el error `0x5000002D`. No hay solución alternativa disponible a nivel de firmware.

## Relacionado

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Visión general de Phone](overview.md)
