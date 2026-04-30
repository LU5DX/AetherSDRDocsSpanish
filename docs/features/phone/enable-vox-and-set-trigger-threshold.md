# Habilitar VOX y ajustar el umbral de activación

VOX (transmisión por voz) activa automáticamente el transmisor cuando su audio supera un nivel establecido, por lo que no necesita presionar PTT durante la operación en teléfono. Esta página explica cómo habilitar VOX y ajustar su umbral de activación en el applet Phone.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Los controles VOX están inactivos sin conexión de radio.
- El applet Phone debe ser visible en el Applet Panel. Si no lo está, haga clic en el botón de bandeja PHNE en la barra lateral derecha.

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja PHNE en la barra lateral derecha.
2. Haga clic en VOX para habilitar la transmisión por voz. El botón se ilumina en verde cuando está activo.
3. Ajuste el control deslizante VOX level para establecer el umbral de activación. Muévalo hacia la derecha para requerir una señal de audio más fuerte antes de que se active la radio; muévalo hacia la izquierda para activarse con audio más bajo. Rango válido: 0–100.

## Qué hace cada control

| Control   | Tipo                                                                | Función                                                                                                                              |
|-----------|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| VOX       | Alterna la transmisión por voz; llama a TransmitModel::setVoxEnable. | v0.9.3: setVoxEnable ahora emite phoneStateChanged para que el panel Phone se actualice inmediatamente cuando VOX se alterna por atajo de teclado (#2084). |
| VOX level | Control deslizante                                                              | Establece el umbral de audio requerido para activar la transmisión                                                                                    |
| Delay     | Control deslizante                                                              | Establece el tiempo de retardo antes de que la radio vuelva a recepción después de que el audio cae por debajo del umbral                                              |

## Consejos

- Si la radio se activa involuntariamente por ruido de fondo, aumente el valor del control deslizante VOX level.
- Si VOX se corta en medio de una sílaba, aumente el control deslizante Delay para extender el tiempo de retardo antes de que la radio vuelva a recepción.

## Solución de problemas

- **La radio no se activa cuando habla** — VOX level puede estar establecido demasiado alto. Baje el valor del control deslizante VOX level para que audio más bajo active la transmisión.
- **La radio permanece en transmisión demasiado tiempo después de dejar de hablar** — Disminuya el valor del control deslizante Delay para acortar el tiempo de retardo.

## Relacionado

- [Ajustar el tiempo de retardo VOX](tune-vox-hang-time.md)
- [Descripción general de Phone](overview.md)
