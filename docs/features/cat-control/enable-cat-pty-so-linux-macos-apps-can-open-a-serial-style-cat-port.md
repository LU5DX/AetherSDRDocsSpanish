# Habilitar CAT PTY para que aplicaciones en Linux/macOS puedan abrir un puerto CAT de estilo serie

La función CAT PTY crea cuatro enlaces simbólicos de puerto serie virtual en `/tmp/` que el software de registro y de concursos puede abrir como si fueran dispositivos serie físicos. Úsela cuando su software espere una ruta de puerto serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet CAT Control requiere una conexión de radio activa.
- Los enlaces simbólicos PTY están disponibles únicamente en Linux y macOS. Esta función no está disponible en Windows.
- El applet CAT Control está oculto de forma predeterminada. Debe hacerlo visible antes de poder usarlo.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para mostrar el applet CAT Control.
2. Haga clic en **Enable TTY**.

El botón se ilumina en verde cuando está activo. Las cuatro filas de canal (A, B, C, D) se actualizan para mostrar las rutas de enlace simbólico activas desde `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`.

3. En su aplicación externa, abra la ruta de puerto serie que se muestra en la fila del canal correspondiente — por ejemplo, `/tmp/AetherSDR-CAT-A` para el canal A.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable TTY** | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. | Desactivado | — | — |
| **Enable TCP** | Inicia o detiene los cuatro servidores TCP de rigctld desde Base hasta Base+3. | Desactivado | — | — |
| **Base** | Puerto TCP base. Los canales se vinculan a puerto, puerto+1, puerto+2, puerto+3. Los canales PTY A–D corresponden a la misma numeración de canales. | 4532 | 1024–65535 | `CatTcpPort` |
| Filas de canal A/B/C/D | Cada fila muestra la insignia del canal, el estado del servidor TCP y la ruta del enlace simbólico PTY actual. | (detenido) | — | — |

## Consejos

- Cada canal (A, B, C, D) corresponde a un slice de radio. Apunte el canal A a su slice principal y use los canales B–D para slices adicionales si es necesario.
- La ruta PTY que se muestra en cada fila de canal se actualiza a la ruta de enlace simbólico en ejecución una vez que **Enable TTY** está activo. Si la fila sigue mostrando `/tmp/AetherSDR-CAT-A`, el PTY no se ha iniciado correctamente.
- Puede habilitar **Enable TTY** y **Enable TCP** simultáneamente para servir tanto a aplicaciones de estilo serie como a aplicaciones conectadas por red al mismo tiempo.
- Para iniciar los enlaces simbólicos PTY automáticamente cada vez que AetherSDR se inicie, use `Settings > Autostart CAT with AetherSDR`.
- Los valores fuera de rango ingresados en **Base** vuelven automáticamente a 4532.

## Solución de problemas

- **La fila del canal sigue mostrando `(stopped)` después de hacer clic en Enable TTY** — Confirme que está ejecutando Linux o macOS. Los enlaces simbólicos PTY no están disponibles en Windows. Confirme también que la conexión de radio está activa; el applet requiere una radio conectada.
- **La aplicación externa no puede abrir `/tmp/AetherSDR-CAT-A`** — Confirme que **Enable TTY** está activo (el botón muestra verde). Verifique que ningún otro proceso tenga un bloqueo exclusivo sobre el enlace simbólico. Compruebe que la ruta mostrada en la fila del canal coincide con la que su aplicación está configurada para abrir.
- **La ruta PTY en la fila del canal no se actualiza** — Es posible que el enlace simbólico no se haya creado. Verifique que `/tmp/` tenga permisos de escritura para su cuenta de usuario.

## Relacionados

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
