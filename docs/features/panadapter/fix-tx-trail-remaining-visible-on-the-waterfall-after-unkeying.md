# Solucionar la estela de TX que permanece visible en el cascada (waterfall) después de soltar la tecla

Después de transmitir, el cascada podía continuar mostrando una estela de TX brillante durante 10–23 segundos después de soltar la tecla. Esta página explica la causa del artefacto y confirma que está resuelto en v0.9.7.

## Antes de comenzar

- Se requiere AetherSDR v0.9.7 o posterior. Las versiones anteriores presentan el artefacto de estela de 10–23 s por diseño.
- El radio debe estar conectado. La corrección depende de recibir el estado TRANSMITTING del interlock del radio a través del protocolo SmartSDR.

## Pasos

El artefacto se corrige automáticamente en v0.9.7. No se requiere ninguna acción por parte del usuario.

Al transmitir, el cascada se congela en cuanto el interlock del radio reporta TRANSMITTING. Al soltar la tecla, el cascada se descongela en cuanto el interlock del radio reporta que el estado TRANSMITTING ha sido eliminado. El congelamiento y descongelamiento ahora siguen el estado real del interlock del radio en lugar de un flanco de software local, que era lo que causaba el artefacto de estela en versiones anteriores.

Si está ejecutando v0.9.7 y aún ve una estela persistente después de soltar la tecla, siga los pasos de solución de problemas que se indican a continuación.

## Consejos

- En una sesión multioperador (multiFLEX), cualquier cliente conectado que transmita activará el congelamiento del cascada en su panadapter. Este es el comportamiento esperado.

## Solución de problemas

- **Estela aún visible después de soltar la tecla en v0.9.7** — Confirme que el firmware del radio es 4.1.5. Si el firmware es más antiguo, es posible que el estado TRANSMITTING del interlock no se reporte correctamente a través del protocolo, lo que impide que el congelamiento y descongelamiento se activen en el momento adecuado.
- **El cascada permanece congelado después de soltar la tecla** — El estado del interlock del radio no se ha eliminado. Verifique que ningún otro elemento (un pedal de pie, VOX u otro cliente) esté manteniendo el radio en TRANSMITTING. Consulte `Settings > multiFLEX...` para revisar los clientes conectados.
- **El artefacto solo aparece en un panadapter desplegado en ventana propia** — En macOS, un panadapter desplegado puede desarrollar problemas de superficie GPU después de ciclos de flotación y acoplamiento. Consulte [Solucionar un espectro estático o desactualizado en un panadapter desplegado en macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md).

## Relacionados

- [Descripción general del panadapter](overview.md)
- [Solucionar un espectro estático o desactualizado en un panadapter desplegado en macOS](fix-a-static-stale-spectrum-in-a-popped-out-panadapter-on-macos.md)
- [Desplegar un panadapter en su propia ventana](pop-a-panadapter-out-into-its-own-window.md)
