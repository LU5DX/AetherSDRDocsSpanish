# Establecer la frecuencia de corte superior del audio TX

Use el applet Phone para subir o bajar el límite superior de la banda de paso del audio TX. Reducir el corte superior disminuye el ancho de banda transmitido; aumentarlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet Phone requiere una conexión activa con el equipo.
- El equipo debe estar en un modo de voz (SSB, AM o similar) para que los cambios en el filtro TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección de filtro TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte superior al siguiente múltiplo de 50 Hz, o haga clic en **<** para disminuirla al siguiente múltiplo inferior de 50 Hz. También puede desplazar la rueda del ratón sobre el indicador de valor para avanzar en cualquier dirección.
4. Lea el valor actual en el indicador numérico entre los botones **<** y **>**.

## Qué hace cada control

| Control                      | Descripción                                                                                              | Predeterminado |
|------------------------------|----------------------------------------------------------------------------------------------------------|----------------|
| **High Cut `<`**             | Disminuye la frecuencia de corte superior del filtro TX al siguiente múltiplo inferior de 50 Hz.        | —              |
| **High Cut `>`**             | Aumenta la frecuencia de corte superior del filtro TX al siguiente múltiplo superior de 50 Hz.          | —              |
| Indicador de valor High Cut  | Muestra la frecuencia de corte superior actual en Hz.                                                    | 3300 Hz        |

La frecuencia de corte superior no puede establecerse por debajo de la frecuencia de corte inferior actual más 50 Hz. Por ejemplo, si el corte inferior está en 100 Hz, el valor mínimo del corte superior es 150 Hz.

## Cómo funciona el avance por pasos

Los botones **<** y **>** ajustan el valor al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el corte superior actual es 3275 Hz, al hacer clic en **>** se establece en 3300 Hz y al hacer clic en **<** se establece en 3250 Hz. Este comportamiento se aplica igualmente a los controles **Low Cut**.

El equipo acepta cualquier valor entero en Hz, por lo que si el valor actual ya es un múltiplo exacto de 50 Hz, el resultado es equivalente a un paso normal de 50 Hz.

## Consejos

- Para cambios mayores, use la rueda del ratón con movimiento rápido en lugar de hacer clic repetidamente en los botones.
- Una banda de paso SSB típica utiliza un corte inferior de 50 Hz y un corte superior de 3300 Hz. Reducir el corte superior a aproximadamente 2700–2800 Hz puede mejorar la inteligibilidad en condiciones de ruido al eliminar el silbido de alta frecuencia.
- La configuración del corte superior no es guardada por los ajustes locales de AetherSDR; se envía directamente al equipo y se almacena en el perfil activo del equipo.

## Relacionados

- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
