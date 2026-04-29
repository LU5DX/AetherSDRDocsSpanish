# Activar el indicador de estado parpadeante

`View > Blink Status Indicator` es un elemento de menú con marca de verificación que controla si el indicador de estado de la barra de título parpadea para señalar el latido del radio. Desactivarlo mantiene el indicador estático si el parpadeo resulta molesto.

## Antes de comenzar

- AetherSDR debe estar en ejecución.
- No es necesario que haya un radio FLEX-8600 conectado para cambiar esta configuración, pero el comportamiento de parpadeo solo es visible cuando hay un latido de radio activo.

## Pasos

1. Haga clic en `View` en la barra de menús.
2. Haga clic en `Blink Status Indicator` para activarlo o desactivarlo.
   - Una marca de verificación junto al elemento indica que el parpadeo está activado.
   - Sin marca de verificación, el indicador permanece estático.

## Qué hace cada control

| Control | Valor predeterminado | Descripción |
|---|---|---|
| `Blink Status Indicator` | Activado (marcado) | Cuando está activado, el indicador de estado de la barra de título parpadea en respuesta a la señal de latido del radio. Cuando está desactivado, el indicador permanece estático. |

## Relacionados

- [Activar ventana sin marco](enable-frameless-window.md)
- [Activar modo mínimo](enable-minimal-mode.md)
