# Habilitar el inicio automático de CAT con AetherSDR

Habilitar el inicio automático de CAT instruye a AetherSDR para que cree puertos serie virtuales para el control CAT cada vez que la aplicación se inicia, de modo que el software externo de registro o de concurso pueda conectarse sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar ejecutándose en Linux o macOS. Esta función crea puertos serie virtuales y no está disponible en Windows.
- Confirme que ningún software que pretenda conectar mediante CAT esté reteniendo los puertos virtuales abiertos desde una sesión anterior.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart CAT with AetherSDR`.

El elemento de menú es seleccionable. Una marca de verificación junto a la etiqueta indica que el inicio automático está habilitado. Hacer clic en el elemento nuevamente elimina la marca de verificación y deshabilita el inicio automático.

## Qué hace cada control

| Control | Descripción | Clave persistida |
|---|---|---|
| `Autostart CAT with AetherSDR` | Elemento de menú seleccionable. Cuando está marcado, AetherSDR crea puertos serie virtuales para el control CAT en cada inicio (solo Linux y macOS). | `AutoStartCAT` |

## Consejos

- El ajuste surte efecto en el próximo inicio de AetherSDR. Activarlo o desactivarlo durante una sesión en curso no inicia ni detiene CAT de inmediato; reinicie la aplicación para aplicar el cambio.
- Si también usa rigctld para el control CAT, consulte [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md) — ejecutar ambos simultáneamente puede causar conflictos de puertos.

## Solución de problemas

- **Los puertos serie virtuales no aparecen después de habilitar el inicio automático** — Verifique que está ejecutando AetherSDR en Linux o macOS. Esta función no está activa en Windows. Confirme también que ha reiniciado AetherSDR después de habilitar el ajuste.
- **El software CAT no puede abrir el puerto virtual** — Es posible que otro proceso ya esté reteniendo el puerto abierto. Cierre cualquier otro cliente CAT y luego reinicie AetherSDR.

## Relacionados

- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Cables USB](usb-cables.md)
