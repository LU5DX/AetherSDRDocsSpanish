# Ajuste del tiempo de retención de VOX

El tiempo de retención de VOX controla cuánto tiempo la radio permanece en transmisión después de que su voz cae por debajo del umbral de activación de VOX. Ajustarlo evita cortes entrecortados de transmisión al final de las palabras, mientras se evita un silencio excesivo antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión de radio activa.
- VOX debe estar habilitado. Si VOX no está activado, habilítelo primero — consulte [Habilitar VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Localice la fila **Delay:**, directamente debajo de la fila del nivel de VOX.
3. Arrastre el deslizador **Delay** hacia la izquierda para acortar el tiempo de retención o hacia la derecha para alargarlo. El valor numérico a la derecha del deslizador se actualiza mientras arrastra.

## Qué hace cada control

| Control          | Descripción                                                                                                    | Rango válido |
|------------------|----------------------------------------------------------------------------------------------------------------|--------------|
| Deslizador **Delay** | Establece el tiempo de retención de VOX — cuánto tiempo la radio permanece en transmisión después de que el habla termina antes de volver a recepción. | 0–100        |

No se persiste ninguna clave de configuración para el deslizador Delay; el valor se envía directamente a la radio.

## Consejos

- Un valor de Delay demasiado bajo hace que el transmisor entre y salga entre palabras. Aumente el valor hasta que se detengan los cortes al final.
- Un valor de Delay demasiado alto mantiene el transmisor activado mucho después de terminar de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que la retención sea lo suficientemente larga para cubrir pausas normales.
- El umbral de nivel de VOX y el Delay interactúan: un nivel de VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Comportamiento de paso de corte del filtro TX

A partir de v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

Por ejemplo, si el corte bajo está actualmente configurado a 87 Hz:

- Presionar **>** (aumentar) lo mueve a **100 Hz** (el siguiente múltiplo de 50 por encima de 87).
- Presionar **<** (disminuir) lo mueve a **50 Hz** (el siguiente múltiplo de 50 por debajo de 87).

Esto significa que una sola pulsación de botón siempre cae en un límite limpio de 50 Hz, independientemente del valor inicial. La rueda del ratón en cada cuadro giratorio sigue el mismo comportamiento de ajuste. La radio acepta cualquier valor entero de Hz, por lo que el ajuste es solo una conveniencia de la interfaz de usuario y no restringe lo que la radio aceptará.

| Control            | Descripción                                                              | Valor predeterminado | Rango válido                        |
|--------------------|--------------------------------------------------------------------------|----------------------|--------------------------------------|
| **Low Cut < / >**  | Establece la frecuencia de corte bajo del filtro TX; ajusta al siguiente límite de 50 Hz. | 50 Hz   | 0 a (corte alto − 50), paso 50 Hz    |
| **High Cut < / >** | Establece la frecuencia de corte alto del filtro TX; ajusta al siguiente límite de 50 Hz.| 3300 Hz | (corte bajo + 50) a 10000, paso 50 Hz |

Ninguno de los controles tiene una clave de configuración persistente; los valores se envían directamente a la radio.

## Formato de valor del deslizador

A partir de v26.5.3, los deslizadores **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor como un porcentaje (por ejemplo, "48%") al arrastrarlos. La etiqueta numérica junto al deslizador continúa mostrando el valor bruto de 0 a 100 sin el signo de porcentaje.

## Relacionados

- [Habilitar VOX y ajustar el umbral de activación](enable-vox-and-set-trigger-threshold.md)
- [Visión general de Phone](overview.md)
