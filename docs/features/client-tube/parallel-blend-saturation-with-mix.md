# Saturación en paralelo mediante Mix

El control Mix mezcla la señal seca (sin procesar) con la señal de tubo completamente saturada. Reducir Mix por debajo del 100 % permite añadir carácter armónico conservando la claridad transitoria y el tono natural de la señal original — una técnica denominada saturación en paralelo.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada en el widget CHAIN. Si no lo está, Mix no produce ningún efecto audible.
- Abra el sub-contenedor TUBE dentro del contenedor padre PooDoo Audio (TXDSP). Si no es visible, haga doble clic en la etapa Tube del widget CHAIN para abrir el editor flotante Tube, o haga clic derecho en la barra de título del sub-contenedor TUBE y elija mostrarlo.

## Pasos

1. Localice el control Mix en la fila de cinco mandos situada en la parte inferior del applet TUBE.
2. Gire Mix para ajustar el balance seco/húmedo. La etiqueta muestra el valor actual como porcentaje (por ejemplo, `50 %`).
   - `100 %` — únicamente la señal saturada.
   - `0 %` — únicamente la señal seca; la saturación queda sin efecto.
   - Los valores intermedios producen una mezcla proporcional.
3. Ajuste Drive, Output o Tone según sea necesario para compensar cambios de nivel o de tono en el punto de mezcla elegido.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---------|----------------------|--------------|-------------------|
| Mix | 100 % | 0 % a 100 % (almacenado como 0.0 a 1.0) | `ClientTubeTxDryWet` |

Mix es una mezcla lineal seco/húmedo. Al 100 % la salida es la señal procesada por el tubo. Al 0 % la salida es la entrada sin modificar. Los valores intermedios suman ambas señales de forma proporcional.

El applet se sincroniza con el editor flotante Tube cada 33 ms, por lo que un valor modificado en cualquiera de los dos lugares se refleja en el otro sin ninguna acción adicional.

## Consejos

- Comience con Drive ajustado moderadamente (6–12 dB) antes de reducir Mix. Un Drive bajo con Mix al 100 % produce menos saturación que un Drive más alto mezclado al 30–50 % de Mix, aunque ambos enfoques suenan diferente — experimente hasta encontrar el carácter deseado.
- Use el control Output para restaurar el nivel sonoro después de reducir Mix, ya que mezclar señal seca suele disminuir el nivel percibido del efecto de saturación.
- La bola de entrada activa sobre la curva de transferencia sigue reflejando la cantidad total de Drive independientemente del ajuste de Mix. Úsela para evaluar el régimen de saturación; use sus oídos para evaluar la mezcla.

## Relacionados

- [Descripción general del Tube Saturator](overview.md)
- [Ajuste Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Omita el tubo desde la cadena](bypass-the-tube-from-the-chain.md)
