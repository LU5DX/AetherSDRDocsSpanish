# Establezca la frecuencia de corte alto del audio TX

Use el applet Phone para aumentar o disminuir el límite superior de la banda de paso del audio TX. Reducir el corte alto disminuye el ancho de banda transmitido; aumentarlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone requiere una conexión de radio activa.
- La radio debe estar en un modo de voz (SSB, AM, o similar) para que los cambios del filtro TX tengan efecto audible.

## Pasos

1. Si el applet Phone no es visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección del filtro TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte alto en 50 Hz, o haga clic en **<** para disminuirla en 50 Hz. También puede desplazar la rueda del ratón sobre la pantalla de valores para cambiar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control                | Descripción                                               | Predeterminado |
|------------------------|-----------------------------------------------------------|----------------|
| **High Cut `<`**       | Disminuye la frecuencia de corte alto del filtro TX en un paso. | —              |
| **High Cut `>`**       | Aumenta la frecuencia de corte alto del filtro TX en un paso.  | —              |
| Pantalla de valor High Cut | Muestra la frecuencia de corte alto actual en Hz.         | 3300 Hz        |

La frecuencia de corte alto no puede establecerse por debajo de la frecuencia de corte bajo actual más 50 Hz. Por ejemplo, si el corte bajo se establece en 100 Hz, el valor mínimo de corte alto es 150 Hz.

## Consejos

- Cada clic en **<** o **>** mueve la frecuencia exactamente 50 Hz. Para cambios mayores, mantenga presionado el botón del ratón o use la rueda de desplazamiento con movimiento rápido.
- Una banda de paso SSB típica utiliza un corte bajo de 50 Hz y un corte alto de 3300 Hz. Reducir el corte alto a aproximadamente 2700–2800 Hz puede mejorar la inteligibilidad en condiciones ruidosas al eliminar el silbido de alta frecuencia.
- AetherSDR no persiste el ajuste de corte alto en su configuración local — se envía directamente a la radio y se almacena en el perfil activo de la radio.

## Relacionado

- [Establezca la frecuencia de corte bajo del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
