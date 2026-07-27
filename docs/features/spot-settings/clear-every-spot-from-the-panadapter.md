# Configuración de Spots

Esta página describe el diálogo de Configuración de Spots, una ventana de configuración rápida e independiente para controlar cómo se muestran los spots de DX y las memorias en el panadapter. Incluye botones de activación, deslizadores, anulaciones de color y una acción para borrar todo.

## Antes de comenzar

- AetherSDR debe estar ejecutándose.
- Al menos un panadapter debe estar abierto.

## Abrir el diálogo de Configuración de Spots

Haga clic derecho en cualquier parte del panadapter, luego seleccione la opción que abre la superposición de Configuración de Spots.

## Controles

### Spots

| Control | Tipo | Valor predeterminado | Descripción |
|---------|------|-------------------|-------------|
| **Spots:** | Botón de activación | Activado | Activación principal para la visualización de spots de DX. Cuando está Activado, la etiqueta del botón muestra "Enabled"; cuando está Desactivado, muestra "Disabled". |
| **Memories:** | Botón de activación | Desactivado | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Cuando está Activado, la etiqueta del botón muestra "Enabled"; cuando está Desactivado, muestra "Disabled". |

### Apariencia

| Control | Tipo | Valor predeterminado | Rango | Descripción |
|---------|------|-------------------|-------|-------------|
| **Levels:** | Deslizador | 3 | 1-10 | Filas de apilamiento vertical para los spots. |
| **Position:** | Deslizador | 50 | 0-100 | Posición vertical en el panadapter como porcentaje. |
| **Font Size:** | Deslizador | 16 | 8-32 | Tamaño del texto de los spots en puntos. |
| **Spot Lifetime:** | Deslizador | Varía | 10 seg – 24 horas (pasos no lineales) | Tiempo que los spots permanecen antes de desvanecerse. El deslizador utiliza una escala no lineal desde 10 segundos hasta 24 horas. El valor se almacena en segundos. |

### Anulaciones de color

| Control | Tipo | Valor predeterminado | Descripción |
|---------|------|-------------------|-------------|
| **Override Colors:** | Botón de activación | Desactivado | Fuerza un solo color de texto para todos los spots. Cuando está Activado, la etiqueta del botón muestra "Enabled"; cuando está Desactivado, muestra "Disabled". |
| **Selector de color de texto de spot** | Botón pulsador | #FFFF00 | Abre un selector de color para elegir el color del texto del spot. Solo activo cuando **Override Colors:** está Activado. |
| **Override Background: Enabled** | Botón de activación | Activado | Dibuja un fondo debajo del texto del spot. Cuando está Activado, la etiqueta del botón muestra "Enabled"; cuando está Desactivado, muestra "Disabled". |
| **Override Background: Auto** | Botón de activación | Activado | Selecciona automáticamente el color de fondo para contraste. |
| **Selector de color de fondo de spot** | Botón pulsador | #000000 | Abre un selector de color para el color de fondo del spot. Solo activo cuando **Override Background: Enabled** está Activado y **Override Background: Auto** está Desactivado. |
| **Background Opacity:** | Deslizador | 48 | 0-100 | Alfa del fondo del spot (0 = transparente, 100 = opaco). |

### Líneas

| Control | Tipo | Valor predeterminado | Descripción |
|---------|------|-------------------|-------------|
| **Spot Lines:** | Botón de activación | Activado | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Cuando está Activado, la etiqueta del botón muestra "Enabled"; cuando está Desactivado, muestra "Disabled". |

## Borrar todos los spots

| Control | Tipo | Descripción |
|---------|------|-------------|
| **Clear All Spots** | Botón pulsador | Borra todos los spots mostrados actualmente en el panadapter. Los nuevos spots continuarán llegando con normalidad. |

## Indicador

| Indicador | Descripción |
|-----------|-------------|
| **Total Spots:** | Muestra el recuento de spots activos actualmente en seguimiento. |

## Pasos

### Borrar todos los spots del panadapter

1. Abra el diálogo de Configuración de Spots.
2. Haga clic en **Clear All Spots**.

Todos los spots se eliminan inmediatamente del panadapter. Los nuevos spots continuarán llegando y mostrándose con normalidad según su configuración actual.

### Activar o desactivar spots

1. Abra el diálogo de Configuración de Spots.
2. Configure **Spots:** en **Enabled** o **Disabled**.

Cuando se configura en **Enabled**, el botón muestra "Enabled" con un fondo activo. Cuando se configura en **Disabled**, el botón muestra "Disabled" con un fondo atenuado.

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
   - Configure **Override Background: Auto** en **Enabled** para que el sistema seleccione un color de contraste automáticamente, o configúrelo en **Disabled** y haga clic en el botón **Selector de color de fondo de spot** para elegir un color personalizado.
   - Ajuste **Background Opacity:** para controlar la transparencia.

### Activar o desactivar las líneas de los spots

1. Abra el diálogo de Configuración de Spots.
2. Configure **Spot Lines:** en **Enabled** o **Disabled**.

Cuando está desactivado, las líneas verticales desde la línea base del espectro hasta cada etiqueta de spot se ocultan, reduciendo el desorden visual.

### Activar o desactivar la visualización de memorias

1. Abra el diálogo de Configuración de Spots.
2. Configure **Memories:** en **Enabled** o **Disabled**.

## Consejos

- **Clear All Spots** no afecta los spots entrantes de su clúster de DX u otras fuentes. Los spots volverán a aparecer a medida que se reciban nuevos.
- El indicador **Total Spots:** en la parte inferior del diálogo de Configuración de Spots muestra el recuento de spots activos actualmente en seguimiento. Después de borrar, este recuento reflejará solo los spots recibidos después de la acción de borrado.
- Para evitar que los spots aparezcan por completo, use el botón de activación **Spots:** para configurarlo en **Disabled**.
- El botón de activación **Spot Lines:** es independiente de **Clear All Spots**. Si el panadapter se siente visualmente recargado durante un concurso, configure **Spot Lines:** en **Disabled** antes o después de borrar los spots para reducir el desorden sin eliminar las etiquetas de los spots.
- Cada botón de activación (Spots, Memories, Override Colors, Override Background: Enabled, Spot Lines) ahora muestra dinámicamente "Enabled" o "Disabled" como su etiqueta para indicar claramente el estado actual.

## Relacionados

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
