# Elija un color de fondo personalizado para las estaciones

Establezca un color de fondo específico que aparezca detrás de las etiquetas de estaciones en el panadapter. Úselo cuando el contraste de color automático no sea adecuado para su pantalla o sus condiciones de operación.

## Antes de comenzar

- Abra el diálogo Spot Settings haciendo clic derecho en la superposición de estaciones en un panadapter.
- Confirme que el botón "Override Background: Enabled" muestre "Enabled". El selector de color de fondo no tiene efecto cuando el fondo está deshabilitado.
- Desactive "Override Background: Auto" si desea que su color elegido tenga efecto. Cuando "Auto" está activo, AetherSDR selecciona el color de fondo automáticamente e ignora el selector de color manual.

## Pasos

1. Haga clic derecho en la superposición de estaciones en el panadapter y abra Spot Settings.
2. Localice la fila **Override Background:**.
3. Si el botón "Enabled" muestra "Disabled", haga clic en él para que muestre "Enabled". Esto se guarda en `IsSpotsOverrideBackgroundColorsEnabled`.
4. Si el botón "Auto" muestra "Enabled", haga clic en él para que muestre "Disabled". Esto se guarda en `IsSpotsOverrideToAutoBackgroundColorEnabled`. Mientras "Auto" esté activo, el selector de color manual será ignorado.
5. Haga clic en el pequeño botón de muestra de color a la derecha de "Auto". Esto abre el diálogo de color del sistema titulado "Spot Background Color".
6. Seleccione el color deseado y confirme la selección.
7. La muestra se actualiza inmediatamente y el fondo del panadapter detrás de las etiquetas de estaciones cambia al color elegido. El valor se guarda en `SpotsOverrideBgColor`.

## Qué hace cada control

| Etiqueta                      | Tipo                                                                                                   | Valor predeterminado          |
|-------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------|
| Spots:                        | Botón de alternancia                                                                                   | Enabled                       |
| Memories:                     | Botón de alternancia                                                                                   | Disabled                      |
| Kiwi DX:                      | Botón de alternancia                                                                                   | Disabled                      |
| Levels:                       | Control deslizante (1–10)                                                                              | 3                             |
| Position:                     | Control deslizante (0–100)                                                                             | 50                            |
| Font Size:                    | Control deslizante (8–32)                                                                              | 16                            |
| Spot Lifetime:                | Control deslizante (pasos no lineales, 10 seg – 24 h)                                                  | (varía)                       |
| Override Colors:              | Botón de alternancia                                                                                   | Disabled                      |
| Selector de color de texto de estaciones | Botón pulsador (muestra de color)                                                            | `#FFFF00`                     |
| Override Background: Enabled  | Botón de alternancia                                                                                   | Enabled                       |
| Override Background: Auto     | Botón de alternancia                                                                                   | Enabled                       |
| Selector de color de fondo de estaciones | Botón pulsador (muestra de color)                                                            | `#000000`                     |
| Background Opacity:           | Control deslizante (0–100)                                                                             | 48                            |
| Spot Lines:                   | Botón de alternancia                                                                                   | Enabled                       |
| Clear All Spots               | Botón pulsador                                                                                         | —                             |

## Indicadores

| Etiqueta   | Significado                                   |
|------------|-----------------------------------------------|
| Total Spots: | Muestra la cantidad de estaciones activas que se están rastreando actualmente. |

## Consejos

- **Kiwi DX:** el valor predeterminado es "Disabled". Actívelo para superponer las estaciones de la base de datos comunitaria de KiwiSDR DX (balizas, servicios, señales de tiempo) en la franja del plan de bandas. El ajuste se guarda en `ShowKiwiDxSpots`. Este control se agregó en v26.8.4.
- Establecer la opacidad en 0 hace que el fondo sea completamente transparente, independientemente del color elegido. Si el fondo desaparece después de elegir un color, revise el control deslizante "Background Opacity:".
- "Override Background: Auto" tiene el valor predeterminado "Enabled", por lo que un diálogo recién abierto ignorará cualquier color manual hasta que desactive "Auto".
- "Spot Lines:" tiene el valor predeterminado "Enabled". Si las líneas verticales desde la línea base del espectro hasta las etiquetas de estaciones agregan desorden durante un concurso, haga clic en el botón de alternancia para que muestre "Disabled". Esto se guarda en `IsSpotsLinesEnabled`.

## Solución de problemas

- **El selector de color no tiene efecto visible en el panadapter** — Confirme que "Override Background: Enabled" muestre "Enabled" y que "Override Background: Auto" muestre "Disabled". Ambas condiciones deben cumplirse para que se muestre un color de fondo manual.
- **El fondo es invisible a pesar de los estados correctos de los botones** — Revise el control deslizante "Background Opacity:". Si está en 0, el fondo es completamente transparente. Consulte [Adjust spot background opacity](adjust-spot-background-opacity.md).
- **Las estaciones Kiwi DX no aparecen** — Confirme que "Kiwi DX:" muestre "Enabled". El botón de alternancia se guarda en `ShowKiwiDxSpots`. Este control se agregó en v26.8.4; si está ejecutando una versión anterior, el ajuste no está disponible.
- **Las líneas de estaciones no son visibles** — Confirme que "Spot Lines:" muestre "Enabled". El botón de alternancia se guarda en `IsSpotsLinesEnabled`. Este control se agregó en v0.9.7; si está ejecutando una versión anterior, el ajuste no está disponible.

## Relacionados

- [Adjust spot background opacity](adjust-spot-background-opacity.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Turn spots on or off](turn-spots-on-or-off.md)
- [Spot Settings overview](overview.md)
