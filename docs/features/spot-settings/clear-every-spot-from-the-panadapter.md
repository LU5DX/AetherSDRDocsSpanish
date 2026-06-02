# Configuración de Spots

Esta página describe el diálogo de Configuración de Spots, una ventana de configuración independiente y rápida para controlar cómo se muestran los spots DX y las memorias en el panadapter. Incluye interruptores, deslizadores, anulaciones de color y una acción para borrar todo.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Al menos un panadapter debe estar abierto.

## Abriendo el diálogo de Configuración de Spots

Haga clic derecho en cualquier lugar del panadapter, luego seleccione la opción que abre la superposición de Configuración de Spots.

## Controles

### Spots

| Control | Tipo | Predeterminado | Descripción |
|---------|------|----------------|-------------|
| **Spots:** | Botón de alternancia | Habilitado | Interruptor maestro para la visualización de spots DX. |
| **Memories:** | Botón de alternancia | Deshabilitado | Alterna las superposiciones de canales de memoria en el panadapter. |

### Apariencia

| Control | Tipo | Predeterminado | Rango | Descripción |
|---------|------|----------------|-------|-------------|
| **Levels:** | Deslizador | 3 | 1-10 | Filas de apilamiento vertical para los spots. |
| **Position:** | Deslizador | 50 | 0-100 | Posición vertical en el panadapter como porcentaje. |
| **Font Size:** | Deslizador | 16 | 8-32 | Tamaño del texto de los spots en puntos. |
| **Spot Lifetime:** | Deslizador | Varía | 10 seg – 24 hrs (pasos no lineales) | Tiempo que los spots permanecen antes de desvanecerse. El deslizador utiliza una escala no lineal desde 10 segundos hasta 24 horas. El valor se almacena en segundos. |

### Anulaciones de Color

| Control | Tipo | Predeterminado | Descripción |
|---------|------|----------------|-------------|
| **Override Colors:** | Botón de alternancia | Deshabilitado | Fuerza un solo color de texto para todos los spots. |
| **Selector de color de texto de spot** | Botón pulsador | #FFFF00 | Abre un selector de color para elegir el color del texto del spot. Solo está activo cuando **Override Colors:** está Habilitado. |
| **Override Background: Enabled** | Botón de alternancia | Habilitado | Dibuja un fondo debajo del texto del spot. |
| **Override Background: Auto** | Botón de alternancia | Habilitado | Selecciona automáticamente el color de fondo para contraste. |
| **Selector de color de fondo de spot** | Botón pulsador | #000000 | Abre un selector de color para el color de fondo del spot. Solo está activo cuando **Override Background: Enabled** está Habilitado y **Override Background: Auto** está Deshabilitado. |
| **Background Opacity:** | Deslizador | 48 | 0-100 | Alfa del fondo del spot (0 = transparente, 100 = opaco). |

### Líneas

| Control | Tipo | Predeterminado | Descripción |
|---------|------|----------------|-------------|
| **Spot Lines:** | Botón de alternancia | Habilitado | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Deshabilítelo durante concursos para reducir el desorden visual. |

## Borrar Todos los Spots

| Control | Tipo | Descripción |
|---------|------|-------------|
| **Clear All Spots** | Botón pulsador | Borra todos los spots mostrados actualmente del panadapter. Los nuevos spots seguirán llegando con normalidad. |

## Indicador

| Indicador | Descripción |
|-----------|-------------|
| **Total Spots:** | Muestra el recuento de spots activos actualmente rastreados. |

## Pasos

### Borrar cada spot del panadapter

1. Abra el diálogo de Configuración de Spots.
2. Haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. Los nuevos spots seguirán llegando y mostrándose con normalidad según su configuración actual.

### Activar o desactivar spots

1. Abra el diálogo de Configuración de Spots.
2. Configure **Spots:** en **Enabled** o **Disabled**.

### Acortar o alargar la duración de los spots

1. Abra el diálogo de Configuración de Spots.
2. Ajuste el deslizador **Spot Lifetime:** a la duración deseada.

Los spots permanecerán en el panadapter durante el tiempo configurado antes de desvanecerse.

### Cambiar la densidad y la posición vertical de los spots

1. Abra el diálogo de Configuración de Spots.
2. Ajuste **Levels:** para establecer el número de filas de apilamiento vertical.
3. Ajuste **Position:** para establecer la posición vertical en el panadapter.

### Personalizar los colores de los spots

1. Abra el diálogo de Configuración de Spots.
2. Configure **Override Colors:** en **Enabled**.
3. Haga clic en el botón **Selector de color de texto de spot** para elegir un color de texto.
4. Configure el fondo:
   - Configure **Override Background: Enabled** en **Enabled** para mostrar un fondo.
   - Configure **Override Background: Auto** en **Enabled** para que el sistema elija un color de contraste automáticamente, o configúrelo en **Disabled** y haga clic en el botón **Selector de color de fondo de spot** para elegir un color personalizado.
   - Ajuste **Background Opacity:** para controlar la transparencia.

### Alternar líneas de spots

1. Abra el diálogo de Configuración de Spots.
2. Configure **Spot Lines:** en **Enabled** o **Disabled**.

Cuando está deshabilitado, las líneas verticales desde la línea base del espectro hasta cada etiqueta de spot se ocultan, reduciendo el desorden visual.

### Alternar visualización de memorias

1. Abra el diálogo de Configuración de Spots.
2. Configure **Memories:** en **Enabled** o **Disabled**.

## Consejos

- **Clear All Spots** no afecta los spots entrantes de su clúster DX u otras fuentes. Los spots reaparecerán a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del diálogo de Configuración de Spots muestra el recuento de spots activos actualmente rastreados. Después de borrar, este recuento reflejará solo los spots recibidos después de la acción de borrado.
- Para evitar que los spots aparezcan por completo, use el interruptor **Spots:** para configurarlo en **Disabled** en su lugar.
- El interruptor **Spot Lines:** es independiente de **Clear All Spots**. Si el panadapter se siente visualmente recargado durante un concurso, configure **Spot Lines:** en **Disabled** antes o después de borrar spots para reducir el desorden sin eliminar las etiquetas de los spots en sí.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
