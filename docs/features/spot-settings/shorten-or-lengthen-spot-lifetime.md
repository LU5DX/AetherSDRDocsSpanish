# Acortar o alargar la duración de los spots

Use el control deslizante **Spot Lifetime:** en la configuración de spots para controlar cuánto tiempo permanecen visibles los spots de DX en el panadapter antes de que expiren.

## Antes de comenzar

- Los spots deben estar visibles en el panadapter. Si no lo están, verifique que el conmutador **Spots:** muestre "Enabled" en la configuración de spots.
- Abra la configuración de spots haciendo clic derecho en la superposición de spots en el panadapter.

## Pasos

1. Haga clic derecho en la superposición de spots en el panadapter para abrir el diálogo **Spot Settings**.
2. Localice la fila **Spot Lifetime:**.
3. Arrastre el control deslizante hacia la izquierda para acortar la duración o hacia la derecha para alargarla. La etiqueta a la derecha del control se actualiza de inmediato, mostrando el valor actual en segundos, minutos u horas (por ejemplo, `30 secs`, `15 mins`, `2 hrs`).
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente.

## Qué hace cada control

| Control                           | Comportamiento                                                                                                                                                                                                                                                                                                             | Valor predeterminado |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| Conmutador **Spots:**             | Conmutador principal para la visualización de spots DX. Haga clic para alternar entre Enabled y Disabled. Se guarda en `IsSpotsEnabled`.                                                                                                                                                                                   | Enabled              |
| Conmutador **Memories:**          | Activa o desactiva las superposiciones de canales de memoria en el panadapter. Haga clic para alternar entre Enabled y Disabled. Se guarda en `IsMemorySpotsEnabled`. La clave de configuración cambió de `IsMemoriesShownOnPanadapter` en v0.9.7.                                                                            | Disabled             |
| Control deslizante **Levels:**    | Establece el número de filas de apilamiento vertical para los spots. Arrástrelo para ajustar de 1 a 10. El valor predeterminado es 3. Se guarda en `SpotsMaxLevel`. La clave de configuración cambió de `SpotsStackLevels` en v0.9.7.                                                                                        | 3                    |
| Control deslizante **Position:**  | Establece la posición vertical de los spots en el panadapter como un porcentaje. Arrástrelo hacia la izquierda para bajar los spots, hacia la derecha para subirlos. El rango es de 0 a 100. El valor predeterminado es 50. Se guarda en `SpotsStartingHeightPercentage`. La clave cambió de `SpotsPosition` en v0.9.7.       | 50                   |
| Control deslizante **Font Size:** | Establece el tamaño del texto del spot en puntos. Arrástrelo para ajustar de 8 a 32. El valor predeterminado es 16. Se guarda en `SpotFontSize`. La clave de configuración cambió de `SpotsFontSize` en v0.9.7.                                                                                                               | 16                   |
| Control deslizante **Spot Lifetime:** | Establece cuánto tiempo permanece un spot en el panadapter antes de desaparecer. La escala no es lineal: la parte inferior avanza en incrementos de 5 segundos (10 s – 55 s), la parte media en incrementos de 5 minutos (5 min – 55 min) y la parte superior en incrementos de 1 hora (1 h – 24 h / 1 día).                  | 30 min               |
| Conmutador **Override Colors:**   | Fuerza un solo color de texto para todos los spots. Haga clic para alternar entre Enabled y Disabled. Se guarda en `IsSpotsOverrideColorsEnabled`.                                                                                                                                                                         | Disabled              |
| Selector de color de texto del spot | Abre un diálogo de color para elegir el color del texto cuando Override Colors está habilitado. El valor predeterminado es amarillo brillante (#FFFF00). Se guarda en `SpotsOverrideColor`.                                                                                                                                | #FFFF00              |
| Conmutador **Override Background: Enabled** | Dibuja un fondo debajo del texto del spot. Haga clic para alternar entre Enabled y Disabled. Se guarda en `IsSpotsOverrideBackgroundColorsEnabled`.                                                                                                                                | Enabled              |
| Conmutador **Override Background: Auto** | Selecciona automáticamente el color de fondo para contraste. Haga clic para alternar entre Enabled y Disabled. Se guarda en `IsSpotsOverrideToAutoBackgroundColorEnabled`.                                                                                                                       | Enabled              |
| Selector de color de fondo del spot | Abre un diálogo de color para elegir el color de fondo cuando Override Background está habilitado y Auto está deshabilitado. El valor predeterminado es negro (#000000). Se guarda en `SpotsOverrideBgColor`.                                                                                                               | #000000              |
| Control deslizante **Background Opacity:** | Establece el alfa del fondo del spot. 0 es completamente transparente, 100 es completamente opaco. El valor predeterminado es 48. Se guarda en `SpotsBackgroundOpacity`. La clave de configuración cambió de `SpotsOverrideBgOpacity` en v0.9.7.                                                                            | 48                   |
| Conmutador **Spot Lines:**        | Dibuja líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Haga clic para alternar entre Enabled y Disabled. Desactívelo durante concursos para reducir el desorden visual. Se guarda en `IsSpotsLinesEnabled`. Añadido en v0.9.7 (#2349).                                                        | Enabled              |
| Botón **Clear All Spots**        | Elimina todos los spots del panadapter de inmediato.                                                                                                                                                                                                                                                                       | —                    |

**Indicador:**

| Indicador          | Significado                                               |
|--------------------|-----------------------------------------------------------|
| **Total Spots:**   | Muestra la cantidad de spots activos que se están rastreando actualmente. |

## Consejos

- El control deslizante utiliza una escala no lineal. Los movimientos pequeños cerca del extremo izquierdo ajustan la duración en segundos; los movimientos cerca del extremo derecho ajustan en horas. Posicione el control con cuidado cuando busque un valor específico.
- La etiqueta mostrada se redondea al paso más cercano: los valores inferiores a 60 segundos se muestran como `sec`, los valores inferiores a 1 hora se muestran como `min` o `mins`, y los valores de 1 hora o más se muestran como `hr`, `hrs` o `1 day`.
- Si las líneas verticales hacen que el panadapter se sienta desordenado durante un concurso, haga clic en **Spot Lines:** para establecerlo en Disabled. El cambio surte efecto de inmediato y se guarda automáticamente.
- Use los conmutadores **Override Colors** y **Override Background** para personalizar la legibilidad de los spots sobre diferentes fondos del panadapter.

## Solución de problemas

- **Los spots antiguos aún aparecen después de reducir la duración** — Los spots existentes que llegaron antes del cambio expirarán según la configuración anterior. Los spots nuevos usarán la duración actualizada. Haga clic en **Clear All Spots** para eliminar los spots existentes de inmediato.

## Relacionado

- [Descripción general de Spot Settings](overview.md)
- [Activar o desactivar los spots](turn-spots-on-or-off.md)
- [Eliminar todos los spots del panadapter](clear-every-spot-from-the-panadapter.md)
