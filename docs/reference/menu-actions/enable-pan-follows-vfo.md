# Activar "Pan Follows VFO"

`View > Pan Follows VFO` controla si el panadapter se desplaza automáticamente para mantener visible la frecuencia activa del VFO cuando sintoniza fuera de la vista actual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600 para que el panadapter esté activo.

## Pasos

1. Haga clic en `View` en la barra de menú.
2. Haga clic en `Pan Follows VFO` para activar o desactivar la marca de verificación.
   - Marca presente: el panadapter se desplaza automáticamente para mantener el VFO a la vista.
   - Marca ausente: el panadapter permanece fijo; el VFO puede moverse fuera del rango visible sin que la vista lo siga.

## Función de cada control

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| `Pan Follows VFO` | Activado (marcado) | Cuando está habilitado, el panadapter se desplaza cada vez que la frecuencia del VFO sale del rango de visualización actual. Cuando está deshabilitado, el panadapter no se mueve independientemente de la posición del VFO. |

## Consejos

- Si prefiere desplazar el panadapter manualmente y sintonizar haciendo clic dentro del rango mostrado, desactive `Pan Follows VFO` y active `View > Single-Click to Tune` para que los clics re-sintonicen el VFO sin mover el centro del panadapter.

## Relacionado

- [Activar "Single-Click to Tune"](enable-single-click-to-tune.md)
