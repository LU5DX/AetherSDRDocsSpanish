# Descripción general de la configuración de Spot

El diálogo Spot Settings controla cómo los spots de DX y los canales de memoria aparecen en el panadapter — incluyendo si se muestran o no, qué tan densamente se apilan, cuánto tiempo persisten y cómo se colorean su texto y fondo. Ábralo desde el menú contextual del panadapter o desde la superposición de spots.

## Antes de comenzar

- No se requiere una conexión de radio para ajustar la configuración de spots; los cambios surten efecto la próxima vez que se muestren spots.
- Los spots deben provenir de un clúster de DX configurado u otra fuente (consulte `Settings > SpotHub...`) antes de que aparezcan spots en el panadapter.

## Cómo funciona

El diálogo Spot Settings es una ventana independiente. Agrupa los controles en tres áreas: visibilidad y diseño, duración y anulación de colores. Todos los cambios se guardan inmediatamente al interactuar con un control. El diálogo sigue automáticamente el tema actual para colores y estilo.

El indicador **Total Spots:** en la parte inferior del diálogo muestra la cantidad de spots activos que se están rastreando actualmente.

Los botones de alternancia muestran texto "Enabled" o "Disabled" que se actualiza según el estado actual, con un fondo de color (verde para habilitado, rojo/ámbar para deshabilitado).

## Qué hace cada control

| Etiqueta                       | Tipo                                                                                                    | Predeterminado                 |
|--------------------------------|---------------------------------------------------------------------------------------------------------|--------------------------------|
| Spots:                         | Botón de alternancia                                                                                    | Enabled                        |
| Memories:                      | Botón de alternancia                                                                                    | Disabled                       |
| Kiwi DX:                       | Botón de alternancia                                                                                    | Disabled                       |
| Levels:                        | Deslizador (1–10)                                                                                       | 3                              |
| Position:                      | Deslizador (0–100)                                                                                      | 50                             |
| Font Size:                     | Deslizador (8–32)                                                                                       | 16                             |
| Spot Lifetime:                 | Deslizador (10 seg – 24 hrs, no lineal)                                                                 | —                              |
| Override Colors:               | Botón de alternancia                                                                                    | Disabled                       |
| Selector de color de texto de spot | Botón pulsador                                                                                      | `#FFFF00`                      |
| Override Background: Enabled   | Botón de alternancia                                                                                    | Enabled                        |
| Override Background: Auto      | Botón de alternancia                                                                                    | Enabled                        |
| Selector de color de fondo de spot | Botón pulsador                                                                                      | `#000000`                      |
| Background Opacity:            | Deslizador (0–100)                                                                                      | 48                             |
| Spot Lines:                    | Botón de alternancia                                                                                    | Enabled                        |
| Clear All Spots                | Botón pulsador                                                                                          | —                              |

### Spots:

Alternancia principal para la visualización de spots de DX. Cuando está en Enabled, los spots de la fuente de clúster de DX configurada se dibujan en el panadapter.

### Memories:

Alterna las superposiciones de canales de memoria en el panadapter. Cuando está en Enabled, los canales de memoria almacenados en su radio aparecen como superposiciones estilo spot para identificar rápidamente actividad en canales guardados.

### Kiwi DX:

Nuevo en v26.8.4. Superpone los spots de la base de datos comunitaria KiwiSDR Community DX (balizas, utilidades, señales de tiempo) en la franja del plan de bandas. El valor predeterminado es Disabled. Esta configuración se guarda en `ShowKiwiDxSpots`.

### Levels:

Filas de apilamiento vertical para spots. El rango es de 1 a 10; el valor predeterminado es 3. Los valores más altos permiten que más spots se apilen verticalmente antes de superponerse.

### Position:

Posición vertical del texto de los spots en el panadapter, expresada como porcentaje. El rango es de 0 a 100; el valor predeterminado es 50 (centro del panadapter).

### Font Size:

Tamaño del texto de los spots en puntos. El rango es de 8 a 32; el valor predeterminado es 16.

### Spot Lifetime:

Cuánto tiempo permanecen los spots en el panadapter antes de desvanecerse. El deslizador no es lineal: los movimientos pequeños en el extremo inferior ajustan la duración en segundos; los movimientos más grandes avanzan a través de minutos y luego horas. El rango es de 10 segundos a 24 horas.

### Override Colors:

Fuerza un único color de texto para todos los spots. Cuando está en Enabled, el color que elija con el selector de color de texto de spot se usa para cada spot, independientemente de la fuente.

### Selector de color de texto de spot

Abre un diálogo de color para elegir el color del texto que se usa cuando Override Colors está en Enabled. El valor predeterminado es `#FFFF00` (amarillo).

### Override Background: Enabled

Dibuja un fondo debajo del texto de los spots. Cuando está en Enabled, el texto de los spots se dibuja con un fondo contrastante para mayor legibilidad.

### Override Background: Auto

Selecciona automáticamente un color de fondo contrastante para el texto de los spots. Cuando está en Enabled, el color seleccionado manualmente se ignora. Cuando está en Disabled, se usa en su lugar el color del selector de color de fondo de spot.

### Selector de color de fondo de spot

Abre un diálogo de color para elegir el color de fondo que se usa cuando Override Background: Enabled está activado y Override Background: Auto está desactivado. El valor predeterminado es `#000000` (negro).

### Background Opacity:

Alfa del fondo de los spots. El rango es de 0 a 100; el valor predeterminado es 48. En 0 el fondo es completamente transparente; en 100 es completamente opaco.

### Spot Lines:

Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos o cuando el panadapter esté congestionado para reducir el desorden visual; las etiquetas de los spots permanecen visibles y solo se ocultan las líneas verticales.

### Clear All Spots

Elimina todos los spots del panadapter inmediatamente.

## Consejos

- Los botones de alternancia muestran texto "Enabled" o "Disabled" que se actualiza según el estado actual, con fondo verde cuando están habilitados y rojo/ámbar cuando están deshabilitados.
- Habilitar Kiwi DX: superpone spots de la base de datos KiwiSDR Community DX, que incluye balizas, utilidades y señales de tiempo que normalmente no están en las fuentes de clúster de DX.
- El deslizador Spot Lifetime no es lineal. Los movimientos pequeños en el extremo inferior del deslizador ajustan la duración en segundos; los movimientos más grandes avanzan a través de minutos y luego horas hasta 24 horas.
- Habilitar Override Background: Auto mientras Override Background: Enabled está activado permite que AetherSDR elija colores de fondo contrastantes automáticamente. Desactive Auto para aplicar su color seleccionado manualmente desde el selector de color de fondo de spot.
- Habilitar Memories: muestra los canales de memoria almacenados en su radio como superposiciones estilo spot, lo cual es útil para identificar rápidamente actividad en canales guardados.
- Desactive Spot Lines: durante concursos o cuando el panadapter esté congestionado para reducir el desorden visual. Las etiquetas de los spots permanecen visibles; solo se ocultan las líneas verticales.
- El diálogo Spot Settings sigue automáticamente el tema actual. Los colores de texto y fondo de los elementos del diálogo se actualizan al cambiar de tema.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Overlay memory channels on the panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Overlay KiwiSDR Community DX spots](overlay-kiwisdr-community-dx-spots.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
