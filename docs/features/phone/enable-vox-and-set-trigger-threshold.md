# Applet de Phone

El applet de Phone proporciona controles de TX de voz para el nivel de portadora AM, VOX, compuerta de ruido DEXP y frecuencias de corte del filtro de TX. Esta página describe cada control del applet y cómo usarlos.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Todos los controles del applet de Phone están inactivos sin una conexión de radio.
- El applet de Phone debe ser visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja PHNE en la barra lateral derecha.

## Abrir el applet de Phone

Haga clic en el botón de bandeja PHNE en la barra lateral derecha. El applet de Phone se abre en el Panel de Applets.

## Qué hace cada control

| Control        | Tipo                                                                                                                                                                                                                           | Qué hace                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AM Carrier     | Deslizador (0–100)                                                                                                                                                                                                             | Establece el nivel de potencia de la portadora AM. El valor actual se muestra como porcentaje junto al deslizador (por ejemplo, `48%`).                                      |
| VOX            | Botón de conmutación                                                                                                                                                                                                           | Activa/desactiva la transmisión por voz. El botón se ilumina en verde cuando está activo.                                                                                   |
| VOX level      | Deslizador (0–100)                                                                                                                                                                                                             | Establece el umbral de audio necesario para activar la transmisión. Muévalo a la derecha para requerir una señal más fuerte; muévalo a la izquierda para activar con audio más silencioso. El valor actual se muestra como porcentaje. |
| Delay          | Deslizador (0–100)                                                                                                                                                                                                             | Establece el tiempo de retención de VOX antes de que la radio vuelva a recepción después de que el audio caiga por debajo del umbral.                                         |
| DEXP           | Botón de conmutación                                                                                                                                                                                                           | Activa/desactiva el expansor descendente (compuerta de ruido).                                                                                                               |
| DEXP threshold | Deslizador (0–100, predeterminado 0)                                                                                                                                                                                           | Establece el umbral de la compuerta DEXP. El valor actual se muestra como porcentaje.                                                                                       |
| Low Cut < / >  | < / > o la rueda del mouse ajusta el corte bajo del filtro de TX en pasos de 50 Hz. Haga doble clic en el valor para escribir un valor exacto en Hz, que se respeta en radios que lo aceptan mientras la lectura propia de la radio se conserva en otros lugares (#3627, #5064). | Un número escrito se trata como una solicitud de ese valor exacto, mientras que los botones de paso se ajustan a la cuadrícula de pasos de la radio.                          |
| High Cut < / > | < / > o la rueda del mouse ajusta el corte alto del filtro de TX en pasos de 50 Hz. Haga doble clic en el valor para escribir un valor exacto en Hz, que se respeta en radios que lo aceptan mientras la lectura propia de la radio se conserva en otros lugares (#3627, #5064). | Un número escrito se trata como una solicitud de ese valor exacto, mientras que los botones de paso se ajustan a la cuadrícula de pasos de la radio.                          |

### Paso del filtro de TX con bordes discretos

Algunas radios informan un conjunto discreto de valores válidos de borde de filtro en lugar de aceptar cualquier Hz entero. Cuando se conecta una radio de este tipo, los botones `<` y `>` se mueven al borde válido más cercano en la dirección elegida en lugar de ajustarse a un múltiplo de 50 Hz. Los valores escritos también se rechazan si no están en el conjunto de bordes informado por la radio.

## Activar VOX y establecer el umbral de activación

1. Abra el applet de Phone haciendo clic en el botón de bandeja PHNE en la barra lateral derecha.
2. Haga clic en **VOX** para activar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el deslizador **VOX level** para establecer el umbral de activación. Muévalo a la derecha para requerir una señal de audio más fuerte antes de que la radio transmita; muévalo a la izquierda para activar con audio más silencioso. Rango válido: 0–100. El porcentaje actual se muestra junto al deslizador.
4. Ajuste el deslizador **Delay** para establecer cuánto tiempo permanece la radio en transmisión después de que el audio caiga por debajo del umbral antes de volver a recepción.

## Activar DEXP

1. Abra el applet de Phone.
2. Haga clic en **DEXP** para activar la compuerta de ruido del expansor descendente.
3. Ajuste el deslizador **DEXP threshold** para establecer el umbral de la compuerta. El porcentaje actual se muestra junto al deslizador.

## Establecer frecuencias de corte del filtro de TX

Use **Low Cut < / >** y **High Cut < / >** para dar forma al ancho de banda del audio transmitido.

- Haga clic en `<` para disminuir el valor, haga clic en `>` para aumentarlo. La rueda del mouse también ajusta el valor.
- El corte bajo predeterminado es de 50 Hz. El corte alto predeterminado es de 3300 Hz.

### Paso del corte del filtro

Los botones `<` y `>` se ajustan al valor válido más cercano en la dirección elegida en lugar de sumar o restar un fijo de 50 Hz al valor actual.

**Ejemplo (radio que acepta cualquier Hz entero):** Si el corte bajo es actualmente 87 Hz:
- Presionar `>` (aumentar) se ajusta a **100 Hz** (siguiente múltiplo de 50 por encima de 87).
- Presionar `<` (disminuir) se ajusta a **50 Hz** (siguiente múltiplo de 50 por debajo de 87).

**Ejemplo (radio con bordes discretos):** Si la radio informa bordes válidos de corte bajo de 0, 50, 100, 200 y 300 Hz, y el valor actual es 100 Hz:
- Presionar `>` (aumentar) se mueve a **200 Hz**.
- Presionar `<` (disminuir) se mueve a **50 Hz**.

### Escribir un valor exacto

Haga doble clic en el valor de corte bajo o corte alto para escribir un número exacto en Hz. El valor se acepta solo si está dentro del rango válido y, en radios que informan bordes discretos, es uno de los bordes informados. Los valores fuera de rango se rechazan y se restaura el valor anterior.

## Consejos

- Si la radio activa la transmisión por ruido de fondo, aumente el valor del deslizador **VOX level** para que se requiera una señal más fuerte para activar la transmisión.
- Si VOX se corta a mitad de sílaba, aumente el deslizador **Delay** para extender el tiempo de retención.
- Si DEXP está activado y la compuerta de ruido está cortando su audio, reduzca el valor del deslizador **DEXP threshold**.

## Solución de problemas

- **La radio no transmite cuando habla** — El nivel de VOX puede estar demasiado alto. Reduzca el deslizador **VOX level** para que el audio más silencioso active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el deslizador **Delay** para acortar el tiempo de retención.
- **El valor de filtro escrito es rechazado** — El valor puede estar fuera del rango válido o, en radios que informan bordes discretos, no ser un borde válido para ese filtro. Use los botones de paso para moverse a un valor válido.

## Relacionado

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
