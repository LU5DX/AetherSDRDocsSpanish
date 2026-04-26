# Activar una memoria con un solo doble clic

El Navegador de Memorias le permite sintonizar la radio directamente a una memoria almacenada haciendo doble clic en su fila dentro de la tabla de memorias. Esto es más rápido que navegar por menús o volver a escribir una frecuencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Navegador de Memorias requiere una conexión activa con la radio.
- La tabla de memorias debe contener al menos una entrada. Si la radio no tiene memorias cargadas, el panel muestra "No memories are available yet." y no hay nada que activar.

## Pasos

1. Abra el panel lateral del Navegador de Memorias. Aparece junto al panadapter en la ventana principal cuando la navegación de memorias está habilitada.
2. Localice la memoria que desea en la tabla de memorias. La tabla muestra dos columnas: **Frequency** y **Name**. La fila resaltada en un tono más oscuro corresponde a la memoria más cercana a su frecuencia sintonizada actual.
3. Haga doble clic en cualquier fila de la tabla de memorias para activar esa memoria.

Alternativamente, haga clic una vez para seleccionar una fila y luego presione **Enter** para activarla.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| Tabla de memorias | Lista todas las memorias almacenadas ordenadas por frecuencia. Haga doble clic o presione Enter en una fila para activar esa memoria. |
| Fila resaltada | Indica la memoria más cercana a la frecuencia sintonizada actual. Se actualiza automáticamente mientras sintoniza. |
| "No memories are available yet." | Se muestra en lugar de la tabla cuando la radio no tiene memorias cargadas. |

## Consejos

- La tabla ordena las entradas por frecuencia, de modo que si sabe aproximadamente dónde se encuentra una memoria dentro de la banda, puede desplazarse hasta esa área en lugar de buscar por nombre.
- Los nombres y frecuencias largos se truncan con puntos suspensivos si no caben en el espacio disponible. Coloque el cursor sobre una celda para ver el valor completo en un tooltip.

## Relacionado

- [Descripción general del Navegador de Memorias](overview.md)
- [Explorar las memorias almacenadas de la radio](browse-the-radio-s-stored-memories.md)
- [Saltar a la memoria más cercana a la frecuencia actual](jump-to-the-memory-closest-to-the-current-frequency.md)
