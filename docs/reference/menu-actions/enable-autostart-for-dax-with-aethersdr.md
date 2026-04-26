# Habilitar el inicio automático de DAX con AetherSDR

Esta página explica cómo configurar AetherSDR para que inicie el puente de audio DAX automáticamente cada vez que se abre la aplicación. Use esta opción si desea que el enrutamiento de audio DAX esté disponible de inmediato sin tener que habilitarlo manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar instalado y ser capaz de conectarse a una radio FLEX-8600.
- La compatibilidad con el puente de audio DAX requiere macOS o un sistema Linux con PipeWire.

## Pasos

1. Haga clic en `Settings` en la barra de menús.
2. Haga clic en `Autostart DAX with AetherSDR`.

El elemento del menú es un interruptor con marca de verificación. Cuando está marcado, AetherSDR iniciará el puente de audio DAX automáticamente en cada arranque. Haga clic en el elemento nuevamente para deshabilitar el inicio automático.

## Qué hace cada control

| Control | Descripción | Clave persistente |
|---|---|---|
| `Autostart DAX with AetherSDR` | Elemento de menú con marca de verificación. Cuando está marcado, AetherSDR inicia el puente de audio DAX al arrancar. Aplica en macOS y sistemas Linux basados en PipeWire. | `AutoStartDAX` |

## Solución de problemas

- **El elemento del menú no tiene efecto en Windows** — El inicio automático de DAX es compatible únicamente con macOS y Linux basado en PipeWire. En otras plataformas, configure el enrutamiento de audio DAX a través de la configuración de audio del sistema.
- **El puente de audio DAX no inicia a pesar de que el elemento está marcado** — Verifique que PipeWire esté en ejecución en su sistema Linux, o que el subsistema de audio de macOS esté disponible al iniciar sesión. Desmarque y vuelva a marcar `Autostart DAX with AetherSDR` para restablecer la configuración.

## Relacionados

- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
