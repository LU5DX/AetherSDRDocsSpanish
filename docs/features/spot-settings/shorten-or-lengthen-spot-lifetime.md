# Acortar o alargar la duración de los puntos

Use el control deslizante **Spot Lifetime:** en Spot Settings para controlar cuánto tiempo permanecen visibles los puntos de DX en el panadapter antes de que expiren.

## Antes de comenzar

- Los puntos deben mostrarse en el panadapter. Si los puntos no son visibles, confirme que el conmutador **Spots:** muestre "Enabled" en Spot Settings.
- Abra Spot Settings haciendo clic derecho en la superposición de puntos en el panadapter.

## Pasos

1. Haga clic derecho en la superposición de puntos en el panadapter para abrir el diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para acortar la duración o hacia la derecha para alargarla. La etiqueta a la derecha del control deslizante se actualiza inmediatamente, mostrando el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `15 mins`, `2 hrs`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control                          | Comportamiento                                                                                                                                                                                                                                                                                                                                             | Predeterminado |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| Conmutador **Spots:**            | Conmutador maestro para la visualización de puntos DX. Haga clic para alternar entre los estados habilitado y deshabilitado. La etiqueta del botón se actualiza a "Enabled" o "Disabled" según el estado actual. Se guarda en `IsSpotsEnabled`.                                                                                                            | Enabled        |
| Conmutador **Memories:**         | Alterna las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre los estados habilitado y deshabilitado. La etiqueta del botón se actualiza a "Enabled" o "Disabled" según el estado actual. Se guarda en `IsMemorySpotsEnabled`. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7.              | Disabled       |
| Control deslizante **Levels:**   | Establece el número de filas de apilamiento vertical para los puntos. Arrastre para establecer de 1 a 10. El valor predeterminado es 3. Se guarda en `SpotsMaxLevel`. La clave de configuración cambió de `SpotsStackLevels` en v0.9.7.                                                                                                                     | 3              |
| Control deslizante **Position:** | Establece la posición vertical de los puntos en el panadapter como un porcentaje. Arrastre hacia la izquierda para mover los puntos hacia abajo, hacia la derecha para moverlos hacia arriba. El rango es de 0 a 100. El valor predeterminado es 50. Se guarda en `SpotsStartingHeightPercentage`. La clave de configuración cambió de `SpotsPosition` en v0.9.7. | 50             |
| Control deslizante **Font Size:**| Establece el tamaño del texto de los puntos en puntos. Arrastre para establecer de 8 a 32. El valor predeterminado es 16. Se guarda en `SpotFontSize`. La clave de configuración cambió de `SpotsFontSize` en v0.9.7.                                                                                                                                       | 16             |
| Control deslizante **Spot Lifetime:** | Establece cuánto tiempo permanece un punto en el panadapter antes de desvanecerse. La escala no es lineal: la parte inferior avanza en incrementos de 5 segundos (10 sec – 55 sec), la parte media en incrementos de 5 minutos (5 min – 55 min) y la parte superior en incrementos de 1 hora (1 hr – 24 hrs / 1 day).                                 | 30 min         |
| Conmutador **Override Colors:**  | Fuerza un solo color de texto para todos los puntos. Haga clic para alternar entre los estados habilitado y deshabilitado. La etiqueta del botón se actualiza a "Enabled" o "Disabled" según el estado actual. Se guarda en `IsSpotsOverrideColorsEnabled`.                                                                                                | Disabled       |
| Selector de color de texto **Spot text color picker** | Abre un diálogo de color para elegir el color del texto cuando Override Colors está habilitado. El valor predeterminado es amarillo brillante (#FFFF00). Se guarda en `SpotsOverrideColor`.                                                                                                                                                               | #FFFF00        |
| Conmutador **Override Background: Enabled** | Dibuja un fondo debajo del texto del punto. Haga clic para alternar entre los estados habilitado y deshabilitado. La etiqueta del botón se actualiza a "Enabled" o "Disabled" según el estado actual. Se guarda en `IsSpotsOverrideBackgroundColorsEnabled`.                                                                                           | Enabled        |
| Conmutador **Override Background: Auto** | Selecciona automáticamente el color de fondo para el contraste. Haga clic para alternar entre los estados habilitado y deshabilitado. El botón siempre muestra "Auto". Se guarda en `IsSpotsOverrideToAutoBackgroundColorEnabled`.                                                                                                                          | Enabled        |
| Selector de color de fondo **Spot background color picker** | Abre un diálogo de color para elegir el color de fondo cuando Override Background está habilitado y Auto está deshabilitado. El valor predeterminado es negro (#000000). Se guarda en `SpotsOverrideBgColor`.                                                                                                                                               | #000000        |
| Control deslizante **Background Opacity:** | Establece el alfa del fondo del punto. 0 es completamente transparente, 100 es completamente opaco. El valor predeterminado es 48. Se guarda en `SpotsBackgroundOpacity`. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7.                                                                                                          | 48             |
| Conmutador **Spot Lines:**      | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de punto. Haga clic para alternar entre los estados habilitado y deshabilitado. La etiqueta del botón se actualiza a "Enabled" o "Disabled" según el estado actual. Desactívelo durante concursos para reducir el desorden visual. Se guarda en `IsSpotsLinesEnabled`. Añadido en v0.9.7 (#2349). | Enabled        |
| Botón **Clear All Spots**       | Limpia todos los puntos del panadapter de inmediato.                                                                                                                                                                                                                                                                                                         | —              |

**Indicador:**

| Indicador         | Significado                                               |
|-------------------|-----------------------------------------------------------|
| **Total Spots:**  | Muestra el recuento de puntos activos que se están rastreando actualmente. |

## Consejos

- El control deslizante utiliza una escala no lineal. Los movimientos pequeños cerca del extremo izquierdo ajustan la duración en segundos; los movimientos cerca del extremo derecho ajustan en horas. Coloque el control deslizante con cuidado cuando busque un valor específico.
- La etiqueta mostrada redondea al paso más cercano: los valores inferiores a 60 segundos se muestran como `sec`, los valores inferiores a 1 hora se muestran como `min` o `mins`, y los valores de 1 hora o más se muestran como `hr`, `hrs` o `1 day`.
- Los botones de conmutación ahora muestran "Enabled" o "Disabled" según su estado actual, lo que hace que el estado sea visible de un vistazo. Anteriormente, los botones siempre mostraban "Enabled" independientemente del estado.
- Si las líneas verticales hacen que el panadapter se sienta desordenado durante un concurso, haga clic en **Spot Lines:** para establecerlo en Disabled. El cambio surte efecto de inmediato y se guarda automáticamente.
- Use los conmutadores **Override Colors** y **Override Background** para personalizar la legibilidad de los puntos en diferentes fondos del panadapter.

## Solución de problemas

- **Los puntos antiguos aún aparecen después de reducir la duración** — Los puntos existentes que llegaron antes del cambio expirarán según la configuración anterior. Los nuevos puntos usarán la duración actualizada. Haga clic en **Clear All Spots** para eliminar los puntos existentes de inmediato.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los puntos](turn-spots-on-or-off.md)
- [Borrar todos los puntos del panadapter](clear-every-spot-from-the-panadapter.md)
