# Alternar giro automático para la animación de cambio de frecuencia externo

Active o desactive la animación automática de giro virtual del mando que se reproduce cuando una fuente externa cambia la frecuencia del slice, como al hacer clic en el panadapter o usar comandos CAT.

## Antes de comenzar

- Abra el diálogo AetherControl a través de **Settings > AetherControl...**

## Pasos

1. Haga clic en **External Spin** para activar o desactivar la animación.

Cuando está activado, arrastrar en el panadapter o cambiar la frecuencia desde una fuente externa activa una animación de gesto de sintonización con giro del mando en el mando virtual. Cuando está desactivado, los cambios de frecuencia ocurren inmediatamente sin animación.

## Qué hace cada control

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Botón de alternancia | External Spin | Activa o desactiva la animación de giro en el mando virtual cuando los cambios de frecuencia se originan fuera del mando. Clave de configuración: `FlexControlVirtualExternalSpin` |

## Relacionados

- [Use el mando virtual para sintonizar el slice activo](use-the-virtual-wheel-to-tune-the-active-slice.md)
- [Configure el controlador hardware AetherControl / FlexControl](configure-the-aethercontrol-flexcontrol-hardware-controller.md)
