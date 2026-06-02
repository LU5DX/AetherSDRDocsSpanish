# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 se pueden mostrar como marcadores tipo "spot" en el panadapter, lo que facilita ver las frecuencias guardadas en contexto con las señales en vivo. Esta página explica cómo activar esa superposición y ajustarla junto con otras configuraciones de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión con la radio para cambiar estas configuraciones.
- Abra el diálogo Spot Settings haciendo clic derecho en el panadapter y seleccionando la opción Spots overlay en el menú contextual.

## Pasos

1. Haga clic derecho en cualquier lugar del panadapter para abrir el menú contextual y luego abra el diálogo Spot Settings.
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. Por defecto muestra "Disabled". Haga clic una vez para cambiarlo a "Enabled".
4. Los canales de memoria ahora aparecen como superposiciones en el panadapter. Vuelva a hacer clic en la alternancia para regresar a "Disabled" si desea ocultarlos.

## Qué hace cada control

| Control                               | Qué hace                                                                                                                              | Por defecto |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------|
| Alternancia **Spots:**                | Encendido/apagado principal para todas las superposiciones de spots y memorias. Las memorias no aparecerán si esto está desactivado.  | Enabled    |
| Alternancia **Memories:**             | Muestra u oculta los marcadores de canales de memoria en el panadapter.                                                               | Disabled   |
| Deslizador **Levels:**                | Número de filas verticales de apilamiento usadas cuando spots o memorias se superponen. Rango: 1–10.                                  | 3          |
| Deslizador **Position:**              | Posición vertical de la banda de superposición en el panadapter, como porcentaje desde arriba. Rango: 0–100.                          | 50         |
| Deslizador **Font Size:**             | Tamaño del texto para etiquetas de spots y memorias. Rango: 8–32.                                                                     | 16         |
| Deslizador **Spot Lifetime:**         | Cuánto tiempo permanecen los spots antes de desvanecerse. Escala no lineal: 10 segundos a 24 horas.                                   | —          |
| Alternancia **Override Colors:**      | Fuerza un solo color de texto para todos los spots y memorias en lugar de los colores asignados por fuente.                           | Disabled   |
| Selector de color de texto de spot    | Abre un selector de color para elegir el color de texto de anulación. Por defecto: `#FFFF00`.                                         | `#FFFF00`  |
| Alternancia **Override Background: Enabled** | Dibuja un fondo coloreado detrás del texto de spots y memorias.                                                               | Enabled    |
| Alternancia **Override Background: Auto**    | Selecciona automáticamente un color de fondo para contraste en lugar de usar el color manual.                                  | Enabled    |
| Selector de color de fondo de spot    | Abre un selector de color para el color de fondo manual. Por defecto: `#000000`.                                                      | `#000000`  |
| Deslizador **Background Opacity:**    | Establece la transparencia del fondo de los spots. Rango: 0–100.                                                                      | 48         |
| Alternancia **Spot Lines:**           | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. | Enabled |
| **Clear All Spots**                   | Elimina todos los spots del panadapter de inmediato. No afecta las memorias.                                                          | —          |

### Indicador Total Spots

La etiqueta **Total Spots:** en la parte inferior del diálogo muestra el conteo de spots activos que se están rastreando actualmente. Se actualiza automáticamente a medida que llegan o expiran los spots.

## Consejos

- Las superposiciones de memoria comparten la misma configuración de posición, fuente, apilamiento y colores que los spots DX. Ajuste **Levels:** y **Position:** para evitar que los marcadores de memoria oculten los picos de señal.
- Si los marcadores de memoria no son visibles incluso después de habilitar **Memories:**, confirme que la alternancia **Spots:** también esté en "Enabled". La alternancia principal Spots controla toda la representación de superposiciones.
- La alternancia **Override Background: Auto** está activa por defecto y selecciona automáticamente colores de fondo apropiados para el contraste. Desactívela solo si desea establecer un color de fondo específico con el selector de color de fondo.
- Durante un concurso, desactive **Spot Lines:** para reducir el desorden visual en el panadapter sin ocultar las etiquetas de spots.
- El diálogo Spot Settings ahora usa los colores del tema activo para su título y la etiqueta Total Spots, coincidiendo con la apariencia de otros diálogos de AetherSDR.

## Solución de problemas

- **Memories: muestra "Enabled" pero no aparecen marcadores en el panadapter** — Verifique que la alternancia **Spots:** esté en "Enabled". La alternancia principal de spots debe estar activada para que cualquier superposición, incluyendo las memorias, se renderice.
- **Los marcadores de memoria se superponen y son difíciles de leer** — Aumente el valor del deslizador **Levels:** para darle al renderizador más filas de apilamiento, o ajuste **Position:** para mover la superposición a un área menos congestionada del panadapter.
- **El texto del diálogo se ve diferente al anterior** — El diálogo Spot Settings ahora aplica el tema actual. No ha cambiado la funcionalidad; solo se actualizó el estilo visual.

## Relacionados

- [Spot Settings overview](overview.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
