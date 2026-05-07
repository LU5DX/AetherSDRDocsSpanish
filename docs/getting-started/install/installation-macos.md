# Instalar AetherSDR en macOS

Esta página le guía en la instalación de AetherSDR en macOS para que pueda conectarse a su radio Flex.

## Antes de comenzar

- Su Mac debe estar conectada a la misma red local que su radio Flex.
- Confirme que su radio Flex ejecuta el firmware 4.1.5.
- Debe tener permisos suficientes para instalar aplicaciones en su Mac (cuenta de administrador o equivalente).

## Pasos

1. Descargue la última imagen de disco de AetherSDR para macOS (`.dmg`) desde el sitio oficial de distribución de AetherSDR.
2. Abra el archivo `.dmg` descargado. Aparecerá una ventana del Finder que muestra el paquete de la aplicación AetherSDR.
3. Arrastre el icono de AetherSDR a la carpeta **Applications**.
4. Expulse la imagen de disco.
5. Abra **Applications** y haga doble clic en **AetherSDR** para iniciarlo.
6. Si macOS muestra un aviso de seguridad indicando que la aplicación proviene de un desarrollador no identificado, abra **System Settings > Privacy & Security**, desplace hacia abajo hasta la notificación de la aplicación bloqueada y haga clic en **Open Anyway**.
7. Una vez que AetherSDR se abra, vaya a `Settings > Connect to Radio...` para descubrir y conectarse a su radio Flex.

## Consejos

- AetherSDR es compatible con `Autostart DAX with AetherSDR` en macOS (requiere PipeWire o un backend de audio compatible). Actívelo mediante `Settings > Autostart DAX with AetherSDR` si desea que el puente de audio DAX se inicie automáticamente al arrancar.
- Los puertos serie virtuales para control CAT están disponibles en macOS. Active el inicio automático mediante `Settings > Autostart CAT with AetherSDR` (se guarda como `AutoStartCAT`).

## Relacionado

- [Install AetherSDR on Linux](installation-linux.md)
- [Install AetherSDR on Windows](installation-windows.md)
