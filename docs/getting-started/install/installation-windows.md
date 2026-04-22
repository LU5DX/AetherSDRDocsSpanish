# Instalar AetherSDR en Windows

Esta página le explica cómo descargar e instalar AetherSDR en Windows para conectarse a su radio FLEX-8600.

## Antes de comenzar

- Su cuenta de usuario de Windows debe tener permiso para ejecutar instaladores.
- Su FLEX-8600 debe estar en la misma red que su equipo Windows.
- Cierre cualquier otro cliente compatible con SmartSDR antes de ejecutar AetherSDR por primera vez.

## Pasos

1. Descargue el instalador más reciente de AetherSDR para Windows desde el sitio oficial de distribución de AetherSDR.
2. Haga doble clic en el archivo instalador descargado para iniciarlo.
3. Siga las instrucciones en pantalla y acepte el directorio de instalación predeterminado, a menos que tenga motivos para cambiarlo.
4. Cuando el instalador termine, haga clic en Finish para cerrarlo.
5. Inicie AetherSDR desde el menú Start o el acceso directo del escritorio creado por el instalador.
6. Cuando AetherSDR se abra, vaya a `Settings > Connect to Radio...` para descubrir y conectarse a su FLEX-8600.

## Solución de problemas

- **AetherSDR no inicia después de la instalación** — Verifique que su sistema cumpla con los requisitos mínimos de tiempo de ejecución de Qt6. Si aparece un error de DLL faltante, vuelva a ejecutar el instalador y elija la opción para instalar las dependencias de tiempo de ejecución, o instale el Visual C++ Redistributable correspondiente a la versión incluida con AetherSDR.
- **No se encuentra la radio en Connect to Radio...** — Confirme que el FLEX-8600 y el equipo Windows estén en la misma subred y que el Firewall de Windows no esté bloqueando el acceso de red de AetherSDR. Si es necesario, agregue una excepción en el firewall para AetherSDR.

## Relacionados

- [Instalar AetherSDR en Linux](installation-linux.md)
- [Instalar AetherSDR en macOS](installation-macos.md)
