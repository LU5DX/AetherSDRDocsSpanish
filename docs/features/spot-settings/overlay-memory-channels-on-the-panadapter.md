# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 pueden mostrarse como marcadores tipo spot en el panadapter, lo que facilita ver las frecuencias guardadas en contexto con las señales en vivo. Esta página explica cómo activar esa superposición y ajustarla junto con otras configuraciones de spots.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar estos ajustes.
- Abra el diálogo de Configuración de Spots haciendo clic derecho en el panadapter y seleccionando la opción de superposición Spots en el menú contextual.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual y luego abra el diálogo de Configuración de Spots.
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. Por defecto muestra "Disabled". Haga clic una vez para cambiarlo a "Enabled".
4. Los canales de memoria aparecen ahora como superposiciones en el panadapter. Vuelva a hacer clic en la alternancia para regresar a "Disabled" si desea ocultarlos.

## Qué hace cada control

| Control                                 | Qué hace                                                                                                                         | Valor por defecto |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| Alternancia **Spots:**                  | Activación/desactivación general para todas las superposiciones de spots y memorias. Las memorias no se mostrarán si esto está apagado. | Enabled           |
| Alternancia **Memories:**               | Muestra u oculta los marcadores de canales de memoria en el panadapter.                                                           | Disabled          |
| Deslizador **Levels:**                  | Número de filas de apilamiento vertical cuando los spots o memorias se superponen. Rango: 1–10.                                  | 3                 |
| Deslizador **Position:**                | Posición vertical de la banda de superposición en el panadapter, como porcentaje desde arriba. Rango: 0–100.                     | 50                |
| Deslizador **Font Size:**               | Tamaño del texto para etiquetas de spots y memorias. Rango: 8–32.                                                                | 16                |
| Deslizador **Spot Lifetime:**           | Cuánto tiempo permanecen los spots antes de desvanecerse. Escala no lineal: 10 segundos a 24 horas.                              | —                 |
| Alternancia **Override Colors:**        | Fuerza un solo color de texto para todos los spots y memorias en lugar de colores asignados por fuente.                           | Disabled          |
| Selector de color de texto de spot      | Abre un selector de color para elegir el color de texto de anulación. Valor por defecto: `#FFFF00`.                               | `#FFFF00`         |
| Alternancia **Override Background: Enabled** | Dibuja un fondo de color detrás del texto de spots y memorias.                                                              | Enabled           |
| Alternancia **Override Background: Auto**    | Selecciona automáticamente un color de fondo para contraste en lugar de usar el color manual.                               | Enabled           |
| Selector de color de fondo de spot      | Abre un selector de color para el color de fondo manual. Valor por defecto: `#000000`.                                           | `#000000`         |
| Deslizador **Background Opacity:**      | Establece la transparencia del fondo del spot. Rango: 0–100.                                                                     | 48                |
| Alternancia **Spot Lines:**             | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir desorden visual. | Enabled           |
| **Clear All Spots**                     | Elimina todos los spots del panadapter de inmediato. No afecta las memorias.                                                     | —                 |

### Indicador de Spots Totales

La etiqueta **Total Spots:** en la parte inferior del diálogo muestra el recuento de spots activos que se están rastreando actualmente. Se actualiza automáticamente a medida que los spots llegan o expiran.

## Consejos

- Las superposiciones de memoria comparten la misma posición, fuente, apilamiento y configuración de color que los spots de DX. Ajuste **Levels:** y **Position:** para evitar que los marcadores de memoria oculten los picos de señal.
- Si los marcadores de memoria no son visibles incluso después de habilitar **Memories:**, confirme que la alternancia **Spots:** también esté configurada en "Enabled". La alternancia maestra de Spots controla toda la representación de superposiciones.
- La alternancia **Override Background: Auto** está activa por defecto y selecciona automáticamente colores de fondo apropiados para el contraste. Desactívela solo si desea establecer un color de fondo específico con el selector de color de fondo.
- Durante un concurso, desactive **Spot Lines:** para reducir el desorden visual en el panadapter sin ocultar las etiquetas de los spots.
- El diálogo de Configuración de Spots ahora usa los colores del tema activo para su título y la etiqueta de Spots Totales, coincidiendo con la apariencia de otros diálogos de AetherSDR.
- Los botones de alternancia ya no cambian su texto mostrado al alternarse. En su lugar, indican su estado únicamente a través de su apariencia de marcado/desmarcado (coloreados en rojo cuando están deshabilitados, color por defecto cuando están habilitados). La etiqueta junto a cada alternancia permanece constante.

## Solución de problemas

- **Memories: muestra "Enabled" pero no aparecen marcadores en el panadapter** — Verifique que la alternancia **Spots:** esté configurada en "Enabled". La alternancia maestra de spots debe estar activada para que cualquier superposición, incluyendo las memorias, se renderice.
- **Los marcadores de memoria se superponen y son difíciles de leer** — Aumente el valor del deslizador **Levels:** para darle al renderizador más filas de apilamiento, o ajuste **Position:** para mover la superposición a un área menos concurrida del panadapter.
- **El texto del diálogo se ve diferente que antes** — El diálogo de Configuración de Spots ahora aplica el tema actual. No ha cambiado ninguna funcionalidad; solo se actualizó el estilo visual.

## Relacionado

- [Descripción general de Configuración de Spots](overview.md)
- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Agrandar o reducir la fuente de los spots](enlarge-or-shrink-the-spot-font.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Forzar un solo color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
