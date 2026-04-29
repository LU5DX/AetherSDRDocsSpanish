# Habilitar VOX y ajustar el umbral de activación

VOX (transmisión activada por voz) acciona automáticamente el transmisor cuando su audio supera un nivel establecido, de modo que no es necesario presionar PTT durante la operación en fonofonía. Esta página explica cómo habilitar VOX y ajustar su umbral de activación en el applet Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los controles de VOX están inactivos sin una conexión de radio.
- El applet Phone debe estar visible en el panel de applets. Si no lo está, haga clic en el botón PHNE de la barra lateral derecha.

## Pasos

1. Abra el applet Phone haciendo clic en el botón PHNE de la barra lateral derecha.
2. Haga clic en VOX para habilitar la transmisión activada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante VOX level para establecer el umbral de activación. Muévalo hacia la derecha para requerir una señal de audio más fuerte antes de que la radio transmita; muévalo hacia la izquierda para activar la transmisión con audio más silencioso. Rango válido: 0–100.

## Qué hace cada control

| Control | Tipo | Función | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|---|---|
| VOX | Botón de alternancia | Habilita o deshabilita la transmisión activada por voz | — | On / Off | — |
| VOX level | Control deslizante | Establece el umbral de audio necesario para activar la transmisión | — | 0–100 | — |
| Delay | Control deslizante | Establece el tiempo de retención antes de que la radio vuelva a recepción tras caer el audio por debajo del umbral | — | 0–100 | — |

## Consejos

- Si la radio transmite involuntariamente por ruido de fondo, aumente el valor del control deslizante VOX level.
- Si VOX se interrumpe a mitad de una sílaba, aumente el control deslizante Delay para extender el tiempo de retención antes de que la radio vuelva a recepción.

## Solución de problemas

- **La radio no transmite cuando usted habla** — Es posible que VOX level esté demasiado alto. Reduzca el valor del control deslizante VOX level para que el audio más silencioso active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de que usted deja de hablar** — Reduzca el valor del control deslizante Delay para acortar el tiempo de retención.

## Relacionado

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
