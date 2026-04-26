# Acortar o alargar la vida útil de los spots

Use esta página para controlar cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de desvanecerse. Una vida útil más corta mantiene la pantalla despejada; una más larga le permite rastrear spots durante sesiones de operación prolongadas.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para cambiar esta configuración.
- El diálogo **Spot Settings** debe estar accesible desde el menú contextual del panadapter o desde la superposición Spots.

## Pasos

1. Haga clic derecho en el panadapter (o en la superposición Spots) para abrir el menú contextual y seleccione la opción que abre **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para acortar la vida útil o hacia la derecha para alargarla. La etiqueta a la derecha del control se actualiza de inmediato para mostrar el valor actual en segundos, minutos u horas.
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Control deslizante **Spot Lifetime:** | Establece cuánto tiempo permanecen los spots en el panadapter antes de desvanecerse. El control utiliza una escala no lineal: las posiciones a la izquierda cubren de 10 a 55 segundos (en pasos de 5 segundos), el centro cubre de 5 a 55 minutos (en pasos de 5 minutos) y la derecha cubre de 1 a 24 horas (en pasos de 1 hora). La etiqueta muestra el valor actual formateado en segundos (`sec`), minutos (`mins`) u horas (`hrs`), con 24 horas mostradas como `1 day`. | 30 min | 10 sec – 24 hr | `SpotsLifetime` (`DxClusterSpotLifetimeSec` internamente, en segundos) |

## Consejos

- El control deslizante se ajusta a pasos predefinidos, no a valores arbitrarios. La resolución más fina es de 5 segundos en el extremo inferior y de 1 hora en el extremo superior.
- Si actualizó desde una versión anterior de AetherSDR, la aplicación migra automáticamente su antiguo valor de vida útil por minuto a la nueva clave por segundo en el primer inicio.
- Establecer una vida útil muy larga (varias horas) puede resultar en un panadapter saturado en bandas con mucha actividad. Use el botón **Clear All Spots** en el mismo diálogo para eliminar los spots acumulados de inmediato.

## Solución de problemas

- **Los spots desaparecen antes de la vida útil configurada** — Verifique que **Spots:** esté establecido en **Enabled** en el mismo diálogo. Si la configuración `IsSpotsEnabled` se desactiva y se vuelve a activar, los spots ya mostrados pueden reiniciar su contador de vida útil.
- **El control deslizante salta más allá del valor deseado** — La escala es no lineal. Muévase lentamente cerca de los puntos de transición (alrededor de 55 segundos y 55 minutos) donde cambia el tamaño del paso.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
- [Cambiar la densidad y la posición vertical de los spots](change-spot-density-and-vertical-position.md)
