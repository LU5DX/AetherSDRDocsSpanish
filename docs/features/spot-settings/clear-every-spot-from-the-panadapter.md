# Configuración de Spots

Esta página describe el diálogo de Configuración de Spots, una ventana de configuración rápida e independiente para controlar cómo se muestran los spots de DX y las memorias en el panadapter. Incluye botones de activación, controles deslizantes, anulaciones de color y una acción para borrar todo.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- Al menos un panadapter debe estar abierto.

## Abriendo el diálogo de Configuración de Spots

Haga clic derecho en cualquier lugar del panadapter, luego seleccione la opción que abre la superposición de Configuración de Spots.

## Controles

### Spots

| Control | Tipo | Predeterminado | Descripción |
|---------|------|-----------------|-------------|
| **Spots:** | Botón de activación | Habilitado | Activación general para la visualización de spots de DX. |
| **Memories:** | Botón de activación | Deshabilitado | Activa o desactiva las superposiciones de canales de memoria en el panadapter. |

### Apariencia

| Control | Tipo | Predeterminado | Rango | Descripción |
|---------|------|-----------------|-------|-------------|
| **Levels:** | Control deslizante | 3 | 1-10 | Filas de apilamiento vertical para los spots. |
| **Position:** | Control deslizante | 50 | 0-100 | Posición vertical en el panadapter como porcentaje. |
| **Font Size:** | Control deslizante | 16 | 8-32 | Tamaño del texto de los spots en puntos. |
| **Spot Lifetime:** | Control deslizante | Varía | 10 seg – 24 hrs (escala no lineal) | Tiempo que los spots permanecen antes de desvanecerse. El control deslizante usa una escala no lineal de 10 segundos a 24 horas. El valor se almacena en segundos. |

### Anulaciones de Color

| Control | Tipo | Predeterminado | Descripción |
|---------|------|-----------------|-------------|
| **Override Colors:** | Botón de activación | Deshabilitado | Fuerza un solo color de texto para todos los spots. |
| **Selector de color de texto de spot** | Botón pulsador | #FFFF00 | Abre un selector de color para elegir el color del texto del spot. Solo activo cuando **Override Colors:** está Habilitado. |
| **Override Background: Enabled** | Botón de activación | Habilitado | Dibuja un fondo debajo del texto del spot. |
| **Override Background: Auto** | Botón de activación | Habilitado | Selecciona automáticamente el color de fondo para contraste. |
| **Selector de color de fondo de spot** | Botón pulsador | #000000 | Abre un selector de color para el color de fondo del spot. Solo activo cuando **Override Background: Enabled** está Habilitado y **Override Background: Auto** está Deshabilitado. |
| **Background Opacity:** | Control deslizante | 48 | 0-100 | Alfa del fondo del spot (0 = transparente, 100 = opaco). |

### Líneas

| Control | Tipo | Predeterminado | Descripción |
|---------|------|-----------------|-------------|
| **Spot Lines:** | Botón de activación | Habilitado | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Deshabilite durante concursos para reducir el desorden visual. |

## Borrar Todos los Spots

| Control | Tipo | Descripción |
|---------|------|-------------|
| **Clear All Spots** | Botón pulsador | Borra todos los spots mostrados actualmente del panadapter. Los nuevos spots seguirán llegando normalmente. |

## Indicador

| Indicador | Descripción |
|-----------|-------------|
| **Total Spots:** | Muestra el conteo de spots activos actualmente rastreados. |

## Pasos

### Borrar todos los spots del panadapter

1. Abra el diálogo de Configuración de Spots.
2. Haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. Los nuevos spots seguirán llegando y mostrándose normalmente según su configuración actual.

### Activar o desactivar spots

1. Abra el diálogo de Configuración de Spots.
2. Establezca **Spots:** en **Enabled** o **Disabled**.

Cuando se establece en **Enabled**, el botón muestra "Enabled" con un fondo activo. Cuando se establece en **Disabled**, el botón muestra "Enabled" con un fondo atenuado.

### Acortar o alargar la duración de los spots

1. Abra el diálogo de Configuración de Spots.
2. Ajuste el control deslizante **Spot Lifetime:** a la duración deseada.

Los spots permanecerán en el panadapter durante el tiempo configurado antes de desvanecerse.

### Cambiar la densidad y posición vertical de los spots

1. Abra el diálogo de Configuración de Spots.
2. Ajuste **Levels:** para establecer el número de filas de apilamiento vertical.
3. Ajuste **Position:** para establecer la posición vertical en el panadapter.

### Personalizar colores de los spots

1. Abra el diálogo de Configuración de Spots.
2. Establezca **Override Colors:** en **Enabled**.
3. Haga clic en el botón **Selector de color de texto de spot** para elegir un color de texto.
4. Configure el fondo:
   - Establezca **Override Background: Enabled** en **Enabled** para mostrar un fondo.
   - Establezca **Override Background: Auto** en **Enabled** para que el sistema seleccione un color de contraste automáticamente, o establézcalo en **Disabled** y haga clic en el botón **Selector de color de fondo de spot** para elegir un color personalizado.
   - Ajuste **Background Opacity:** para controlar la transparencia.

### Activar o desactivar líneas de spots

1. Abra el diálogo de Configuración de Spots.
2. Establezca **Spot Lines:** en **Enabled** o **Disabled**.

Cuando está deshabilitado, las líneas verticales desde la línea base del espectro hasta cada etiqueta de spot se ocultan, reduciendo el desorden visual.

### Activar o desactivar visualización de memorias

1. Abra el diálogo de Configuración de Spots.
2. Establezca **Memories:** en **Enabled** o **Disabled**.

## Consejos

- **Clear All Spots** no afecta los spots entrantes de su clúster de DX u otras fuentes. Los spots reaparecerán a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del diálogo de Configuración de Spots muestra el conteo de spots activos actualmente rastreados. Después de borrar, este conteo reflejará solo los spots recibidos después de la acción de borrado.
- Para evitar que los spots aparezcan por completo, use el botón de activación **Spots:** para establecerlo en **Disabled**.
- El botón de activación **Spot Lines:** es independiente de **Clear All Spots**. Si el panadapter se siente visualmente ocupado durante un concurso, establezca **Spot Lines:** en **Disabled** antes o después de borrar spots para reducir el desorden sin eliminar las etiquetas de spots.

## Relacionados

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y posición vertical de los spots](change-spot-density-and-vertical-position.md)
