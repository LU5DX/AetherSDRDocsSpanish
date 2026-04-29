# Ajustar el tiempo de retención del VOX

El tiempo de retención del VOX controla cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral de activación del VOX. Ajustarlo evita cortes intermitentes al final de las palabras y, a su vez, evita silencio excesivo antes de regresar a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone requiere una conexión activa con el radio.
- El VOX debe estar habilitado. Si el VOX no está activo, habilítelo primero — consulte [Habilitar VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Ubique la fila **Delay:**, directamente debajo de la fila del nivel de VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el tiempo de retención o hacia la derecha para aumentarlo. El valor numérico a la derecha del control se actualiza mientras arrastra.

## Qué hace cada control

| Control | Descripción | Rango válido | Valor predeterminado |
|---|---|---|---|
| Control deslizante **Delay** | Establece el tiempo de retención del VOX: cuánto tiempo permanece el radio en transmisión después de que termina el habla antes de regresar a recepción. | 0–100 | — |

No se guarda ninguna clave de configuración para el control deslizante Delay; el valor se envía directamente al radio.

## Consejos

- Un valor de Delay demasiado bajo provoca que el transmisor se corte entre palabras. Aumente el valor hasta que los cortes al final desaparezcan.
- Un valor de Delay demasiado alto mantiene el transmisor activo mucho después de que usted termina de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que la retención sea apenas suficiente para cubrir las pausas normales.
- El umbral del nivel de VOX y el Delay interactúan: un nivel de VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Relacionados

- [Habilitar VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Descripción general de Phone](overview.md)
