# Habilitar el inicio automático de CAT con AetherSDR

Esta página explica cómo habilitar el inicio automático de los puertos serie virtuales para control CAT cuando se inicia AetherSDR. Use esta función si desea que su software de registro de QSO o de concursos con soporte CAT se conecte a AetherSDR inmediatamente al arranque, sin necesidad de habilitar CAT manualmente en cada sesión.

## Antes de comenzar

- El inicio automático de CAT crea puertos serie virtuales y solo está disponible en Linux y macOS. Los usuarios de Windows deben consultar un método CAT alternativo, como rigctld.
- Compruebe que su software de terceros está configurado para conectarse al puerto serie virtual que creará AetherSDR.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart CAT with AetherSDR`.

El elemento de menú es seleccionable. Una marca de verificación junto a la etiqueta indica que el inicio automático de CAT está habilitado. Al hacer clic de nuevo se elimina la marca y se deshabilita el inicio automático. La configuración se conserva entre sesiones bajo la clave `AutoStartCAT`.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Clave persistente |
|---|---|---|---|
| `Autostart CAT with AetherSDR` | Cuando está marcado, AetherSDR crea puertos serie virtuales para control CAT cada vez que se inicia. Compatible con Linux y macOS. | Desactivado (sin marcar) | `AutoStartCAT` |

## Solución de problemas

- **El elemento de menú está presente pero CAT no se inicia en Windows** — El inicio automático de CAT mediante puertos serie virtuales no es compatible con Windows. Use `Autostart rigctld with AetherSDR` como interfaz CAT alternativa en esa plataforma.
- **El software de terceros indica que el puerto serie no está disponible** — Verifique que el software esté configurado para usar el puerto virtual correcto y que ningún otro proceso tenga el puerto abierto. Desmarque y vuelva a marcar `Autostart CAT with AetherSDR` para forzar la recreación de los puertos virtuales y, a continuación, reinicie AetherSDR.

## Temas relacionados

- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Cables USB](usb-cables.md)
