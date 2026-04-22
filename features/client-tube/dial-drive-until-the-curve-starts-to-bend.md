# Drive: gire el control hasta que la curva empiece a doblarse

Drive controla con qué intensidad se empuja la señal hacia el modelo de válvula. Al aumentarlo, la curva de transferencia se dobla visiblemente y se aleja de una diagonal recta, que es el punto en que comienza la saturación armónica.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada. Si el subcontenedor TUBE no es visible, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.
- Abra el subcontenedor TUBE dentro del contenedor padre PooDoo Audio (TXDSP) para que la curva de transferencia y los mandos sean visibles.

## Pasos

1. Observe el display de la curva de transferencia en la parte superior del applet TUBE. Con Drive en 0.0 dB, la curva es una línea diagonal casi recta.
2. Gire el mando Drive en sentido horario. La etiqueta del mando se actualiza en tiempo real y muestra el valor como `X.X dB`.
3. Observe la curva. A medida que Drive aumenta, los hombros de la curva comienzan a aplanarse y doblarse. Detenga el ajuste cuando el doblez alcance la cantidad de saturación deseada.
4. Hable al micrófono (o genere un tono). La bola de entrada en vivo se desplaza a lo largo de la curva, mostrando el punto en que opera su señal sobre la función de transferencia. Procure que la bola permanezca en la región doblada durante los picos típicos.
5. Si el nivel general ha cambiado notablemente, use el mando Output para compensarlo. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistente | Comportamiento |
|---|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | Empuja más señal hacia la etapa de válvula. Valores más altos producen mayor doblez de la curva y más contenido armónico. |
| Curva de transferencia | — | — | — | Dibuja la curva de transferencia actual de la válvula. Se actualiza de inmediato al cambiar Drive, Bias o el modelo. |
| Bola de entrada en vivo | — | — | — | Un punto que se mueve a lo largo de la curva de transferencia según el nivel de entrada actual suavizado, indicando el régimen de saturación activo. |

## Consejos

- La bola se suaviza con una constante de tiempo corta, por lo que las transitorias breves no la desplazarán hacia los extremos. Juzgue la región de operación observando la bola durante voz sostenida o tono continuo, no en picos instantáneos.
- Drive interactúa con Bias: una vez que tenga el doblez de curva deseado, ajuste Bias para modificar la mezcla armónica sin cambiar la cantidad total de doblez. Consulte [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md).
- Si abre el editor flotante de Tube al mismo tiempo, ambas vistas permanecen sincronizadas. Los cambios realizados en cualquiera de los dos lugares se reflejan en el otro en aproximadamente 33 ms.

## Solución de problemas

- **La curva de transferencia no se dobla sin importar qué tan alto se ajuste Drive** — confirme que la etapa Tube esté habilitada. Una etapa deshabilitada muestra el applet pero no procesa audio, por lo que la curva puede no responder como se espera. Use el widget CHAIN para verificar que la etapa esté activa. Consulte [Omitir la válvula desde la cadena](bypass-the-tube-from-the-chain.md).
- **La bola de entrada en vivo no se mueve** — la bola requiere un motor de audio activo y una señal en vivo. Confirme que la radio esté conectada y que el audio fluya hacia la cadena TX DSP.
- **La posición del mando no coincide con el valor mostrado en el editor flotante** — el applet se sincroniza cada 33 ms. Si los valores aparecen momentáneamente desfasados, espere un ciclo de sincronización o mueva cualquiera de los mandos ligeramente para forzar una actualización.

## Relacionados

- [Descripción general del Tube Saturator](overview.md)
- [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Mezclar la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
