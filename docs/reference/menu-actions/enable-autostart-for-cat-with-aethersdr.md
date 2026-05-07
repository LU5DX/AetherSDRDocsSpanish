# Habilitar el inicio automático de CAT con AetherSDR

Habilitar el inicio automático de CAT le indica a AetherSDR que cree puertos serie virtuales para el control CAT cada vez que se inicie la aplicación, de modo que el software externo de registro o de concurso pueda conectarse sin intervención manual.

## Antes de empezar

- AetherSDR debe ejecutarse en Linux o macOS. Esta función crea puertos serie virtuales y no está disponible en Windows.
- Asegúrese de que cualquier software que pretenda conectar a través de CAT no tenga ya abiertos los puertos virtuales de una sesión anterior.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart CAT with AetherSDR`.

El elemento del menú es seleccionable. Una marca de verificación junto a la etiqueta indica que el inicio automático está habilitado. Al hacer clic nuevamente en el elemento, se elimina la marca de verificación y se deshabilita el inicio automático.

## Función de cada control

| Control | Descripción | Clave persistente |
|---|---|---|
| `Autostart CAT with AetherSDR` | Elemento de menú seleccionable. Cuando está marcado, AetherSDR crea puertos serie virtuales para el control CAT en cada inicio (solo Linux y macOS). | `AutoStartCAT` |

## Consejos

- La configuración surte efecto en el siguiente inicio de AetherSDR. Alternarla durante una sesión en ejecución no inicia ni detiene CAT inmediatamente; reinicie la aplicación para aplicar el cambio.
- Si también utiliza rigctld para el control CAT, consulte [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md) — ejecutar ambos simultáneamente puede provocar conflictos de puertos.

## Solución de problemas

- **Los puertos serie virtuales no aparecen después de habilitar el inicio automático** — Verifique que está ejecutando AetherSDR en Linux o macOS. Esta función no está activa en Windows. También confirme que ha reiniciado AetherSDR después de habilitar la configuración.
- **El software CAT no puede abrir el puerto virtual** — Es posible que otro proceso ya tenga el puerto abierto. Cierre cualquier otro cliente CAT y luego reinicie AetherSDR.

## Relacionados

- [Habilitar el inicio automático de rigctld con AetherSDR](enable-autostart-for-rigctld-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Cables USB](usb-cables.md)
