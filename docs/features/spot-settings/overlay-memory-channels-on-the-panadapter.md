# Superponer canales de memoria en el panadapter

Los canales de memoria almacenados en su FLEX-8600 pueden mostrarse como marcadores tipo spot en el panadapter, lo que facilita visualizar las frecuencias guardadas en contexto con las señales en vivo. Esta página explica cómo activar esa superposición y ajustarla junto con otras configuraciones de spots.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere conexión con la radio para cambiar estos ajustes.
- Abra el diálogo Spot Settings haciendo clic derecho en el panadapter y seleccionando la opción Spots overlay del menú contextual.

## Pasos

1. Haga clic derecho en cualquier parte del panadapter para abrir el menú contextual, luego abra el diálogo Spot Settings.
2. Localice la fila **Memories:**.
3. Haga clic en el botón de alternancia junto a **Memories:**. Por defecto muestra "Disabled". Haga clic una vez para cambiarlo a "Enabled".
4. Los canales de memoria ahora aparecen como superposiciones en el panadapter. Haga clic nuevamente en el botón para volver a "Disabled" si desea ocultarlos.

## Función de cada control

| Control                               | Qué hace                                                                                                                 | Valor predeterminado |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------|----------------------|
| **Spots:** toggle                     | Activación/desactivación general de todas las superposiciones de spots y memorias. Las memorias no aparecerán si está desactivado. | Enabled              |
| **Memories:** toggle                  | Muestra u oculta los marcadores de canales de memoria en el panadapter.                                                  | Disabled             |
| **Levels:** slider                    | Número de filas verticales de apilamiento cuando los spots o memorias se superponen. Rango: 1–10.                         | 3                    |
| **Position:** slider                  | Posición vertical de la banda de superposición en el panadapter, como porcentaje desde arriba. Rango: 0–100.              | 50                   |
| **Font Size:** slider                 | Tamaño del texto para las etiquetas de spots y memorias. Rango: 8–32.                                                    | 16                   |
| **Spot Lifetime:** slider             | Tiempo que los spots permanecen antes de desvanecerse. Escala no lineal: 10 segundos a 24 horas.                         | —                    |
| **Override Colors:** toggle           | Fuerza un solo color de texto para todos los spots y memorias en lugar de los colores asignados por fuente.               | Disabled             |
| Selector de color de texto de spot    | Abre un selector de color para elegir el color de texto de anulación. Valor predeterminado: `#FFFF00`.                   | `#FFFF00`            |
| **Override Background: Enabled** toggle | Dibuja un fondo de color detrás del texto de spots y memorias.                                                          | Enabled              |
| **Override Background: Auto** toggle  | Selecciona automáticamente un color de fondo para contraste en lugar de usar el color manual.                            | Enabled              |
| Selector de color de fondo de spot    | Abre un selector de color para el color de fondo manual. Valor predeterminado: `#000000`.                                | `#000000`            |
| **Background Opacity:** slider        | Establece la transparencia del fondo del spot. Rango: 0–100.                                                             | 48                   |
| **Spot Lines:** toggle                | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir saturación visual. | Enabled |
| **Clear All Spots**                   | Elimina todos los spots del panadapter de inmediato. No afecta las memorias.                                             | —                    |

### Indicador Total Spots

La etiqueta **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando actualmente. Se actualiza automáticamente a medida que los spots llegan o caducan.

## Consejos

- Las superposiciones de memoria comparten la misma posición, fuente, apilamiento y colores que los spots DX. Ajuste **Levels:** y **Position:** para evitar que los marcadores de memoria oculten picos de señal.
- Si los marcadores de memoria no son visibles incluso después de activar **Memories:**, verifique que el botón **Spots:** también esté configurado en "Enabled". El control general Spots gobierna toda la representación de superposiciones.
- **Override Background: Auto** está activo por defecto y selecciona automáticamente colores de fondo apropiados para el contraste. Desactívelo solo si desea establecer un color de fondo específico con el selector de color de fondo.
- Durante un concurso, desactive **Spot Lines:** para reducir la saturación visual en el panadapter sin ocultar las etiquetas de los spots.

## Solución de problemas

- **Memories: muestra "Enabled" pero no aparecen marcadores en el panadapter** — Verifique que el botón **Spots:** esté configurado en "Enabled". El control general de spots debe estar activado para que se represente cualquier superposición, incluidas las memorias.
- **Los marcadores de memoria se superponen y son difíciles de leer** — Aumente el valor del control deslizante **Levels:** para darle al motor de representación más filas de apilamiento, o ajuste **Position:** para mover la superposición a un área menos congestionada del panadapter.

## Relacionado

- [Spot Settings overview](overview.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
