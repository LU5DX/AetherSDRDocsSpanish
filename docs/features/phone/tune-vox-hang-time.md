# Ajustar el tiempo de retención del VOX

El tiempo de retención del VOX controla cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral del VOX. Ajustarlo evita que el radio vuelva a recepción demasiado rápido entre palabras.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone no está disponible cuando está desconectado.
- El VOX debe estar habilitado. Consulte [Habilitar el VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone en el Panel de Applets. Si no está visible, haga clic en el botón **PHNE** de la bandeja en la barra lateral derecha.
2. Localice la fila **Delay** debajo de la fila del nivel de VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el tiempo de retención o hacia la derecha para aumentarlo. El valor numérico a la derecha del control deslizante se actualiza mientras arrastra.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Delay** | Establece el tiempo de retención del VOX: cuánto tiempo permanece el radio en transmisión después de que el audio cae por debajo del umbral del VOX. | — | 0–100 | — |

No hay ningún valor predeterminado disponible en el catálogo. El rango es de 0 a 100 (escala sin unidades enviada al radio).

## Consejos

- Si el radio vuelve a recepción en medio de una oración, aumente el valor de **Delay**.
- Si el radio permanece en transmisión demasiado tiempo después de que deja de hablar, disminuya el valor de **Delay**.
- El control deslizante **Delay** no tiene efecto a menos que **VOX** esté habilitado.

## Relacionados

- [Habilitar el VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Descripción general de Phone](overview.md)
