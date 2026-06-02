# Corregir la estela de TX que permanece visible en el waterfall después de desactivar la transmisión

Después de transmitir, el waterfall podía seguir mostrando una estela brillante de TX durante 10–23 segundos después de soltar la tecla. Esta página explica qué causaba el artefacto y confirma que está resuelto en v0.9.7.

## Antes de empezar

- Se requiere AetherSDR v0.9.7 o posterior. Las versiones anteriores presentan el artefacto de la estela de 10–23 s por diseño.
- La radio debe estar conectada. La corrección depende de recibir el estado de TRANSMITTING del interlock de la radio a través del protocolo SmartSDR.

## Pasos

El artefacto se corrige automáticamente en v0.9.7. No se requiere ninguna acción del usuario.

Cuando transmite, el waterfall se congela tan pronto como el interlock de la radio reporta TRANSMITTING. Cuando desactiva la transmisión, el waterfall se descongela tan pronto como el interlock de la radio reporta que el estado TRANSMITTING se ha despejado. La congelación y descongelación ahora siguen el estado real del interlock de la radio en lugar de un flanco local del software, que era lo que causaba el artefacto de estela en versiones anteriores.

Si está ejecutando v0.9.7 y aún ve una estela persistente después de desactivar la transmisión, siga los pasos de solución de problemas a continuación.

## Consejos

- En una sesión multioperador (multiFLEX), cualquier cliente conectado que transmita activará la congelación del waterfall en su panadapter. Este es un comportamiento esperado.
- Al reconectar la radio, los valores deseados de FPS del panadapter y duración de línea del waterfall se restablecen para evitar una caída silenciosa al valor predeterminado de 10 Hz de la radio.

## Solución de problemas

- **La estela sigue siendo visible después de desactivar la transmisión en v0.9.7** — Confirme que el firmware de la radio sea 4.1.5. Si el firmware es más antiguo, es posible que el estado TRANSMITTING del interlock no se reporte correctamente a través del protocolo, lo que impide que la congelación/descongelación se active en el momento adecuado.
- **El waterfall permanece congelado después de desactivar la transmisión** — El estado del interlock de la radio no se ha despejado. Verifique que nada más (un pedal, VOX u otro cliente) esté manteniendo la radio en estado TRANSMITTING. Consulte `Settings > multiFLEX...` para revisar los clientes conectados.
- **El artefacto solo aparece en un panadapter emergido** — En macOS, un panadapter emergido puede desarrollar problemas de superficie GPU después de ciclos de flotación/acoplamiento. Consulte [Fix a static/stale spectrum in a popped-out panadapter on macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md).

## Relacionado

- [Panadapter overview](overview.md)
- [Fix a static/stale spectrum in a popped-out panadapter on macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
