# Establecer la frecuencia de corte superior del audio TX

Use el applet Phone para subir o bajar el límite superior de la banda de paso del audio TX. Reducir el corte superior disminuye el ancho de banda transmitido; subirlo permite pasar más contenido de audio de alta frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone requiere una conexión activa al radio.
- El radio debe estar en un modo de voz (SSB, AM o similar) para que los cambios en el filtro TX tengan efecto audible.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Localice la columna **High Cut** en el lado derecho de la sección de filtro TX, debajo de la fila DEXP.
3. Haga clic en **>** para aumentar la frecuencia de corte superior en 50 Hz, o haga clic en **<** para disminuirla en 50 Hz. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica ubicada entre los botones **<** y **>**.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido |
|---|---|---|---|
| **High Cut `<`** | Disminuye la frecuencia de corte superior del filtro TX en un paso. | — | — |
| **High Cut `>`** | Aumenta la frecuencia de corte superior del filtro TX en un paso. | — | — |
| Pantalla de valor High Cut | Muestra la frecuencia de corte superior actual en Hz. | 3300 Hz | (corte inferior + 50) a 10000 Hz, en pasos de 50 Hz |

La frecuencia de corte superior no puede establecerse por debajo de la frecuencia de corte inferior actual más 50 Hz. Por ejemplo, si el corte inferior está en 100 Hz, el valor mínimo del corte superior es 150 Hz.

## Consejos

- Cada clic en **<** o **>** mueve la frecuencia exactamente 50 Hz. Para cambios mayores, mantenga presionado el botón del ratón o use la rueda de desplazamiento con movimiento rápido.
- Una banda de paso SSB típica utiliza un corte inferior de 50 Hz y un corte superior de 3300 Hz. Reducir el corte superior a alrededor de 2700–2800 Hz puede mejorar la inteligibilidad en condiciones de ruido al eliminar el siseo de alta frecuencia.
- La configuración de corte superior no es guardada por la configuración local de AetherSDR — se envía directamente al radio y se almacena en el perfil activo del radio.

## Temas relacionados

- [Establecer la frecuencia de corte inferior del audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
