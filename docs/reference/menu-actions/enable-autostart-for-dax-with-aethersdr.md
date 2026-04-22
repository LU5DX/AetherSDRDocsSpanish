# Habilitar el inicio automático de DAX con AetherSDR

Esta página explica cómo configurar AetherSDR para iniciar el puente de audio DAX automáticamente cada vez que se inicia la aplicación. Use esta configuración si desea que el enrutamiento de audio DAX esté disponible de inmediato sin habilitarlo manualmente después de cada inicio.

## Antes de comenzar

- AetherSDR debe estar instalado y poder conectarse a su FLEX-8600.
- El puente de audio DAX es compatible con macOS y sistemas Linux basados en PipeWire. Esta configuración no tiene efecto en otras plataformas.

## Pasos

1. En la barra de menús, haga clic en `Settings`.
2. Haga clic en `Autostart DAX with AetherSDR`.

El elemento de menú es seleccionable. Cuando está marcado, AetherSDR inicia el puente de audio DAX cada vez que se inicia la aplicación. Haga clic de nuevo para desmarcarlo y deshabilitar el inicio automático.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| `Autostart DAX with AetherSDR` | Elemento de menú seleccionable. Cuando está marcado, el puente de audio DAX se inicia automáticamente al lanzar la aplicación (solo en macOS y PipeWire). | Sin marcar | `AutoStartDAX` |

## Consejos

- La configuración `AutoStartDAX` se conserva entre sesiones. Solo es necesario establecerla una vez.
- Si ejecuta AetherSDR en múltiples plataformas, tenga en cuenta que esta configuración solo está activa en macOS y Linux basado en PipeWire. En otros sistemas, la opción puede aparecer pero no tiene efecto.

## Relacionado

- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
