# Acortar o alargar la duración de los spots

Use el control deslizante **Spot Lifetime:** en la configuración de spots (Spot Settings) para controlar cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de desaparecer.

## Antes de empezar

- Los spots deben mostrarse en el panadapter. Si no son visibles, confirme que el interruptor **Spots:** muestra "Enabled" en Spot Settings.
- Abra Spot Settings haciendo clic derecho en la superposición de spots del panadapter.

## Pasos

1. Haga clic derecho en la superposición de spots del panadapter para abrir el cuadro de diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para acortar la duración o hacia la derecha para alargarla. La etiqueta a la derecha del control se actualiza inmediatamente, mostrando el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `15 mins`, `2 hrs`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Función de cada control

| Control                               | Comportamiento                                                                                                                                                                                                                                                                                        | Valor predeterminado |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Interruptor **Spots:**                | Activación general de la visualización de spots DX. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Se guarda en `IsSpotsEnabled`.                                                                                                                       | Enabled |
| Interruptor **Memories:**             | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Se guarda en `IsMemorySpotsEnabled`. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7.             | Disabled |
| Control deslizante **Levels:**        | Define la cantidad de filas verticales para apilar spots. Arrastre para establecer de 1 a 10. El valor predeterminado es 3. Se guarda en `SpotsMaxLevel`. La clave de configuración cambió de `SpotsStackLevels` en v0.9.7.                                                                              | 3       |
| Control deslizante **Position:**      | Define la posición vertical de los spots en el panadapter como porcentaje. Arrastre hacia la izquierda para bajar los spots, hacia la derecha para subirlos. El rango es de 0 a 100. El valor predeterminado es 50. Se guarda en `SpotsStartingHeightPercentage`. La clave de configuración cambió de `SpotsPosition` en v0.9.7. | 50      |
| Control deslizante **Font Size:**     | Define el tamaño del texto del spot en puntos. Arrastre para establecer de 8 a 32. El valor predeterminado es 16. Se guarda en `SpotFontSize`. La clave de configuración cambió de `SpotsFontSize` en v0.9.7.                                                                                           | 16      |
| Control deslizante **Spot Lifetime:** | Define cuánto tiempo permanece un spot en el panadapter antes de desvanecerse. La escala no es lineal: la parte inferior avanza en incrementos de 5 segundos (10 sec – 55 sec), la parte media en incrementos de 5 minutos (5 min – 55 min) y la parte superior en incrementos de 1 hora (1 hr – 24 hrs / 1 day). | 30 min  |
| Interruptor **Override Colors:**      | Fuerza un único color de texto para todos los spots. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Se guarda en `IsSpotsOverrideColorsEnabled`.                                                                                                          | Disabled |
| Selector de color de texto de spot   | Abre un cuadro de diálogo de color para elegir el color del texto cuando Override Colors está habilitado. El valor predeterminado es amarillo brillante (#FFFF00). Se guarda en `SpotsOverrideColor`.                                                                                                   | #FFFF00 |
| Interruptor **Override Background: Enabled** | Dibuja un fondo debajo del texto del spot. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Se guarda en `IsSpotsOverrideBackgroundColorsEnabled`.                                                                                            | Enabled |
| Interruptor **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Se guarda en `IsSpotsOverrideToAutoBackgroundColorEnabled`.                                                                    | Enabled |
| Selector de color de fondo de spot   | Abre un cuadro de diálogo de color para elegir el color de fondo cuando Override Background está habilitado y Auto está deshabilitado. El valor predeterminado es negro (#000000). Se guarda en `SpotsOverrideBgColor`.                                                                                 | #000000 |
| Control deslizante **Background Opacity:** | Define el alfa del fondo del spot. 0 es completamente transparente, 100 es completamente opaco. El valor predeterminado es 48. Se guarda en `SpotsBackgroundOpacity`. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7.                                                           | 48      |
| Interruptor **Spot Lines:**           | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Haga clic para alternar entre habilitado y deshabilitado. El botón siempre muestra "Enabled". Deshabilítelo durante concursos para reducir el desorden visual. Se guarda en `IsSpotsLinesEnabled`. Añadido en v0.9.7 (#2349). | Enabled |
| Botón **Clear All Spots**            | Elimina todos los spots del panadapter de inmediato.                                                                                                                                                                                                                                                     | —       |

**Indicador:**

| Indicador        | Significado                                                |
|------------------|------------------------------------------------------------|
| **Total Spots:** | Muestra la cantidad de spots activos que se están rastreando. |

## Consejos

- El control deslizante usa una escala no lineal. Los movimientos pequeños cerca del extremo izquierdo ajustan la duración en segundos; los movimientos cerca del extremo derecho la ajustan en horas. Posicione el control con cuidado si busca un valor específico.
- La etiqueta mostrada redondea al paso más cercano: los valores por debajo de 60 segundos se muestran como `sec`, los valores por debajo de 1 hora se muestran como `min` o `mins`, y los valores de 1 hora o más se muestran como `hr`, `hrs` o `1 day`.
- Los interruptores siempre muestran "Enabled" independientemente de su estado marcado real. El estado marcado se indica por el color de fondo del botón.
- Si las líneas verticales hacen que el panadapter se vea recargado durante un concurso, haga clic en **Spot Lines:** para establecerlo en Disabled. El cambio tiene efecto de inmediato y se guarda automáticamente.
- Use los interruptores **Override Colors** y **Override Background** para personalizar la legibilidad de los spots sobre diferentes fondos del panadapter.

## Solución de problemas

- **Los spots antiguos aún aparecen después de reducir la duración** — Los spots existentes que llegaron antes del cambio expirarán según la configuración anterior. Los nuevos spots usarán la duración actualizada. Haga clic en **Clear All Spots** para eliminar los spots existentes de inmediato.

## Relacionados

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
