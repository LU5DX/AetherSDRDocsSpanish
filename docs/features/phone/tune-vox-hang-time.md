# Ajuste del tiempo de retención VOX

El tiempo de retención VOX controla cuánto tiempo permanece la radio en transmisión después de que su voz cae por debajo del umbral de activación VOX. Ajustarlo evita cortes de transmisión entrecortados al final de las palabras, mientras evita un silencio excesivo antes de volver a recepción.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión de radio activa.
- VOX debe estar habilitado. Si VOX no está activado, actívelo primero; consulte [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md).

## Pasos

1. Abra el applet Phone haciendo clic en el botón de la bandeja **PHNE** en la barra lateral derecha. Si el panel del applet está oculto, haga clic en el borde del panel o use `View > Applet Panel` para mostrarlo.
2. Localice la fila **Delay:**, directamente debajo de la fila del nivel VOX.
3. Arrastre el control deslizante **Delay** hacia la izquierda para acortar el tiempo de retención o hacia la derecha para alargarlo. El valor numérico a la derecha del control deslizante se actualiza mientras arrastra.

## Qué hace cada control

| Control          | Descripción                                                                                                    | Rango válido |
|------------------|----------------------------------------------------------------------------------------------------------------|--------------|
| **AM Carrier**   | Establece el nivel de potencia de la portadora AM. Se muestra como porcentaje (ej., "48%") al arrastrarlo.      | 0–100        |
| **VOX**          | Activa o desactiva la transmisión por voz.                                                                     | —            |
| **VOX level**    | Establece el umbral de activación VOX. Se muestra como porcentaje al arrastrarlo.                              | 0–100        |
| **Delay**        | Establece el tiempo de retención VOX: cuánto tiempo permanece la radio en transmisión después de hablar.       | 0–100        |
| **DEXP**         | Activa o desactiva el expansor descendente (puerta de ruido).                                                  | —            |
| **DEXP threshold**| Establece el umbral de la puerta de ruido DEXP.                                                               | 0–100        |
| **Low Cut < / >**| Establece la frecuencia de corte bajo del filtro TX; se ajusta al siguiente límite de 50 Hz.                  | 50 Hz        | 0 a (high-cut − 50), paso 50 Hz |
| **High Cut < / >**| Establece la frecuencia de corte alto del filtro TX; se ajusta al siguiente límite de 50 Hz.                 | 3300 Hz      | (low-cut + 50) a 10000, paso 50 Hz |

## Persistencia de la configuración

- El valor del interruptor **DEXP** y del control deslizante **DEXP threshold** se envían directamente a la radio. Ya no se almacenan en la configuración de AetherSDR.
- Ningún otro control en el applet Phone tiene una clave de configuración persistente; todos los valores se envían directamente a la radio.

## Consejos

- Un valor de Delay demasiado bajo provoca que el transmisor entre y salga entre palabras. Aumente el valor hasta que los cortes de cola se detengan.
- Un valor de Delay demasiado alto mantiene el transmisor activado mucho después de terminar de hablar, bloqueando a otras estaciones. Reduzca el valor hasta que la retención sea lo suficientemente larga para cubrir pausas normales.
- El umbral de nivel VOX y el Delay interactúan: un nivel VOX más sensible (más bajo) puede requerir un Delay más corto, y viceversa.

## Comportamiento de ajuste de frecuencia de corte del filtro TX

A partir de la versión v0.9.5.1, los botones **Low Cut < / >** y **High Cut < / >** ajustan la frecuencia del filtro al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual.

Por ejemplo, si el corte bajo está actualmente en 87 Hz:

- Al presionar **>** (aumentar) se mueve a **100 Hz** (el siguiente múltiplo de 50 por encima de 87).
- Al presionar **<** (disminuir) se mueve a **50 Hz** (el siguiente múltiplo de 50 por debajo de 87).

Esto significa que una sola pulsación siempre termina en un límite limpio de 50 Hz, independientemente del valor inicial. La rueda del ratón en cada control de número sigue el mismo comportamiento de ajuste. La radio acepta cualquier valor entero en Hz, por lo que el ajuste es solo una conveniencia de la interfaz de usuario y no restringe lo que la radio acepta.

| Control               | Descripción                                                               | Valor predeterminado | Rango válido                         |
|-----------------------|---------------------------------------------------------------------------|----------------------|--------------------------------------|
| **Low Cut < / >**     | Establece la frecuencia de corte bajo del filtro TX; se ajusta a 50 Hz.   | 50 Hz                | 0 a (high-cut − 50), paso 50 Hz     |
| **High Cut < / >**    | Establece la frecuencia de corte alto del filtro TX; se ajusta a 50 Hz.   | 3300 Hz              | (low-cut + 50) a 10000, paso 50 Hz  |

Ninguno de los controles tiene una clave de configuración persistente; los valores se envían directamente a la radio.

## Formato del valor del control deslizante

A partir de la versión v26.5.3, los controles deslizantes **AM Carrier**, **VOX level** y **DEXP threshold** muestran su valor como un porcentaje (ej., "48%") al arrastrarlos. La etiqueta numérica junto al control deslizante continúa mostrando el valor bruto de 0 a 100 sin el signo de porcentaje.

## Soporte de temas

A partir de la versión v26.6.1, el applet Phone utiliza colores adaptables al tema en lugar de valores hexadecimales fijos. Los fondos de los controles deslizantes, colores del mango, fondos de los botones y colores del texto siguen el tema cargado actualmente. Los temas se gestionan a través de `View > Theme Manager`.

## Relacionados

- [Enable VOX and set trigger threshold](enable-vox-and-set-trigger-threshold.md)
- [Phone overview](overview.md)
