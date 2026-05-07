# Instalar AetherSDR en Linux

Esta página le guía a través de la instalación de AetherSDR en un sistema Linux para que pueda conectarse a su radio Flex.

## Antes de comenzar

- Confirme que su distribución y arquitectura de Linux sean compatibles con el paquete AetherSDR que ha obtenido.
- Asegúrese de tener privilegios suficientes para instalar software (acceso `root` o `sudo`).
- Verifique que su sistema tenga las bibliotecas de ejecución de Qt6 disponibles si va a instalar desde un binario precompilado y no desde un paquete de distribución.
- Mantenga activa su conexión de red — AetherSDR descubre radios en la red local en el primer inicio.

## Pasos

1. Descargue el paquete AetherSDR para Linux desde la fuente de distribución oficial.
2. Abra una terminal en el directorio que contiene el archivo descargado.
3. Instale el paquete usando el gestor de paquetes de su distribución. Por ejemplo, en un sistema Debian o Ubuntu:
   ```
   sudo apt install ./aethersdr_<version>_amd64.deb
   ```
   En un sistema basado en RPM:
   ```
   sudo rpm -i aethersdr-<version>.x86_64.rpm
   ```
4. Una vez completada la instalación, inicie AetherSDR desde el menú de aplicaciones o ejecutando:
   ```
   aethersdr
   ```
5. En el primer inicio, vaya a `Settings > Connect to Radio...` para descubrir y conectarse a su radio Flex.

## Consejos

- Si planea usar control CAT desde un software de registro de terceros, active `Settings > Autostart CAT with AetherSDR` después de conectarse. Esta función crea puertos serie virtuales y está disponible en Linux.
- Si usa software compatible con rigctld, active `Settings > Autostart rigctld with AetherSDR` para que AetherSDR inicie el servidor CAT rigctld automáticamente en cada inicio.
- Si se requiere puenteo de audio DAX a través de PipeWire, active `Settings > Autostart DAX with AetherSDR`.

## Solución de problemas

- **AetherSDR no se inicia después de la instalación** — Confirme que las bibliotecas de ejecución de Qt6 estén instaladas en su sistema. El gestor de paquetes de su distribución debería instalarlas automáticamente desde las dependencias del paquete; si no, instale las bibliotecas base de Qt6 manualmente.
- **No se encuentran radios en `Settings > Connect to Radio...`** — Confirme que el radio Flex esté encendido y conectado al mismo segmento de red local. Verifique que ninguna regla de cortafuegos esté bloqueando el tráfico de descubrimiento UDP.
- **Los puertos serie virtuales para CAT no se crean** — Confirme que `Settings > Autostart CAT with AetherSDR` esté activado. Esta función requiere que los módulos de kernel apropiados para puertos serie virtuales estén cargados en su sistema.

## Relacionado

- [Install AetherSDR on Windows](installation-windows.md)
- [Install AetherSDR on macOS](installation-macos.md)
