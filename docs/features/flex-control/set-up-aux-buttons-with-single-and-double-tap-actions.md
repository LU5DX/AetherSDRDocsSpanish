# Configurar botones auxiliares con acciones de un solo toque y doble toque

Configure los cinco botones auxiliares en el diálogo AetherControl / FlexControl para que cada botón pueda activar una acción diferente con un solo toque o con un doble toque.

## Antes de comenzar

- Abra el diálogo AetherControl: `Settings > AetherControl...`
- Familiarícese con la [descripción general](overview.md) del controlador

## Pasos

1. Haga clic en uno de los cinco botones auxiliares numerados para seleccionarlo. El botón seleccionado se resalta en verde.
2. En el cuadro combinado de un solo toque debajo de los botones auxiliares, seleccione una acción para un solo toque.
3. En el cuadro combinado de doble toque debajo de los botones auxiliares, seleccione una acción para un doble toque.
4. Repita para cada botón auxiliar que desee configurar.

## Qué hace cada control

| Control | Descripción | Claves de configuración |
|---|---|---|
| Botones auxiliares (1–5) | Selecciona un botón auxiliar para configurar. El botón activo se muestra con un punto verde. | Ninguna |
| Cuadro combinado de un solo toque aux. | Asigna una acción a un solo toque del botón auxiliar seleccionado. | `FlexControlBtn1Action0` – `FlexControlBtn4Action0` |
| Cuadro combinado de doble toque aux. | Asigna una acción a un doble toque del botón auxiliar seleccionado. | `FlexControlBtn1Action1` – `FlexControlBtn4Action1` |

Las acciones disponibles son:

Tune Slice, Band Zoom, Segment Zoom, RIT, XIT, Master Volume, Headphone Volume, AGCT, APF, Clear RIT, Clear XIT, Toggle APF, Change Active Slice, Split Active Slice, MOX, RF Power, CW Speed, CWX Macro 1–12, Step Up, Step Down, Toggle Tune, Toggle Mute, Toggle Lock, Previous Slice, Toggle AGC, Slice AF Up, Slice AF Down, None.

## Consejos

- Un doble toque debe completarse dentro de los 230 ms posteriores al primer toque. Si toca demasiado lento, la acción se activa como dos toques simples.
- Las acciones que son controles continuos (Tune Slice, Master Volume, etc.) enganchan el botón auxiliar en un modo de sintonización. Las acciones de un solo disparo (Step Up, Toggle MOX, macros) se ejecutan inmediatamente y no se enganchan.

## Relacionado

- [Configurar acciones de un solo toque y doble toque para el botón PUSH](configure-single-and-double-tap-actions-for-the-push-button.md)
- [Mapear acciones del botón pulsador y de doble toque a la rueda](map-push-button-and-double-tap-actions-to-the-wheel.md)
- [Usar la rueda virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
