# Seleccionar el carácter Aphex (Even) o Behringer (Odd)

El excitador PUDU ofrece dos sabores armónicos distintos. Use Even para una calidez estilo Aphex con saturación de bajas frecuencias Big Bottom, o Odd para una brillantez estilo Behringer con un compresor de graves de alimentación directa (feed-forward).

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. El applet PUDU permanece oculto hasta que la etapa esté activa. Consulte [Omitir PUDU desde la cadena](bypass-pudu-from-the-chain.md) si el applet no es visible.
- Abra el applet PUDU: localice el subcontenedor PUDU dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante.

## Pasos

1. Localice la fila de alternancia de modo en la parte superior del applet PUDU, directamente debajo del logotipo de PooDoo.
2. Haga clic en "Even" para seleccionar el modelado asimétrico de linaje Aphex — armónicos predominantemente pares, tono más cálido, con saturación de bajas frecuencias Big Bottom. El botón se ilumina en ámbar cuando está seleccionado.
3. Haga clic en "Odd" para seleccionar el modelado simétrico tanh de linaje Behringer — armónicos impares puros, presencia más brillante, con un compresor de graves feed-forward en lugar de saturación de bajas frecuencias.

La selección tiene efecto de inmediato y se guarda en `ClientPuduTxMode`.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de ajuste |
|---------|---------------|----------------------|-----------------|
| Even | Selecciona el modelado asimétrico de linaje Aphex. Armónicos predominantemente pares, carácter más cálido, con saturación de bajas frecuencias Big Bottom. Excluyente con Odd. | — | `ClientPuduTxMode` |
| Odd | Selecciona el modelado simétrico tanh de linaje Behringer. Armónicos impares puros, carácter más brillante, con un compresor de graves feed-forward. Excluyente con Even. | — | `ClientPuduTxMode` |

## Consejos

- El modo Even es adecuado para voces que necesitan calidez y peso en los medios-bajos. El modo Odd es adecuado para voces que ya tienen cuerpo en las bajas frecuencias y necesitan presencia o corte.
- El grupo Poo (Drive, Tune, Mix) moldea el procesador de bajas frecuencias; su comportamiento difiere sutilmente entre los dos modos porque el algoritmo de saturación subyacente cambia. Después de cambiar de modo, verifique su ajuste de Poo / Drive — lo que era apropiado en Even puede ser demasiado agresivo en Odd.
- El logotipo de PooDoo pulsa con mayor brillo a medida que aumenta la señal procesada (wet). Úselo como verificación visual rápida de que el excitador está activo después de cambiar de modo.

## Relacionados

- [Descripción general del excitador PUDU](overview.md)
- [Ajustar el Poo Drive para grosor en bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Omitir PUDU desde la cadena](bypass-pudu-from-the-chain.md)
