# Applet de Phone

El applet de Phone proporciona controles de transmisión de voz para el nivel de portadora AM, VOX, puerta de ruido DEXP y frecuencias de corte del filtro de TX. Esta página describe cada control del applet y cómo usarlos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Todos los controles del applet de Phone están inactivos sin una conexión de radio.
- El applet de Phone debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja PHNE en la barra lateral derecha.

## Abrir el applet de Phone

Haga clic en el botón de bandeja PHNE en la barra lateral derecha. El applet de Phone se abre en el Panel de Applets.

## Qué hace cada control

| Control | Tipo | Qué hace | Notas |
|---|---|---|---|
| AM Carrier | Deslizador (0–100) | Establece el nivel de potencia de la portadora AM. El valor actual se muestra como un porcentaje junto al deslizador (por ejemplo, `48%`). | — |
| VOX | Botón de alternancia | Activa/desactiva la transmisión por voz. El botón se ilumina en verde cuando está activo. | — |
| VOX level | Deslizador (0–100) | Establece el umbral de audio necesario para activar la transmisión. Muévalo a la derecha para requerir una señal más fuerte; muévalo a la izquierda para activarse con audio más bajo. El valor actual se muestra como porcentaje. | — |
| Delay | Deslizador (0–100) | Establece el tiempo de retención de VOX antes de que la radio vuelva a recibir después de que el audio caiga por debajo del umbral. | — |
| DEXP | Botón de alternancia | Activa/desactiva el expansor descendente (puerta de ruido). | — |
| DEXP threshold | Deslizador (0–100, predeterminado 0) | Establece el umbral de la puerta DEXP. El valor actual se muestra como porcentaje. | — |
| Low Cut < / > | Cuadro de giro | Ajusta la frecuencia de corte bajo del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se redondean al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Paso de corte del filtro](#paso-de-corte-del-filtro)). Rango válido: 0 Hz hasta (corte alto − 50 Hz). Predeterminado: 50 Hz. | — |
| High Cut < / > | Cuadro de giro | Ajusta la frecuencia de corte alto del filtro de TX. Haga clic en `<` o `>`, o use la rueda del ratón, para cambiar el valor. Los pasos se redondean al múltiplo de 50 Hz más cercano en la dirección elegida (consulte [Paso de corte del filtro](#paso-de-corte-del-filtro)). Rango válido: (corte bajo + 50 Hz) hasta 10000 Hz. Predeterminado: 3300 Hz. | — |

## Activar VOX y establecer el umbral de activación

1. Abra el applet de Phone haciendo clic en el botón de bandeja PHNE en la barra lateral derecha.
2. Haga clic en **VOX** para activar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador de **VOX level** para establecer el umbral de activación. Muévalo a la derecha para requerir una señal de audio más fuerte antes de que la radio active la transmisión; muévalo a la izquierda para activarse con audio más bajo. Rango válido: 0–100. El porcentaje actual se muestra junto al deslizador.
4. Ajuste el deslizador de **Delay** para establecer cuánto tiempo permanece la radio en transmisión después de que el audio caiga por debajo del umbral antes de volver a recepción.

## Activar DEXP

1. Abra el applet de Phone.
2. Haga clic en **DEXP** para activar la puerta de ruido del expansor descendente.
3. Ajuste el deslizador de **DEXP threshold** para establecer el umbral de la puerta. El porcentaje actual se muestra junto al deslizador.

## Establecer frecuencias de corte del filtro de TX

Use **Low Cut < / >** y **High Cut < / >** para dar forma al ancho de banda del audio transmitido.

- Haga clic en `<` para disminuir el valor, haga clic en `>` para aumentarlo. La rueda del ratón también ajusta el valor.
- El corte bajo predeterminado es 50 Hz. El corte alto predeterminado es 3300 Hz.

### Paso de corte del filtro

Los botones `<` y `>` se redondean al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz del valor actual.

**Ejemplo:** Si el corte bajo es actualmente 87 Hz:
- Presionar `>` (aumentar) se redondea a **100 Hz** (siguiente múltiplo de 50 por encima de 87).
- Presionar `<` (disminuir) se redondea a **50 Hz** (siguiente múltiplo de 50 por debajo de 87).

Esto significa que el valor siempre termina en un límite limpio de 50 Hz independientemente de su punto de partida. La radio acepta cualquier valor entero en Hz; esto es solo una conveniencia de la interfaz de usuario.

## Consejos

- Si la radio se activa con ruido de fondo, aumente el valor del deslizador de **VOX level** para que se requiera una señal más fuerte para activar la transmisión.
- Si VOX se desactiva a media sílaba, aumente el deslizador de **Delay** para extender el tiempo de retención.
- Si DEXP está activado y la puerta de ruido está cortando su audio, reduzca el valor del deslizador de **DEXP threshold**.

## Solución de problemas

- **La radio no activa la transmisión cuando habla** — El nivel de VOX puede estar demasiado alto. Reduzca el deslizador de **VOX level** para que el audio más bajo active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el deslizador de **Delay** para acortar el tiempo de retención.

## Relacionado

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
