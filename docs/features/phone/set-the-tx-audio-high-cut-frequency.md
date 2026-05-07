# Establecer la frecuencia de corte alto del audio de TX

Use el applet Phone para subir o bajar el límite superior de la banda de paso del audio de TX. Reducir el corte alto reduce el ancho de banda transmitido; subirlo permite pasar más contenido de audio de alta frecuencia.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión activa con la radio.
- La radio debe estar en un modo de phone (SSB, AM, o similar) para que los cambios del filtro de TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección del filtro de TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte alto al siguiente múltiplo de 50 Hz, o haga clic en **<** para disminuirla al siguiente múltiplo inferior de 50 Hz. También puede desplazar la rueda del ratón sobre la visualización del valor para incrementar o reducir en cualquier dirección.
4. Lea el valor actual en la visualización numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control                | Descripción                                                                                      | Predeterminado |
|------------------------|--------------------------------------------------------------------------------------------------|----------------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro de TX al siguiente múltiplo inferior de 50 Hz. | —              |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro de TX al siguiente múltiplo superior de 50 Hz.   | —              |
| Visualización del valor High Cut | Muestra la frecuencia de corte alto actual en Hz.                                      | 3300 Hz        |

La frecuencia de corte alto no se puede establecer por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo está establecido en 100 Hz, el valor mínimo del corte alto es 150 Hz.

## Cómo funciona el incremento por pasos

Los botones **<** y **>** fijan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte alto actual es 3275 Hz, hacer clic en **>** lo establece en 3300 Hz y hacer clic en **<** lo establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles **Low Cut**.

La radio acepta cualquier valor entero en Hz, por lo que si el valor actual ya es un múltiplo exacto de 50 Hz, el resultado es el mismo que un paso simple de 50 Hz.

## Consejos

- Para cambios más grandes, use la rueda de desplazamiento con movimiento rápido en lugar de hacer clic repetidamente en los botones.
- Una banda de paso SSB típica usa un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a alrededor de 2700–2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el siseo de alta frecuencia.
- La configuración del corte alto no se conserva en los ajustes locales de AetherSDR — se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionado

- [Establecer la frecuencia de corte bajo del audio de TX](set-the-tx-audio-low-cut-frequency.md)
- [Resumen de Phone](overview.md)
