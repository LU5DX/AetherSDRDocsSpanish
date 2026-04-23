# Instalar AetherSDR en macOS

Esta página le guía paso a paso para instalar AetherSDR en macOS y conectarse a su radio Flex.

## Antes de comenzar

- Su Mac debe estar conectado a la misma red local que su radio Flex.
- Confirme que su radio Flex ejecuta el firmware 4.1.5.
- Debe tener permisos suficientes para instalar aplicaciones en su Mac (cuenta de administrador o equivalente).

## Pasos

1. Descargue la imagen de disco macOS más reciente de AetherSDR (`.dmg`) desde el sitio oficial de distribución de AetherSDR.
2. Abra el archivo `.dmg` descargado. Aparecerá una ventana de Finder con el paquete de aplicación de AetherSDR.
3. Arrastre el ícono de AetherSDR a su carpeta **Applications**.
4. Expulse la imagen de disco.
5. Abra **Applications** y haga doble clic en **AetherSDR** para iniciarlo.
6. Si macOS muestra un aviso de seguridad indicando que la aplicación proviene de un desarrollador no identificado, abra **System Settings > Privacy & Security**, desplácese hasta el aviso de la aplicación bloqueada y haga clic en **Open Anyway**.
7. Una vez que AetherSDR esté abierto, vaya a `Settings > Connect to Radio...` para descubrir y conectarse a su radio Flex.

## Consejos

- AetherSDR admite `Autostart DAX with AetherSDR` en macOS (requiere PipeWire o un backend de audio compatible). Actívelo mediante `Settings > Autostart DAX with AetherSDR` si desea que el puente de audio DAX se inicie automáticamente al lanzar la aplicación.
- Los puertos serie virtuales para control CAT están disponibles en macOS. Habilite el inicio automático mediante `Settings > Autostart CAT with AetherSDR` (almacenado como `AutoStartCAT`).

## Relacionados

- [Instalar AetherSDR en Linux](installation-linux.md)
- [Instalar AetherSDR en Windows](installation-windows.md)
