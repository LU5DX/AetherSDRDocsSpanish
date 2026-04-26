# Activar VOX y ajustar el umbral de disparo

VOX (transmisión activada por voz) permite que el radio cambie a transmisión automáticamente cuando detecta audio, sin necesidad de presionar PTT. Esta página explica cómo activar VOX y establecer el nivel al que se dispara.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de VOX se envían directamente al FLEX-8600 y requieren una conexión activa.
- El applet Phone debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja PHNE en la barra lateral derecha.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja PHNE en la barra lateral derecha.
2. Haga clic en VOX para habilitar la transmisión activada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante VOX level para establecer el umbral de disparo. Los valores más altos requieren una señal de audio más fuerte antes de que el radio transmita. Rango válido: 0–100.
4. Hable a su nivel de operación normal y observe si hay activaciones no deseadas o disparos fallidos. Ajuste el control deslizante VOX level hacia arriba o hacia abajo según sea necesario, hasta que el radio se active de forma confiable con su voz y no con el ruido de fondo.

## Qué hace cada control

| Control | Tipo | Qué hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|---|
| VOX | Botón de alternancia | Habilita o deshabilita la transmisión activada por voz | — | On / Off | — |
| VOX level | Control deslizante | Establece el umbral de audio al que se activa VOX | — | 0–100 | — |
| Delay | Control deslizante | Establece cuánto tiempo el radio permanece en transmisión después de que el audio se detiene (tiempo de retención) | — | 0–100 | — |

## Consejos

- Si el radio permanece activado después de que deja de hablar, reduzca el control deslizante Delay. Consulte [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md) para más detalles.
- Si el ruido de fondo dispara VOX, aumente el control deslizante VOX level hasta que el ruido ya no active la transmisión.
- El valor numérico junto a cada control deslizante se actualiza en tiempo real mientras lo arrastra.

## Solución de problemas

- **VOX activa el radio con el ruido del entorno** — Aumente el control deslizante VOX level hasta que el umbral supere el piso de ruido.
- **VOX no se dispara cuando habla** — Reduzca el control deslizante VOX level. Si ya está cerca de 0 y el radio aún no se activa, verifique que su micrófono y entrada de audio estén configurados correctamente en `Settings > Radio Setup...`.
- **El radio permanece en transmisión después de que termina el audio** — Reduzca el control deslizante Delay. Consulte [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md).

## Temas relacionados

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
