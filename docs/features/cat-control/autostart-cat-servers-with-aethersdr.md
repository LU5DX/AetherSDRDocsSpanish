# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para iniciar sus servidores TCP CAT y/o puertos serie PTY automáticamente cada vez que la aplicación se inicie, de modo que el software externo de registro y concursos esté listo sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El control CAT requiere una conexión de radio.
- Decida si necesita servidores TCP (para software como N1MM, Log4OM o WSJT-X), puertos serie PTY (solo Linux/macOS), o ambos.
- Confirme el puerto TCP base que desea usar. El valor predeterminado es `4532`. Consulte [Cambiar el puerto TCP base](change-the-base-tcp-port.md) si necesita un valor diferente.

## Pasos

### Inicio automático de servidores TCP

1. Haga clic en `Settings > Autostart rigctld with AetherSDR`.

   Aparece una marca de verificación junto al elemento. En el próximo inicio, AetherSDR arrancará automáticamente los cuatro servidores TCP rigctld en los puertos `Base` hasta `Base+3`.

2. Para verificar que los servidores iniciaron, haga clic en el botón de bandeja **CAT** en la barra lateral derecha para abrir el applet de control CAT. Cada fila de canal (A, B, C, D) debe mostrar un puerto y un recuento de clientes en lugar de `(stopped)`.

### Inicio automático de puertos serie PTY (solo Linux/macOS)

1. Haga clic en `Settings > Autostart CAT with AetherSDR`.

   Aparece una marca de verificación junto al elemento. En el próximo inicio, AetherSDR creará automáticamente enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`.

2. Para verificar, abra el applet de control CAT mediante el botón de bandeja **CAT**. La columna de ruta PTY en cada fila de canal mostrará la ruta del enlace simbólico activo cuando esté en ejecución.

### Desactivar el inicio automático

1. Haga clic en el mismo elemento de menú nuevamente (`Settings > Autostart rigctld with AetherSDR` o `Settings > Autostart CAT with AetherSDR`).

   Se elimina la marca de verificación. Los servidores o puertos PTY ya no se iniciarán al arrancar.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| `Settings > Autostart rigctld with AetherSDR` | Desactivado | Activado / Desactivado | `AutoStartRigctld` | Cuando está marcado, inicia los cuatro servidores TCP rigctld al arrancar. |
| `Settings > Autostart CAT with AetherSDR` | Desactivado | Activado / Desactivado | `AutoStartCAT` | Cuando está marcado, crea enlaces simbólicos PTY al arrancar (Linux/macOS). |
| Base (en el applet de control CAT) | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base. Los canales se vinculan a `Base`, `Base+1`, `Base+2`, `Base+3`. Los valores fuera de rango revierten a `4532`. |

## Consejos

- El inicio automático únicamente levanta los servidores; no abre el panel del applet de control CAT. El applet permanece oculto hasta que haga clic en el botón de bandeja **CAT**.
- Si cambia el puerto base en el campo `Base` mientras los servidores TCP están en ejecución, estos se reinician automáticamente en los nuevos puertos. No es necesario desactivar y volver a activar `Enable TCP`.
- La configuración de inicio automático TCP (`AutoStartRigctld`) y la configuración de inicio automático PTY (`AutoStartCAT`) son independientes. Puede activar una, ambas o ninguna.

## Solución de problemas

- **Las filas de canal siguen mostrando `(stopped)` después del inicio con el arranque automático activado** — El inicio automático requiere una conexión de radio antes de que los servidores puedan vincularse. Si AetherSDR se inició pero aún no se ha conectado a la radio, los servidores no arrancarán. Conéctese a la radio y luego active `Enable TCP` manualmente en el applet de control CAT.
- **Las rutas PTY no aparecen en Windows** — La creación de puertos serie PTY es una función de Linux/macOS. El elemento `Settings > Autostart CAT with AetherSDR` no tiene efecto en Windows.
- **El enlace de puerto falla al iniciar** — Es posible que otra aplicación ya esté usando el puerto `4532` (o el puerto base que configuró). Cambie el puerto base en el campo `Base` del applet de control CAT y reinicie.

## Relacionados

- [Activar CAT TCP para que N1MM, Log4OM y WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Activar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
