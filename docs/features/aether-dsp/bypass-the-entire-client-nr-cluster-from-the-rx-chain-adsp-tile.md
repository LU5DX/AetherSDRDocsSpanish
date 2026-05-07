# Omitir todo el clúster de NR del cliente desde el mosaico ADSP de la cadena RX

Desactive rápidamente todos los motores de reducción de ruido del cliente a la vez usando el mosaico ADSP en la tira de la cadena RX, sin abrir el cuadro de diálogo completo de AetherDSP Settings.

## Antes de comenzar

- Asegúrese de que haya una conexión de radio activa y de tener una franja de recepción (slice) RX visible.
- Localice la tira de la cadena RX que muestra los mosaicos de procesamiento (ADSP, NB, etc.).

## Pasos

1. Localice el mosaico **ADSP** en la tira de la cadena RX.
2. Haga doble clic en el mosaico **ADSP**. Se abre el cuadro de diálogo de AetherDSP Settings.
3. En la fila de alternadores de la parte superior, haga clic en cualquier alternador de reducción de ruido activo (iluminado) (NR2, NR4, MNR, DFNR, RN2 o BNR) para desactivarlo.
4. Repita el paso 3 para cada alternador iluminado hasta que todos estén atenuados. Ahora ningún motor NR del cliente está activo.

El mosaico ADSP en la tira de la cadena RX se actualiza para reflejar el estado de omisión.

## Consejos

- Omitir todo el clúster devuelve el audio al flujo de audio bruto de la franja de recepción (slice) proveniente de la radio, sin procesamiento del lado del cliente.
- Los seis alternadores DSP (NR2, NR4, MNR, DFNR, RN2, BNR) también sirven como selectores de pestañas. Al hacer clic en un alternador, se activa ese motor y se selecciona su pestaña; pero solo un motor puede estar activo a la vez (NR2, NR4 y DFNR son mutuamente excluyentes; MNR y BNR pueden apilarse en algunas versiones).
- Para volver a activar rápidamente un solo motor, haga clic en su alternador en la fila.

## Relacionados

- [Resumen de AetherDSP Settings](overview.md)
- [Abrir AetherDSP Settings desde el botón ADSP de la cuadrícula DSP del VFO](open-aetherdsp-settings-from-the-vfo-dsp-grid-adsp-button.md)
- [Elegir la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
