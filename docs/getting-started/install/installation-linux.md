# Instalar AetherSDR en Linux

Esta página le guía a través de la instalación de AetherSDR en un sistema Linux para que pueda conectarse a su radio Flex.

## Antes de comenzar

- Confirme que su distribución de Linux y arquitectura son compatibles con el paquete de AetherSDR que ha obtenido.
- Asegúrese de contar con los privilegios suficientes para instalar software (acceso como `root` o mediante `sudo`).
- Verifique que su sistema tenga disponibles las bibliotecas de tiempo de ejecución de Qt6 si está instalando desde un binario precompilado en lugar de un paquete de distribución.
- Tenga activa su conexión de red — AetherSDR descubre radios en la red local al primer inicio.

## Pasos

1. Descargue el paquete de AetherSDR para Linux desde la fuente de distribución oficial.
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

- Si planea usar control CAT desde software de registro de terceros, habilite `Settings > Autostart CAT with AetherSDR` después de conectarse. Esta función crea puertos serie virtuales y está disponible en Linux.
- Si utiliza software compatible con rigctld, habilite `Settings > Autostart rigctld with AetherSDR` para que AetherSDR inicie automáticamente el servidor CAT rigctld en cada arranque.
- Si se requiere puente de audio DAX mediante PipeWire, habilite `Settings > Autostart DAX with AetherSDR`.

## Solución de problemas

- **AetherSDR no inicia después de la instalación** — Confirme que las bibliotecas de tiempo de ejecución de Qt6 están instaladas en su sistema. El gestor de paquetes de su distribución debería incluirlas automáticamente desde las dependencias del paquete; de no ser así, instale manualmente las bibliotecas base de Qt6.
- **No se encuentran radios en `Settings > Connect to Radio...`** — Confirme que la radio Flex está encendida y conectada al mismo segmento de red local. Verifique que ninguna regla de firewall esté bloqueando el tráfico de descubrimiento UDP.
- **No se crean los puertos serie virtuales para CAT** — Confirme que `Settings > Autostart CAT with AetherSDR` está habilitado. Esta función requiere que los módulos de kernel apropiados para puertos serie virtuales estén cargados en su sistema.

## Relacionados

- [Instalar AetherSDR en Windows](installation-windows.md)
- [Instalar AetherSDR en macOS](installation-macos.md)
