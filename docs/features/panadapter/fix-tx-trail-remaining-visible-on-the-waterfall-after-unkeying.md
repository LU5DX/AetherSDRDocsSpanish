# Solucionar la persistencia de la estela TX en el waterfall después de dejar de transmitir

Después de transmitir, el waterfall podía seguir mostrando una estela TX brillante durante 10–23 segundos después de soltar la tecla. Esta página explica qué causaba el artefacto y confirma que está resuelto en v0.9.7.

## Antes de comenzar

- Se requiere AetherSDR v0.9.7 o posterior. Las versiones anteriores presentan el artefacto de estela de 10–23 s por diseño.
- El equipo debe estar conectado. La corrección depende de recibir el estado TRANSMITTING del interlock del equipo a través del protocolo SmartSDR.

## Pasos

El artefacto se corrige automáticamente en v0.9.7. No se requiere ninguna acción del usuario.

Cuando transmite, el waterfall se congela en cuanto el interlock del equipo indica TRANSMITTING. Cuando deja de transmitir, el waterfall se descongela en cuanto el interlock del equipo indica que el estado TRANSMITTING se ha desactivado. La congelación y descongelación ahora siguen el estado real del interlock del equipo en lugar de un flanco local del software, que es lo que causaba el artefacto de estela en versiones anteriores.

Si está usando v0.9.7 y aún ve una estela persistente después de dejar de transmitir, siga los pasos de solución de problemas a continuación.

## Consejos

- En una sesión multioperador (multiFLEX), cualquier cliente conectado que esté transmitiendo provocará la congelación del waterfall en su panadapter. Este comportamiento es esperado.

## Solución de problemas

- **La estela sigue siendo visible después de dejar de transmitir en v0.9.7** — Confirme que el firmware del equipo sea 4.1.5. Si el firmware es más antiguo, es posible que el estado TRANSMITTING del interlock no se informe correctamente a través del protocolo, lo que impide que la congelación/descongelación se active en el momento adecuado.
- **El waterfall permanece congelado después de dejar de transmitir** — El estado del interlock del equipo no se ha desactivado. Verifique que nada más (un pedal, VOX u otro cliente) esté manteniendo el equipo en estado TRANSMITTING. Consulte `Settings > multiFLEX…` para revisar los clientes conectados.
- **El artefacto solo aparece en un panadapter emergido** — En macOS, un panadapter emergido puede desarrollar problemas en la superficie de GPU después de ciclos de flotación/acoplamiento. Consulte [Solucionar un espectro estático/desactualizado en un panadapter emergido en macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md).

## Relacionado

- [Descripción general del panadapter](overview.md)
- [Solucionar un espectro estático/desactualizado en un panadapter emergido en macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md)
- [Emerger un panadapter a su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
