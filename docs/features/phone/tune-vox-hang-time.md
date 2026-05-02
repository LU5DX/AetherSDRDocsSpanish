# Ajustar el tiempo de retención VOX

El tiempo de retención VOX controla cuánto tiempo permanece el radio en transmisión después de que su voz cae por debajo del umbral de disparo VOX. Ajustarlo evita cortes abruptos al final de las palabras y, al mismo tiempo, evita silencios excesivos antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone requiere una conexión activa con el radio.
- VOX debe estar habilitado. Si VOX no está activo, actívelo primero — consulte [Habilitar VOX y configurar el umbral de disparo](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón **PHNE** de la bandeja en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Localice la fila **Delay:**, directamente debajo de la fila del nivel VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para reducir el tiempo de retención o hacia la derecha para aumentarlo. El valor numérico a la derecha del control se actualiza mientras arrastra.

## Qué hace cada control

| Control                    | Descripción                                                                                                                          | Rango válido |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------|--------------|
| Control deslizante **Delay** | Establece el tiempo de retención VOX — cuánto tiempo permanece el radio en transmisión después de que termina la voz antes de volver a recepción. | 0–100        |

No se guarda ninguna clave de configuración para el control deslizante Delay; el valor se envía directamente al radio.

## Consejos

- Un valor de Delay demasiado bajo hace que el transmisor se corte entre palabras. Aumente el valor hasta que los cortes al final desaparezcan.
- Un valor de Delay demasiado alto mantiene el transmisor activado mucho después de que usted termina de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que el tiempo de retención sea justo el suficiente para cubrir las pausas normales.
- El umbral del nivel VOX y el Delay interactúan: un nivel VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Comportamiento de paso en los puntos de corte del filtro TX

A partir de la v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

Por ejemplo, si el corte bajo está actualmente en 87 Hz:

- Presionar **>** (aumentar) lo mueve a **100 Hz** (el siguiente múltiplo de 50 por encima de 87).
- Presionar **<** (disminuir) lo mueve a **50 Hz** (el siguiente múltiplo de 50 por debajo de 87).

Esto significa que una sola pulsación del botón siempre llega a un límite limpio de 50 Hz independientemente del valor de partida. La rueda del ratón en cada cuadro de giro sigue el mismo comportamiento de ajuste. El radio acepta cualquier valor entero en Hz, por lo que el ajuste es únicamente una conveniencia de la interfaz y no restringe lo que el radio aceptará.

| Control                | Descripción                                                                              | Valor predeterminado | Rango válido                              |
|------------------------|------------------------------------------------------------------------------------------|----------------------|-------------------------------------------|
| **Low Cut < / >**      | Establece la frecuencia de corte bajo del filtro TX; se ajusta al siguiente límite de 50 Hz. | 50 Hz            | 0 a (corte alto − 50), paso 50 Hz         |
| **High Cut < / >**     | Establece la frecuencia de corte alto del filtro TX; se ajusta al siguiente límite de 50 Hz. | 3300 Hz          | (corte bajo + 50) a 10000, paso 50 Hz     |

Ninguno de los controles tiene una clave de configuración guardada; los valores se envían directamente al radio.

## Relacionado

- [Habilitar VOX y configurar el umbral de disparo](enable-vox-and-set-trigger-threshold.md)
- [Descripción general de Phone](overview.md)
