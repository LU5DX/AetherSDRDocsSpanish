# Habilitar inicio automático de DAX con AetherSDR

Esta página explica cómo configurar AetherSDR para iniciar el puente de audio DAX automáticamente cada vez que se lance la aplicación. Úselo si desea tener disponible el enrutamiento de audio DAX de inmediato, sin tener que habilitarlo manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar instalado y ser capaz de conectarse a una radio FLEX-8600.
- La compatibilidad con el puente de audio DAX requiere macOS o un sistema Linux con PipeWire.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart DAX with AetherSDR`.

El elemento de menú es una casilla de verificación. Cuando está marcado, AetherSDR iniciará el puente de audio DAX automáticamente en cada inicio. Haga clic nuevamente en el elemento para deshabilitar el inicio automático.

## Descripción de cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| `Autostart DAX with AetherSDR` | Elemento de menú seleccionable. Cuando está marcado, AetherSDR inicia el puente de audio DAX al iniciarse. Se aplica en macOS y sistemas Linux basados en PipeWire. | `AutoStartDAX` |

## Solución de problemas

- **El elemento de menú no tiene efecto en Windows**: el inicio automático de DAX solo es compatible con macOS y sistemas Linux basados en PipeWire. En otras plataformas, configure el enrutamiento de audio DAX a través de la configuración de audio de su sistema.
- **El puente de audio DAX no se inicia a pesar de que el elemento esté marcado**: verifique que PipeWire se esté ejecutando en su sistema Linux, o que el subsistema de audio de su macOS esté disponible al iniciar sesión. Desmarque y vuelva a marcar `Autostart DAX with AetherSDR` para restablecer la configuración.

## Relacionados

- [Habilitar inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
