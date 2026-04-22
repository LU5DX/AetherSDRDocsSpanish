# Ajustar el tiempo de retención del VOX

El tiempo de retención del VOX controla cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral del VOX. Ajustarlo evita que el radio corte el final de su transmisión o que permanezca en TX demasiado tiempo entre palabras.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone no está disponible sin una conexión al radio.
- El VOX debe estar habilitado. Consulte [Habilitar el VOX y configurar el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice el control deslizante **Delay** en el applet Phone.
3. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el tiempo de retención, o hacia la derecha para aumentarlo. El valor numérico a la derecha del control se actualiza mientras arrastra.

## Qué hace cada control

| Control | Descripción | Rango válido | Predeterminado | Clave de configuración |
|---|---|---|---|---|
| **Delay** | Establece el tiempo de retención del VOX: cuánto tiempo permanece el radio en transmisión después de que el audio cae por debajo del umbral del VOX. | 0–100 | — | — |

## Consejos

- Si el radio vuelve a recepción entre palabras, aumente el valor de **Delay**.
- Si el radio permanece en transmisión demasiado tiempo después de que usted deja de hablar, reduzca el valor de **Delay**.

## Relacionados

- [Habilitar el VOX y configurar el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Descripción general de Phone](overview.md)
