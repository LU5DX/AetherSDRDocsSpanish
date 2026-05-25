# Applet de Phone

El applet de Phone proporciona controles de transmisión de voz para el nivel de portadora AM, VOX, compuerta de ruido DEXP y frecuencias de corte del filtro de TX. Esta página describe cada control del applet y cómo utilizarlos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Todos los controles del applet de Phone están inactivos sin una conexión de radio.
- El applet de Phone debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de la bandeja PHNE en la barra lateral derecha.

## Cómo abrir el applet de Phone

Haga clic en el botón de la bandeja PHNE en la barra lateral derecha. El applet de Phone se abre en el Panel de Applets.

## Qué hace cada control

| Control | Tipo | Qué hace | Notas |
|---|---|---|---|
| AM Carrier | Deslizador (0–100) | Establece el nivel de potencia de la portadora AM. El valor actual se muestra como un porcentaje junto al deslizador (por ejemplo, `48%`). | — |
| VOX | Botón de alternancia | Activa o desactiva la transmisión por voz. El botón se ilumina en verde cuando está activo. | — |
| VOX level | Deslizador (0–100) | Establece el umbral de audio necesario para activar la transmisión. Muévalo a la derecha para requerir una señal más fuerte; muévalo a la izquierda para activarse con audio más suave. El valor actual se muestra como un porcentaje. | — |
| Delay | Deslizador (0–100) | Establece el tiempo de retención de VOX antes de que la radio vuelva a recepción después de que el audio caiga por debajo del umbral. | — |
| DEXP | Botón de alternancia | Activa o desactiva el expansor descendente (compuerta de ruido). Se conserva en `DexpEnabled`. | No funcional en firmware v1.4.0.0 — la radio devuelve el error `0x5000002D`. |
| DEXP threshold | Deslizador (0–100, predeterminado 0) | Establece el umbral de la compuerta DEXP. Se conserva en `DexpLevel`. El valor actual se muestra como un porcentaje. | Sujeto a la misma limitación de firmware que el botón de alternancia DEXP. |
| Low Cut < / > | Spinbox | Ajusta la frecuencia de corte bajo del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Paso del corte del filtro](#paso-del-corte-del-filtro)). Rango válido: 0 Hz hasta (corte alto − 50 Hz). Predeterminado: 50 Hz. | — |
| High Cut < / > | Spinbox | Ajusta la frecuencia de corte alto del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Paso del corte del filtro](#paso-del-corte-del-filtro)). Rango válido: (corte bajo + 50 Hz) hasta 10000 Hz. Predeterminado: 3300 Hz. | — |

## Habilitar VOX y establecer el umbral de activación

1. Abra el applet de Phone haciendo clic en el botón de la bandeja PHNE en la barra lateral derecha.
2. Haga clic en **VOX** para habilitar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador de **VOX level** para establecer el umbral de activación. Muévalo a la derecha para requerir una señal de audio más fuerte antes de que la radio active la transmisión; muévalo a la izquierda para activarse con audio más suave. Rango válido: 0–100. El porcentaje actual se muestra junto al deslizador.
4. Ajuste el deslizador de **Delay** para establecer cuánto tiempo permanece la radio en transmisión después de que el audio caiga por debajo del umbral antes de volver a recepción.

## Habilitar DEXP

> **Nota:** DEXP no es funcional en firmware v1.4.0.0. La radio devuelve el error `0x5000002D` cuando se utiliza esta función en esa versión de firmware.

1. Abra el applet de Phone.
2. Haga clic en **DEXP** para habilitar la compuerta de ruido del expansor descendente.
3. Ajuste el deslizador de **DEXP threshold** para establecer el umbral de la compuerta. El valor se almacena en `DexpLevel` y persiste entre sesiones. El porcentaje actual se muestra junto al deslizador.

## Establecer frecuencias de corte del filtro de TX

Use **Low Cut < / >** y **High Cut < / >** para dar forma al ancho de banda del audio transmitido.

- Haga clic en `<` para disminuir el valor, haga clic en `>` para aumentarlo. La rueda del ratón también ajusta el valor.
- El corte bajo predeterminado es 50 Hz. El corte alto predeterminado es 3300 Hz.

### Paso del corte del filtro

Desde la versión v0.9.5.1, los botones `<` y `>` se ajustan al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

**Ejemplo:** Si el corte bajo es actualmente 87 Hz:
- Al presionar `>` (aumentar) se ajusta a **100 Hz** (siguiente múltiplo de 50 por encima de 87).
- Al presionar `<` (disminuir) se ajusta a **50 Hz** (siguiente múltiplo de 50 por debajo de 87).

Esto significa que el valor siempre termina en un límite limpio de 50 Hz, independientemente de su punto de partida. La radio acepta cualquier valor entero de Hz; esto es solo una conveniencia de la interfaz de usuario.

## Consejos

- Si la radio activa la transmisión por ruido de fondo, aumente el valor del deslizador de **VOX level** para que se requiera una señal más fuerte para activar la transmisión.
- Si VOX se interrumpe a media sílaba, aumente el deslizador de **Delay** para extender el tiempo de retención.
- Si DEXP está habilitado y la compuerta de ruido está cortando su audio, baje el valor del deslizador de **DEXP threshold**.

## Solución de problemas

- **La radio no activa la transmisión cuando habla** — El nivel de VOX puede estar configurado demasiado alto. Baje el deslizador de **VOX level** para que el audio más suave active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el deslizador de **Delay** para acortar el tiempo de retención.
- **El botón de alternancia DEXP no tiene efecto** — Esta es una limitación conocida del firmware v1.4.0.0. La radio devuelve el error `0x5000002D`. No hay solución alternativa disponible a nivel de firmware.

## Relacionados

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
