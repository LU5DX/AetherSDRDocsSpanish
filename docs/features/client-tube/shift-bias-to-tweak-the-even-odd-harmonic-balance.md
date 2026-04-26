# Ajustar el Bias para equilibrar los armónicos pares e impares

El control **Bias** desplaza el punto de operación del modelo de válvula sobre la curva de transferencia, cambiando la proporción entre armónicos pares e impares en la señal saturada. Úselo para añadir calidez asimétrica o para conseguir un timbre más complejo y rico en armónicos.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada y visible. Si el subcontenedor TUBE está oculto, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.
- El Drive ya debe estar ajustado lo suficientemente alto como para que la curva de transferencia muestre una curvatura visible. Sin cierto nivel de Drive, el Bias tiene poco efecto audible.

## Pasos

1. Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Localice la pantalla de curva de transferencia en la parte superior del applet. La bola de entrada en tiempo real recorre la curva según el nivel de entrada actual.
3. Gire el control **Bias**. Parta del valor predeterminado de 0 % y aumente hacia 100 % mientras observa cómo la curva se dobla asimétricamente.
4. Transmita una señal estable — por ejemplo, hable al micrófono en SSB o emita un tono — y escuche el cambio en el carácter armónico a medida que el Bias aumenta.
5. Detenga el ajuste en el valor donde el equilibrio de armónicos pares/impares se adapte a su gusto. La curva de transferencia y la bola de entrada en tiempo real se actualizan al instante para reflejar el nuevo punto de operación.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Bias | 0 % | 0 % a 100 % | `ClientTubeTxBiasAmount` | Desplaza el punto de operación sobre la curva de transferencia. Los valores más altos incrementan la saturación asimétrica, alterando la mezcla de armónicos pares/impares. |
| Drive | 0.0 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` | Introduce más señal en la etapa de válvula. Mayor Drive hace que los cambios de Bias sean más pronunciados. |
| Curva de transferencia | — | — | — | Dibuja la curva de transferencia de válvula actual. Se actualiza de inmediato al cambiar el Bias. La bola de entrada en tiempo real muestra el régimen de saturación actual. |

## Consejos

- El Bias funciona en conjunto con el Drive. Con un Drive de 0.0 dB, la curva es casi lineal y el Bias tiene un efecto audible mínimo. Aumente primero el Drive hasta que la curva se curve y, después, ajuste el Bias.
- La asimetría de la curva de transferencia se vuelve visible cuando el Bias supera el 0 %. Úsela como referencia visual junto con el resultado auditivo.
- Si el cambio de Bias desplaza notablemente el nivel de salida general, utilice el control **Output** (`ClientTubeTxOutputGainDb`, valor predeterminado 0.0 dB, rango −24.0 a 12.0 dB) para compensarlo.
- Los cambios realizados en el Bias desde el editor flotante de Tube se reflejan en el control del applet en aproximadamente 33 ms, y viceversa.

## Solución de problemas

- **El control Bias no tiene efecto audible** — Es probable que el Drive esté en 0.0 dB o cerca de ese valor. Aumente el Drive hasta que la curva de transferencia muestre una curvatura clara y, luego, ajuste el Bias.
- **El cambio de Bias desaparece al reiniciar AetherSDR** — El valor se persiste en `ClientTubeTxBiasAmount`. Si el ajuste no se está guardando, confirme que la etapa Tube esté completamente habilitada antes de cerrar la aplicación.

## Temas relacionados

- [Descripción general del Tube Saturator](overview.md)
- [Ajustar el Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Mezclar la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
