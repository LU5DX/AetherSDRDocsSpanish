# Solucionar el rastro de TX que permanece visible en el waterfall tras soltar la tecla

Después de transmitir, el waterfall podía continuar mostrando un rastro brillante de TX durante 10–23 segundos después de soltar la tecla. Esta página explica qué causaba el artefacto y confirma que está resuelto en la v0.9.7.

## Antes de comenzar

- Se requiere AetherSDR v0.9.7 o posterior. Las versiones anteriores presentan el artefacto del rastro de 10–23 s por diseño.
- La radio debe estar conectada. La corrección depende de recibir el estado de TRANSMITTING del interlock de la radio a través del protocolo SmartSDR.

## Pasos

El artefacto se corrige automáticamente en la v0.9.7. No se requiere ninguna acción del usuario.

Cuando transmite, el waterfall se congela tan pronto como el interlock de la radio reporta TRANSMITTING. Cuando suelta la tecla, el waterfall se descongela tan pronto como el interlock de la radio reporta que el estado TRANSMITTING se ha despejado. La congelación y descongelación ahora siguen el estado real del interlock de la radio en lugar de un flanco local del software, que era lo que causaba el artefacto del rastro en versiones anteriores.

Si está ejecutando la v0.9.7 y aún ve un rastro persistente después de soltar la tecla, siga los pasos de solución de problemas a continuación.

## Consejos

- En una sesión multioperador (multiFLEX), cualquier cliente conectado que transmita provocará la congelación del waterfall en su panadapter. Esto es un comportamiento esperado.
- Al reconectar la radio, los valores deseados de FPS del panadapter y duración de línea del waterfall se reafirman para evitar una caída silenciosa al valor predeterminado de 10 Hz de la radio.

## Solución de problemas

- **El rastro aún es visible después de soltar la tecla en la v0.9.7** — Confirme que el firmware de la radio es 4.1.5. Si el firmware es anterior, es posible que el estado TRANSMITTING del interlock no se reporte correctamente a través del protocolo, impidiendo que la congelación/descongelación se active en el momento adecuado.
- **El waterfall permanece congelado después de soltar la tecla** — El estado del interlock de la radio no se ha despejado. Verifique que nada más (un pedal, VOX u otro cliente) esté manteniendo la radio en estado TRANSMITTING. Consulte `Settings > multiFLEX...` para revisar los clientes conectados.
- **El artefacto solo aparece en un panadapter emergido** — En macOS, un panadapter emergido puede desarrollar problemas de superficie de GPU después de ciclos de flotación/acoplamiento. Consulte [Fix a static/stale spectrum in a popped-out panadapter on macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md).

## Relacionado

- [Panadapter overview](overview.md)
- [Fix a static/stale spectrum in a popped-out panadapter on macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md)
- [Pop a panadapter out into its own window](pop-a-panadapter-out-into-its-own-window.md)
