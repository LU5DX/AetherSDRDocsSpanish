# Instalar AetherSDR en Windows

Esta página le guía paso a paso para descargar e instalar AetherSDR en Windows y conectarse a su radio Flex.

## Antes de comenzar

- Su cuenta de usuario de Windows debe tener permisos para ejecutar instaladores.
- Su radio Flex debe estar en la misma red que su equipo Windows.
- Cierre cualquier otro cliente compatible con SmartSDR antes de ejecutar AetherSDR por primera vez.

## Pasos

1. Descargue el instalador más reciente de AetherSDR para Windows desde el sitio oficial de distribución de AetherSDR.
2. Haga doble clic en el archivo del instalador descargado para iniciarlo.
3. Siga las instrucciones en pantalla y acepte el directorio de instalación predeterminado, a menos que tenga una razón para cambiarlo.
4. Cuando el instalador finalice, haga clic en Finish para cerrarlo.
5. Inicie AetherSDR desde el menú Start o desde el acceso directo del escritorio creado por el instalador.
6. Cuando AetherSDR se abra, vaya a `Settings > Connect to Radio...` para detectar y conectarse a su radio Flex.

## Solución de problemas

- **AetherSDR no inicia después de la instalación** — Verifique que su sistema cumpla con los requisitos mínimos del entorno de ejecución Qt6. Si aparece un error de DLL faltante, vuelva a ejecutar el instalador y seleccione la opción para instalar las dependencias del entorno de ejecución, o instale el paquete Visual C++ Redistributable correspondiente a la versión incluida con AetherSDR.
- **No se encuentra la radio en Connect to Radio...** — Confirme que el radio Flex y el equipo Windows están en la misma subred y que el Firewall de Windows no está bloqueando el acceso a la red de AetherSDR. Si es necesario, agregue una excepción en el firewall para AetherSDR.

## Relacionados

- [Instalar AetherSDR en Linux](installation-linux.md)
- [Instalar AetherSDR en macOS](installation-macos.md)
