# Ajustar tiempo de retardo VOX

El tiempo de retardo VOX controla cuánto tiempo la radio permanece en transmisión después de que tu voz cae por debajo del umbral de disparo VOX. Ajustarlo evita cortes entrecortados en la transmisión al final de las palabras, a la vez que se evita aire muerto excesivo antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión de radio activa.
- VOX debe estar habilitado. Si VOX aún no está activado, habilítalo primero — consulta [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abre el applet Phone haciendo clic en el botón de bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haz clic en el borde del panel o usa `View > Applet Panel` para mostrarlo.
2. Localiza la fila **Delay:**, directamente debajo de la fila de nivel VOX.
3. Arrastra el regulador **Delay** hacia la izquierda para acortar el tiempo de retardo o hacia la derecha para alargarlo. El valor numérico a la derecha del regulador se actualiza mientras lo arrastras.

## Qué hace cada control

| Control          | Descripción                                                                                                    | Rango válido |
|------------------|----------------------------------------------------------------------------------------------------------------|-------------|
| Regulador **Delay** | Establece el tiempo de retardo VOX — cuánto tiempo la radio permanece en transmisión después de que la voz termina antes de volver a recepción. | 0–100       |

No se persiste ninguna clave de configuración para el regulador Delay; el valor se envía directamente a la radio.

## Consejos

- Un valor Delay demasiado bajo causa que el transmisor se encienda y apague entre palabras. Aumenta el valor hasta que dejen de ocurrir cortes en la cola.
- Un valor Delay demasiado alto mantiene el transmisor activado mucho después de que termines de hablar, bloqueando otras estaciones. Reduce el valor hasta que el retardo sea apenas lo suficiente para cubrir pausas normales.
- El umbral de nivel VOX y Delay interactúan: un nivel VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Relacionado

- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Phone overview](overview.md)
