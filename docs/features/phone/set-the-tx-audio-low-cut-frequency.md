# Establecer la frecuencia de corte inferior del audio TX

Use el control Low Cut del applet Phone para elevar el límite inferior de la banda de paso del audio TX y eliminar ruido de fondo, ruido de respiración o interferencia de baja frecuencia de la señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión de radio activa.
- Asegúrese de que el panel de applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón **PHNE** de la barra lateral derecha para abrir el applet Phone.
2. Ubique la sección **Low Cut** en el área de filtro TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte inferior o en **>** para aumentarla. También puede desplazar la rueda del mouse sobre el indicador de valor para avanzar en cualquier dirección.
4. Lea el valor actual en el indicador numérico entre los dos botones. El valor predeterminado es **50 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** desplaza la frecuencia de corte inferior al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo desplazan al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre cae en un límite limpio de 50 Hz independientemente del valor de partida.

## Qué hace cada control

| Control               | Predeterminado | Rango válido                                      |
|-----------------------|----------------|---------------------------------------------------|
| **Low Cut** **<**     | —              | Desplaza hacia abajo al siguiente múltiplo de 50 Hz inferior |
| **Low Cut** **>**     | —              | Desplaza hacia arriba al siguiente múltiplo de 50 Hz superior |
| Indicador de valor Low Cut | 50 Hz     | 0 Hz a (corte superior − 50 Hz), paso de 50 Hz   |

## Sugerencias

- El valor de corte inferior no puede establecerse por encima de la frecuencia de corte superior actual menos 50 Hz. Si está cerca de ese límite, primero reduzca el corte superior o auméntelo para crear margen.
- Para voz en SSB, un corte inferior típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Dado que los botones se desplazan a múltiplos de 50 Hz, hacer clic una vez desde cualquier valor fuera de ese límite puede mover la frecuencia menos de 50 Hz. Este es el comportamiento esperado.

## Resolución de problemas

- **Los botones Low Cut no responden** — Confirme que la radio esté conectada. Los controles de filtro TX requieren una conexión de radio activa para enviar los cambios de filtro al FLEX-8600.

## Relacionado

- [Establecer la frecuencia de corte superior del audio TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Activar VOX y establecer el umbral de activación](enable-vox-and-set-trigger-threshold.md)
