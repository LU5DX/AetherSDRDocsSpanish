# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 pueden mostrarse como marcadores tipo "spot" en el panadapter, lo que facilita ver las frecuencias guardadas en contexto con las señales activas. Esta página explica cómo activar esa superposición y ajustarla junto con otras configuraciones de spots.

## Antes de empezar

- AetherSDR debe estar ejecutándose. No se requiere conexión con la radio para cambiar estos ajustes.
- Abra el diálogo "Spot Settings" haciendo clic derecho en el panadapter y seleccionando la opción de superposición "Spots" en el menú contextual.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual y luego abra el diálogo "Spot Settings".
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. Por defecto muestra "Disabled". Haga clic una vez para cambiarlo a "Enabled".
4. Los canales de memoria aparecerán ahora como superposiciones en el panadapter. Haga clic nuevamente en el botón para volver a "Disabled" si desea ocultarlos.

## Qué hace cada control

| Control                                 | Qué hace                                                                                                                 | Valor predeterminado |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Spots:** toggle                       | Encendido/apagado general para todas las superposiciones de spots y memorias. El texto del botón cambia a "Enabled" o "Disabled" según el estado. Las memorias no aparecerán si esto está apagado. | Enabled |
| **Memories:** toggle                    | Muestra u oculta los marcadores de canales de memoria en el panadapter. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | Disabled |
| **Levels:** slider                      | Número de filas de apilamiento vertical que se usan cuando los spots o memorias se superponen. Rango: 1–10. | 3 |
| **Position:** slider                    | Posición vertical de la banda de superposición en el panadapter, como porcentaje desde la parte superior. Rango: 0–100. | 50 |
| **Font Size:** slider                   | Tamaño del texto para etiquetas de spots y memorias. Rango: 8–32. | 16 |
| **Spot Lifetime:** slider               | Cuánto tiempo permanecen los spots antes de desvanecerse. Escala no lineal: 10 segundos a 24 horas. | — |
| **Override Colors:** toggle             | Fuerza un solo color de texto para todos los spots y memorias en lugar de los colores asignados por fuente. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | Disabled |
| Selector de color de texto de spots     | Abre un selector de color para elegir el color de texto de anulación. Valor predeterminado: `#FFFF00`. | `#FFFF00` |
| **Override Background: Enabled** toggle | Dibuja un fondo de color detrás del texto de spots y memorias. El texto del botón cambia a "Enabled" o "Disabled" según el estado. | Enabled |
| **Override Background: Auto** toggle    | Selecciona automáticamente un color de fondo para contraste en lugar de usar el color manual. | Enabled |
| Selector de color de fondo de spots     | Abre un selector de color para el color de fondo manual. Valor predeterminado: `#000000`. | `#000000` |
| **Background Opacity:** slider          | Establece la transparencia del fondo de los spots. Rango: 0–100. | 48 |
| **Spot Lines:** toggle                  | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. El texto del botón cambia a "Enabled" o "Disabled" según el estado. Desactívelo durante concursos para reducir el desorden visual. | Enabled |
| **Clear All Spots**                     | Elimina todos los spots del panadapter de inmediato. No afecta las memorias. | — |

### Indicador de spots totales

La etiqueta **Total Spots:** en la parte inferior del diálogo muestra el número de spots activos que se están rastreando actualmente. Se actualiza automáticamente a medida que los spots llegan o expiran.

## Consejos

- Las superposiciones de memoria comparten la misma posición, fuente, apilamiento y configuración de colores que los spots de DX. Ajuste **Levels:** y **Position:** para evitar que los marcadores de memoria oculten los picos de señal.
- Si los marcadores de memoria no son visibles incluso después de habilitar **Memories:**, verifique que el botón **Spots:** también esté en "Enabled". El botón general de Spots controla toda la representación de superposiciones.
- El botón **Override Background: Auto** está activo por defecto y selecciona colores de fondo de contraste adecuados automáticamente. Desactívelo solo si desea establecer un color de fondo específico con el selector de color de fondo.
- Durante un concurso, desactive **Spot Lines:** para reducir el desorden visual en el panadapter sin ocultar las etiquetas de los spots.
- El diálogo "Spot Settings" ahora usa los colores del tema activo para su título y la etiqueta "Total Spots", coincidiendo con la apariencia de otros diálogos de AetherSDR.
- Los botones de alternancia ahora actualizan su texto mostrado a "Enabled" o "Disabled" al ser presionados, además de su apariencia de marcado/desmarcado (coloreados en verde cuando están habilitados, rojo cuando están deshabilitados).

## Solución de problemas

- **Memories: muestra "Enabled" pero no aparecen marcadores en el panadapter** — Verifique que el botón **Spots:** esté en "Enabled". El botón general de Spots debe estar activado para que se represente cualquier superposición, incluidas las memorias.
- **Los marcadores de memoria se superponen y son difíciles de leer** — Aumente el valor del control deslizante **Levels:** para darle al motor de representación más filas de apilamiento, o ajuste **Position:** para mover la superposición a un área menos congestionada del panadapter.
- **El texto del diálogo se ve diferente que antes** — El diálogo "Spot Settings" ahora aplica el tema actual. No ha cambiado ninguna funcionalidad; solo se actualizó el estilo visual.

## Relacionado

- [Spot Settings overview](overview.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
