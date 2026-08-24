# Superponer las señales de la comunidad KiwiSDR DX en la franja del plan de bandas

Superponga las señales de la base de datos de la comunidad KiwiSDR DX (balizas, servicios, señales horarias) en la franja del plan de bandas del panadapter.

## Antes de comenzar

- AetherSDR conectado a una radio FLEX-8600. Esta función no requiere una conexión de radio para configurarse, pero las señales se muestran en el panadapter.

## Pasos

1. Abra el diálogo Spot Settings desde el menú contextual del panadapter.
2. Busque la fila **Kiwi DX:**.
3. Haga clic en **Disabled** para cambiarlo a **Enabled**.
4. Ajuste **Levels:**, **Position:**, **Font Size:**, **Spot Lifetime:** y las configuraciones de color según lo desee.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Conmutador **Kiwi DX:** | Disabled | Enabled / Disabled | `ShowKiwiDxSpots` |
| Deslizador **Levels:** | 3 | 1–10 | `SpotsMaxLevel` |
| Deslizador **Position:** | 50 | 0–100 | `SpotsStartingHeightPercentage` |
| Deslizador **Font Size:** | 16 | 8–32 | `SpotFontSize` |
| Deslizador **Spot Lifetime:** | 30 min | 10 seg – 24 hrs (pasos no lineales) | `DxClusterSpotLifetimeSec` |
| Conmutador **Override Colors:** | Disabled | Enabled / Disabled | `IsSpotsOverrideColorsEnabled` |
| Selector de color del texto de la señal | #FFFF00 | Cualquier color | `SpotsOverrideColor` |
| Conmutador **Override Background:** | Enabled | Enabled / Disabled | `IsSpotsOverrideBackgroundColorsEnabled` |
| Conmutador **Override Background:** **Auto** | Enabled | Enabled / Disabled | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| Selector de color de fondo de la señal | #000000 | Cualquier color | `SpotsOverrideBgColor` |
| Deslizador **Background Opacity:** | 48 | 0–100 | `SpotsBackgroundOpacity` |
| Conmutador **Spot Lines:** | Enabled | Enabled / Disabled | `IsSpotsLinesEnabled` |

## Consejos

- Las señales Kiwi DX aparecen en la franja del plan de bandas de forma independiente de las señales del DX cluster, por lo que puede ver balizas y servicios aportados por la comunidad junto con su fuente de DX cluster en vivo.
- Establezca **Spot Lines:** en **Disabled** durante los concursos para reducir el desorden visual.

## Relacionado

- [Turn spots on or off](turn-spots-on-or-off.md)
- [Overlay memory channels on the panadapter](overlay-memory-channels-on-the-panadapter.md)
- [Change spot density and vertical position](change-spot-density-and-vertical-position.md)
- [Enlarge or shrink the spot font](enlarge-or-shrink-the-spot-font.md)
- [Shorten or lengthen spot lifetime](shorten-or-lengthen-spot-lifetime.md)
- [Force a single spot text color](force-a-single-spot-text-color.md)
- [Pick a custom background color for spots](pick-a-custom-background-color-for-spots.md)
- [Adjust spot background opacity](adjust-spot-background-opacity.md)
- [Toggle vertical spot lines for contest or casual operating](../dx-cluster/toggle-vertical-spot-lines-for-contest-or-casual-operating.md)
- [Clear every spot from the panadapter](clear-every-spot-from-the-panadapter.md)
- [Spot Settings overview](overview.md)
