# Configurar la frecuencia de corte bajo del audio de TX

Use el control Low Cut en el applet Phone para elevar el borde inferior del ancho de banda de audio de TX, reduciendo el ruido de fondo, el ruido de respiración o las interferencias de baja frecuencia en su señal transmitida.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone requiere una conexión activa a la radio.
- Asegúrese de que el Panel de applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Haga clic en el botón de la bandeja **PHNE** en la barra lateral derecha para abrir el applet Phone.
2. Localice la sección **Low Cut** en el área de filtro de TX en la parte inferior del applet.
3. Haga clic en **<** para disminuir la frecuencia de corte bajo o en **>** para aumentarla. También puede girar la rueda del ratón sobre la pantalla de valores para ajustar en cualquier dirección.
4. Lea el valor actual en la pantalla numérica entre los dos botones. El valor predeterminado es **50 Hz**.

## Cómo funcionan los botones de paso

Cada clic en **<** o **>** ajusta la frecuencia de corte bajo al múltiplo de 50 Hz más cercano en la dirección elegida, en lugar de sumar o restar un valor fijo de 50 Hz al valor actual. Por ejemplo, si el valor actual es 87 Hz, al hacer clic en **>** se establece en 100 Hz y al hacer clic en **<** se establece en 50 Hz. Si el valor ya es un múltiplo exacto de 50 Hz, los botones lo mueven al siguiente múltiplo en la dirección elegida.

Esto significa que un solo clic siempre aterriza en un límite limpio de 50 Hz independientemente del valor inicial.

## Función de cada control

| Control               | Predeterminado | Rango válido                               |
|-----------------------|----------------|--------------------------------------------|
| **Low Cut** **<**     | —              | Ajusta al siguiente múltiplo inferior de 50 Hz |
| **Low Cut** **>**     | —              | Ajusta al siguiente múltiplo superior de 50 Hz |
| Pantalla de valor Low Cut | 50 Hz      | 0 Hz a (corte alto − 50 Hz), paso 50 Hz    |

## Consejos

- El valor de corte bajo no puede ser mayor que la frecuencia de corte alto actual menos 50 Hz. Si se encuentra cerca de ese límite, reduzca primero el corte alto o auméntelo para crear espacio.
- Para voz en SSB, un corte bajo típico de 100–200 Hz reduce el ruido de baja frecuencia sin afectar notablemente la inteligibilidad de la voz.
- Debido a que los botones se ajustan a múltiplos de 50 Hz, un solo clic desde cualquier valor fuera del límite puede mover la frecuencia en menos de 50 Hz. Este comportamiento es normal.

## Solución de problemas

- **Los botones Low Cut no responden** — Verifique que la radio esté conectada. Los controles de filtro de TX requieren una conexión activa a la radio para enviar los cambios de filtro a la FLEX-8600.

## Relacionados

- [Configurar la frecuencia de corte alto del audio de TX](set-the-tx-audio-high-cut-frequency.md)
- [Descripción general de Phone](overview.md)
- [Habilitar VOX y configurar el umbral de activación](enable-vox-and-set-trigger-threshold.md)
