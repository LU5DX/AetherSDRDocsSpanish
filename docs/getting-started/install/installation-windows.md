# Instalar AetherSDR en Windows

Esta página le guía a través de la descarga e instalación de AetherSDR en Windows para que pueda conectarse a su radio Flex.

## Antes de comenzar

- Su cuenta de usuario de Windows debe tener permiso para ejecutar instaladores.
- Su radio Flex debe estar en la misma red que su equipo Windows.
- Cierre cualquier otro cliente compatible con SmartSDR antes de ejecutar AetherSDR por primera vez.

## Pasos

1. Descargue el instalador más reciente de AetherSDR para Windows desde el sitio de distribución oficial de AetherSDR.
2. Haga doble clic en el archivo del instalador descargado para iniciarlo.
3. Siga las instrucciones en pantalla, aceptando el directorio de instalación predeterminado a menos que tenga un motivo para cambiarlo.
4. Cuando el instalador finalice, haga clic en **Finish** para cerrarlo.
5. Inicie AetherSDR desde el menú Inicio o el acceso directo del escritorio creado por el instalador.
6. Cuando AetherSDR se abra, vaya a `Settings > Connect to Radio...` para descubrir su radio Flex y conectarse a ella.

## Solución de problemas

- **AetherSDR no se inicia después de la instalación** — Verifique que su sistema cumple con los requisitos mínimos del tiempo de ejecución de Qt6. Si aparece un error de DLL faltante, vuelva a ejecutar el instalador y elija la opción de instalar las dependencias de tiempo de ejecución, o instale el paquete Redistribuible de Visual C++ para la versión incluida con AetherSDR.
- **No se encuentra la radio en Connect to Radio...** — Confirme que la radio Flex y el equipo Windows están en la misma subred y que el Firewall de Windows no está bloqueando el acceso de red de AetherSDR. Agregue una excepción de firewall para AetherSDR si es necesario.

## Relacionados

- [Instalar AetherSDR en Linux](installation-linux.md)
- [Instalar AetherSDR en macOS](installation-macos.md)
