# Arrastre la línea guía de corte del filtro TX o RX para mover la banda de paso del radio

El lienzo del editor de EQ muestra líneas verticales discontinuas de color amarillo en los bordes de corte actuales del filtro TX o RX del radio. Arrastrar estas líneas mueve la banda de paso del radio en tiempo real, lo que permite ajustar el modelado del EQ a los límites reales del filtro sin salir del editor de EQ.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El editor flotante del lado correspondiente (TX o RX) debe estar abierto. Las líneas guía solo se pueden arrastrar en el lienzo del editor sin marco, no en el tile del applet acoplado.
- Para abrir el editor flotante, haga doble clic en la etapa EQ en el widget CHAIN del lado TX o RX. Consulte [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md).

## Pasos

1. Abra el editor flotante del lado que desea ajustar: haga doble clic en la etapa EQ en el widget CHAIN. La barra de título del editor muestra "Aetherial Parametric EQ — TX" o "Aetherial Parametric EQ — RX".
2. Localice las líneas verticales discontinuas de color amarillo en el lienzo. Hay dos: una en el borde de corte inferior y otra en el borde de corte superior de la banda de paso actual del radio.
3. Mueva el puntero hacia una de las líneas discontinuas amarillas. Cuando el puntero esté suficientemente cerca de la línea, el cursor cambiará a una flecha de cambio de tamaño horizontal.
4. Haga clic y arrastre la línea hacia la izquierda o la derecha. El corte del filtro correspondiente del radio se actualiza en tiempo real mientras arrastra.
5. Suelte para establecer la nueva posición de corte.
6. Repita el procedimiento con la otra línea guía si desea ajustar el borde opuesto de la banda de paso.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Líneas guía de corte del filtro (TX) | Líneas verticales discontinuas de color amarillo en el lienzo del editor TX que marcan los cortes inferior y superior actuales del filtro TX del radio. Arrástrelas en el editor para mover la banda de paso TX del radio en tiempo real. | El cursor cambia a una flecha de cambio de tamaño horizontal al acercarse a una línea. |
| Líneas guía de corte del filtro (RX) | Líneas verticales discontinuas de color amarillo en el lienzo del editor RX que marcan los bordes de la banda de paso RX del slice activo (en el dominio de la frecuencia de audio). Arrástrelas en el editor para mover la banda de paso RX del radio en tiempo real. | El cursor cambia a una flecha de cambio de tamaño horizontal al acercarse a una línea. |

## Consejos

- Las líneas guía son visibles tanto en el tile del applet acoplado como en el editor flotante, pero el arrastre solo está activo en el lienzo del editor flotante.
- Una línea guía no aparece cuando el valor de corte correspondiente es 0 o el radio no lo ha establecido.
- Observe la fila de texto de parámetros en la parte inferior del editor mientras arrastra para confirmar los bordes resultantes de la banda de paso.

## Solución de problemas

- **El cursor no cambia a una flecha de cambio de tamaño horizontal cerca de la línea** — Está situando el puntero sobre el tile del applet acoplado, no sobre el lienzo del editor flotante. Abra el editor flotante haciendo doble clic en la etapa EQ en el widget CHAIN e inténtelo de nuevo.
- **No hay líneas discontinuas amarillas visibles en el lienzo** — El radio no ha reportado valores de corte del filtro, o ambos valores de corte son 0. Verifique que el radio esté conectado y que haya un slice activo.

## Relacionado

- [Abrir el editor sin marco para agregar / eliminar / ajustar bandas en cualquier lado](open-the-frameless-editor-to-add-remove-tune-bands-on-either-side.md)
- [Inspeccionar la curva de EQ TX y el espectro en vivo](inspect-the-tx-eq-curve-and-live-spectrum.md)
- [Inspeccionar la curva de EQ RX y el espectro en vivo](inspect-the-rx-eq-curve-and-live-spectrum.md)
- [Leer los valores exactos de frecuencia / ganancia / Q en la fila de texto de parámetros](read-exact-freq-gain-q-values-in-the-parameter-text-row.md)
