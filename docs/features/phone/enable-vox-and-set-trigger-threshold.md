# Habilitar VOX y ajustar el umbral de activación

Use el applet Phone para activar la transmisión controlada por voz (VOX) y ajustar su sensibilidad al audio. VOX activa automáticamente el transmisor cuando usted habla, eliminando la necesidad de presionar un botón PTT.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de VOX se envían directamente al FLEX-8600 y requieren una conexión activa.
- El applet Phone debe estar visible. Si no lo está, haga clic en el botón PHNE del panel lateral derecho para mostrarlo.

## Pasos

1. Abra el applet Phone haciendo clic en el botón PHNE del panel lateral derecho.
2. Haga clic en el botón de alternancia **VOX** para habilitar la transmisión controlada por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante **VOX level** para establecer el umbral de activación. Muévalo hacia la derecha para requerir una señal de audio más fuerte antes de que el radio transmita; muévalo hacia la izquierda para aumentar la sensibilidad. El rango válido es 0–100. El valor actual se muestra como un número a la derecha del control deslizante.

## Qué hace cada control

| Control | Tipo | Rango válido | Predeterminado | Comportamiento |
|---|---|---|---|---|
| VOX | Botón de alternancia | On / Off | Off | Habilita o deshabilita la transmisión controlada por voz. |
| VOX level | Control deslizante | 0–100 | — | Establece el nivel de audio requerido para activar el transmisor. Valores más altos requieren audio más fuerte. |

## Consejos

- Después de ajustar el umbral, observe el indicador de transmisión mientras habla a su nivel operativo normal. Si el radio transmite con el ruido de fondo, aumente el valor de **VOX level**. Si no activa la transmisión con la voz, disminúyalo.
- El tiempo de retención de VOX (cuánto tiempo permanece el radio en transmisión después de dejar de hablar) se controla por separado con el control deslizante **Delay**. Consulte [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md).

## Solución de problemas

- **VOX no activa el radio aunque se hable en voz alta** — El umbral de **VOX level** puede estar demasiado alto. Mueva el control deslizante hacia 0 para reducir el nivel de activación requerido.
- **VOX se activa con ruido de fondo o sonido ambiental** — El umbral de **VOX level** es demasiado bajo. Mueva el control deslizante hacia 100 hasta que el ruido ambiental deje de activar el transmisor.

## Relacionados

- [Ajustar el tiempo de retención de VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
- [Establecer la frecuencia de corte inferior del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Establecer la frecuencia de corte superior del audio de TX](set-the-tx-audio-high-cut-frequency.md)
