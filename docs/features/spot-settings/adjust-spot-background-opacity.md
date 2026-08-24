# Configuración de spots

Use esta página para controlar cómo se muestran los spots de DX y las memorias en el panadapter. Puede alternar su visibilidad, ajustar la densidad y posición de apilamiento, establecer el tamaño de fuente, controlar cuánto tiempo permanecen los spots en pantalla y sobrescribir sus colores.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho en la superposición de spots sobre el panadapter.

## Qué hace cada control

| Control                              | Predeterminado | Rango válido                        | Clave de configuración                    |
|--------------------------------------|----------------|-------------------------------------|-------------------------------------------|
| **Spots:** alternar                  | Habilitado     | Habilitado / Deshabilitado          | `IsSpotsEnabled`                          |
| **Memories:** alternar               | Deshabilitado  | Habilitado / Deshabilitado          | `IsMemorySpotsEnabled`                    |
| **Kiwi DX:** alternar                | Deshabilitado  | Habilitado / Deshabilitado          | `ShowKiwiDxSpots`                         |
| **Levels:** deslizador               | 3              | 1 – 10                              | `SpotsMaxLevel`                           |
| **Position:** deslizador             | 50             | 0 – 100                             | `SpotsStartingHeightPercentage`           |
| **Font Size:** deslizador            | 16             | 8 – 32                              | `SpotFontSize`                            |
| **Spot Lifetime:** deslizador        | Varía          | 10 seg – 24 horas (pasos no lineales)| `DxClusterSpotLifetimeSec`               |
| **Override Colors:** alternar        | Deshabilitado  | Habilitado / Deshabilitado          | `IsSpotsOverrideColorsEnabled`            |
| Selector de color de texto del spot  | `#FFFF00`      | Cualquier color                     | `SpotsOverrideColor`                      |
| **Override Background:** alternar    | Habilitado     | Habilitado / Deshabilitado          | `IsSpotsOverrideBackgroundColorsEnabled`  |
| **Override Background: Auto** alternar| Habilitado    | Habilitado / Deshabilitado          | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo del spot  | `#000000`      | Cualquier color                     | `SpotsOverrideBgColor`                    |
| **Background Opacity:** deslizador   | 48             | 0 – 100                             | `SpotsBackgroundOpacity`                  |
| **Spot Lines:** alternar             | Habilitado     | Habilitado / Deshabilitado          | `IsSpotsLinesEnabled`                     |
| Botón **Clear All Spots**            | N/A            | N/A                                 | N/A                                       |

## Uso de los conmutadores

Los botones de alternancia muestran el texto "Enabled" o "Disabled" y usan indicadores de color de fondo verde/rojo para mostrar el estado.

1. Haga clic en **Spots:** para mostrar u ocultar los spots de DX en el panadapter.
2. Haga clic en **Memories:** para mostrar u ocultar las superposiciones de canales de memoria.
3. Haga clic en **Kiwi DX:** para superponer los spots de la base de datos comunitaria KiwiSDR DX (balizas, utilidades, señales de tiempo) en la franja del plan de bandas.
4. Haga clic en **Override Colors:** para forzar un único color de texto para todos los spots y luego use el selector de color de texto del spot para elegir el color.
5. Haga clic en **Override Background:** para dibujar un fondo bajo el texto de los spots.
6. Haga clic en **Override Background: Auto** para seleccionar automáticamente el color de fondo con fines de contraste.
7. Haga clic en **Spot Lines:** para dibujar líneas verticales desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir la saturación visual.
8. Haga clic en **Clear All Spots** para borrar todos los spots del panadapter.

## Ajuste de los deslizadores

1. Arrastre el deslizador **Levels:** para establecer cuántas filas de apilamiento vertical pueden usar los spots.
2. Arrastre el deslizador **Position:** para establecer la posición vertical de los spots en el panadapter como porcentaje.
3. Arrastre el deslizador **Font Size:** para establecer el tamaño del texto de los spots en puntos.
4. Arrastre el deslizador **Spot Lifetime:** para establecer cuánto tiempo permanecen los spots antes de desvanecerse. La escala es no lineal, de 10 segundos a 24 horas.
5. Arrastre el deslizador **Background Opacity:** para establecer el nivel alfa del fondo del spot. 0 es totalmente transparente, 100 es totalmente opaco.

## Selección de colores

1. Haga clic en el selector de color de texto del spot para abrir un diálogo de color y elegir el color del texto de los spots.
2. Haga clic en el selector de color de fondo del spot para abrir un diálogo de color y elegir el color de fondo para el texto de los spots.

## Consejos

- Cuando "Override Background: Auto" está habilitado, AetherSDR selecciona automáticamente el color de fondo para el contraste. El deslizador de opacidad aún se aplica sobre ese color seleccionado automáticamente.
- Si desea un color de fondo específico, deshabilite primero "Override Background: Auto" y luego use el selector de color de fondo del spot para elegir un color antes de ajustar la opacidad.
- Una opacidad de fondo de 0 hace que el fondo sea totalmente transparente; el texto del spot seguirá apareciendo pero sin relleno de respaldo.
- Una opacidad de fondo de 100 hace que el fondo sea totalmente opaco. Esto puede ocultar señales débiles debajo de una etiqueta de spot.
- La configuración se guarda automáticamente cuando la cambia. Cierre el diálogo para descartarlo.

## Solución de problemas

- **Mover el deslizador Background Opacity no tiene efecto** — Confirme que el conmutador **Override Background:** muestra "Enabled" con fondo verde. Si muestra "Disabled" con fondo rojo, haga clic en él para habilitar el fondo y luego ajuste el deslizador.
- **Los botones de alternancia muestran el estado incorrecto** — Cada botón de alternancia actualiza su texto automáticamente al hacer clic. Si el texto no coincide con el color de fondo, cierre y vuelva a abrir el diálogo Spot Settings para actualizarlo.

## Relacionado

- [Activar o desactivar spots](turn-spots-on-or-off.md)
- [Forzar un único color de texto para los spots](force-a-single-spot-text-color.md)
- [Elegir un color de fondo personalizado para los spots](pick-a-custom-background-color-for-spots.md)
- [Ajustar la opacidad del fondo de los spots](adjust-spot-background-opacity.md)
