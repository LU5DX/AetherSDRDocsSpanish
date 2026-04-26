# Ampliar o reducir el tamaño de fuente de los spots

Use esta página para aumentar o disminuir el tamaño del texto de los spots de DX que se muestran en el panadapter. Una fuente más grande facilita la lectura de los indicativos de un vistazo; una fuente más pequeña reduce el desorden visual cuando hay muchos spots visibles.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El diálogo Spot Settings debe ser accesible desde el menú contextual del panadapter o desde la superposición Spots.

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición Spots) para abrir el menú contextual y, a continuación, seleccione la opción que abre el diálogo Spot Settings.
2. Localice la fila **Font Size:**.
3. Arrastre el control deslizante hacia la izquierda para disminuir el tamaño de fuente o hacia la derecha para aumentarlo. El valor actual se muestra a la derecha del control deslizante.
4. Suelte el control deslizante. El cambio se guarda inmediatamente en `SpotsFontSize` y surte efecto en el panadapter sin necesidad de cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Control deslizante **Font Size:** | Establece el tamaño del texto de las etiquetas de spots en el panadapter. | 16 | 8–32 (puntos) | `SpotsFontSize` |

## Consejos

- El tamaño de fuente predeterminado es 16 pt. Los valores en el extremo inferior del rango (8–10 pt) son útiles cuando el control deslizante **Levels:** está configurado en un valor alto y hay muchas filas apiladas de spots visibles.
- Cambiar el tamaño de fuente no afecta a **Background Opacity:** ni a la posición de los spots. Ajuste **Position:** y **Levels:** por separado si el texto redimensionado se superpone a otros elementos del panadapter.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
- [Acortar o alargar la duración de los spots](shorten-or-lengthen-spot-lifetime.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
