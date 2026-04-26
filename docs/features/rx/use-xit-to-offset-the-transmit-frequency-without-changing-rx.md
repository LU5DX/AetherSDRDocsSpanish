# Usar XIT para desplazar la frecuencia de transmisión sin cambiar la recepción

XIT (Transmit Incremental Tuning) desplaza la frecuencia de transmisión un número fijo de Hz sin modificar la frecuencia de recepción. Esto es útil para trabajar estaciones DX en split o para compensar un transceptor cuya frecuencia de TX necesita un ajuste fino sin resintonizar el VFO.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX requiere una conexión de radio activa.
- Seleccione el slice con el que desea trabajar usando las pestañas de slice (A..H) en el applet RX.

## Pasos

1. Abra el applet RX Controls haciendo clic en el botón **RX** de la bandeja en la barra lateral derecha, si no está visible aún.
2. Desplácese hasta la fila XIT cerca de la parte inferior del applet.
3. Haga clic en **XIT** para habilitar Transmit Incremental Tuning. El botón se ilumina cuando está activo.
4. Ajuste el desplazamiento XIT usando los botones **<** y **>** a cada lado del cuadro de número **XIT offset**, o use la rueda del ratón sobre dicho cuadro. Cada paso mueve la frecuencia de TX 10 Hz.
5. Para restablecer el desplazamiento de TX a cero sin deshabilitar XIT, haga clic en **XIT 0**.
6. Para deshabilitar XIT por completo, haga clic en **XIT** nuevamente para desactivarlo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido / paso | Comportamiento |
|---|---|---|---|
| **XIT** | Desactivado | Activado / Desactivado | Habilita o deshabilita Transmit Incremental Tuning. |
| **XIT offset** | +0 Hz | Pasos de 10 Hz | Establece el desplazamiento de frecuencia de TX relativo al VFO. Ajuste con **<** / **>** o la rueda del ratón. |
| **XIT 0** | — | — | Restablece inmediatamente el desplazamiento XIT a cero. |

## Consejos

- XIT y RIT son independientes. Puede usar ambos simultáneamente: RIT desplaza lo que escucha, XIT desplaza lo que transmite.
- Como cada paso es de 10 Hz, mantenga presionado **<** o **>**, o gire la rueda del ratón de forma continua para alcanzar desplazamientos mayores rápidamente.
- Si cambia de slice usando las pestañas A..H, el estado de XIT es por slice. Verifique que XIT esté configurado correctamente en cada slice que use para transmitir.

## Solución de problemas

- **El botón XIT aparece pero el desplazamiento no tiene efecto en la transmisión** — Confirme que el slice ajustado es el slice de TX activo. Haga clic en el botón **TX (badge)** en el encabezado del applet RX para establecer ese slice como slice de TX y, a continuación, verifique que el desplazamiento XIT no sea cero.
- **El desplazamiento XIT se reinicia inesperadamente** — Compruebe si una aplicación de registro o un controlador CAT está reenviando comandos de frecuencia que sobreescriben el desplazamiento.

## Relacionado

- [Usar RIT para desplazar la frecuencia de recepción ante una estación con deriva](use-rit-to-offset-the-receive-frequency-for-a-drifting-station.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Sintonizar el radio a una frecuencia (escribir MHz en el indicador)](tune-the-radio-to-a-frequency-type-mhz-in-the-readout.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
