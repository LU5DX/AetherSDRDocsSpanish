# Saturación en paralelo con mezcla mediante Mix

El control Mix mezcla la señal seca (sin procesar) con la salida completamente saturada (húmeda). Úselo para agregar riqueza armónica mientras conserva el carácter transitorio de la señal original — una técnica conocida como compresión en paralelo o saturación en paralelo.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada mediante el widget CHAIN. Consulte [Omitir el tubo desde la cadena](bypass-the-tube-from-the-chain.md).
- El subcontenedor TUBE debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante Tube, o haga clic derecho en la barra de título del subcontenedor TUBE y seleccione la opción correspondiente para mostrarlo.
2. Localice el control Mix — el knob situado más a la derecha en la fila de cinco knobs en la parte inferior del applet.
3. Gire Mix hacia 0 % para aumentar la proporción de señal seca. Gírelo hacia 100 % para utilizar más señal saturada.
4. Ajuste Mix al valor en el que el audio transmitido suene pleno sin perder la claridad de la señal original. Un punto de partida de 50 % a 70 % es típico para la saturación en paralelo.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---------|----------------------|--------------|--------------------|
| Mix | 100 % | 0 % a 100 % (interno: 0.0 a 1.0) | `ClientTubeTxDryWet` |

Al 100 % la salida es completamente la señal saturada. Al 0 % la etapa de tubo queda efectivamente omitida en cuanto al contenido de audio, aunque permanece activa en la cadena de señal. Los valores intermedios mezclan la señal seca y la húmeda de forma proporcional.

## Consejos

- Los cambios realizados en Mix desde el editor flotante Tube se reflejan en el knob del applet en aproximadamente 33 ms, y viceversa.
- Si la señal mezclada suena más fuerte que la señal seca sola, use el control Output para reducir el nivel. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).
- Para obtener calidez sutil sin distorsión evidente, ajuste Drive al máximo para doblar la curva y luego reduzca Mix a 20 %–40 %.

## Solución de problemas

- **El control Mix no tiene efecto** — Confirme que la etapa Tube esté habilitada en el widget CHAIN. Si la etapa está omitida (bypass), no se produce señal húmeda y el control Mix no puede alterar la salida.
- **La posición del knob no coincide con lo que configuró en el editor flotante** — El applet se sincroniza cada ~33 ms. Espere un momento y el knob se actualizará para reflejar el valor actual.

## Relacionados

- [Omitir el tubo desde la cadena](bypass-the-tube-from-the-chain.md)
- [Ajustar Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Descripción general del Tube Saturator](overview.md)
