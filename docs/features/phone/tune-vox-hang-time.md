# Ajustar el tiempo de retención VOX

El tiempo de retención VOX controla cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral de activación VOX. Ajustarlo evita cortes bruscos al final de las palabras y, al mismo tiempo, previene silencios excesivos antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone requiere una conexión activa con el radio.
- VOX debe estar habilitado. Si VOX no está activado todavía, actívelo primero — consulte [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Localice la fila **Delay:**, directamente debajo de la fila del nivel VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el tiempo de retención o hacia la derecha para aumentarlo. El valor numérico a la derecha del control se actualiza mientras arrastra.

## Qué hace cada control

| Control | Descripción | Rango válido | Valor predeterminado |
|---|---|---|---|
| Control deslizante **Delay** | Establece el tiempo de retención VOX — cuánto tiempo permanece el radio en transmisión después de que termina el audio de voz antes de volver a recepción. | 0–100 | — |

No se guarda ninguna clave de configuración para el control deslizante Delay; el valor se envía directamente al radio.

## Consejos

- Un valor de Delay demasiado bajo provoca que el transmisor se corte entre palabras. Aumente el valor hasta que desaparezcan los cortes al final de las palabras.
- Un valor de Delay demasiado alto mantiene el transmisor activado mucho después de terminar de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que el tiempo de retención sea justo el necesario para cubrir las pausas normales.
- El umbral de nivel VOX y el Delay interactúan: un nivel VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Relacionado

- [Habilitar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Descripción general de Phone](overview.md)
