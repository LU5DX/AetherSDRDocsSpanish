# Configurar la frecuencia de corte alto de audio TX

Use el applet Phone para subir o bajar el límite superior de la banda de paso de audio TX. Reducir el corte alto elimina contenido innecesario de alta frecuencia; ampliarlo puede mejorar la claridad de audio en modos de mayor ancho de banda.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone se deshabilita sin una conexión de radio.
- La radio debe estar en un modo de voz (SSB, AM o similar) para que los cambios en el filtro TX surtan efecto en el aire.

## Pasos

1. Si el applet Phone no está visible, haga clic en el botón de bandeja **PHNE** en la barra lateral derecha para mostrarlo.
2. Ubique la columna **High Cut** en el lado derecho de la sección de filtro TX, en la parte inferior del applet Phone.
3. Haga clic en **>** para aumentar la frecuencia de corte alto en 50 Hz, o en **<** para disminuirla en 50 Hz. También puede desplazar la rueda del ratón sobre la pantalla de valor para avanzar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los botones **<** y **>**.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **High Cut `<`** | — | Disminuye en pasos de 50 Hz | Reduce la frecuencia de corte alto del filtro TX en 50 Hz por clic. |
| **High Cut `>`** | — | Aumenta en pasos de 50 Hz | Incrementa la frecuencia de corte alto del filtro TX en 50 Hz por clic. |
| Pantalla de valor High Cut | 3300 Hz | (corte bajo + 50) a 10000 Hz, paso de 50 Hz | Muestra la frecuencia de corte alto actual en Hz. También acepta entrada mediante la rueda del ratón. |

La frecuencia de corte alto no puede establecerse por debajo de la frecuencia de corte bajo actual más 50 Hz, ni puede superar los 10000 Hz.

## Consejos

- Para voz SSB estándar, un corte alto de 2800–3300 Hz es lo habitual. Los valores superiores a 3300 Hz permiten mayor ancho de banda de audio, pero aumentan el espectro ocupado.
- Ajuste primero **Low Cut** si desea una banda de paso estrecha o con forma determinada, y luego configure **High Cut** para mantener la separación mínima de 50 Hz.

## Relacionado

- [Configurar la frecuencia de corte bajo de audio TX](set-the-tx-audio-low-cut-frequency.md)
- [Descripción general de Phone](overview.md)
