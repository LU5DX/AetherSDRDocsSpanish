# Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie

La función CAT PTY crea cuatro enlaces simbólicos de puerto serie virtual bajo `/tmp/` que el software de registro y de concursos en Linux y macOS puede abrir como si fueran puertos serie físicos. Úsela cuando su aplicación espere una ruta de dispositivo serie en lugar de una conexión TCP.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT Control requiere una conexión de radio activa.
- Los enlaces simbólicos PTY solo se crean en Linux y macOS. Esta función no está disponible en Windows.
- El botón CAT del área de notificación debe ser visible en la barra lateral derecha. Si no es visible, consulte [Descripción general de CAT Control](overview.md).

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para abrir el applet CAT Control.
2. Haga clic en **Enable TTY** para iniciar los servidores PTY.
3. Revise las filas de cada canal. Cuando cada PTY esté en ejecución, la columna de ruta se actualiza desde `/tmp/AetherSDR-CAT-A` (o B, C, D) a la ruta del enlace simbólico activo asignada por el sistema.
4. En su aplicación de registro o de concursos, configure el puerto serie con la ruta que se muestra en la fila del canal correspondiente — por ejemplo `/tmp/AetherSDR-CAT-A` para el canal A.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **Enable TTY** | Botón de alternancia | Off | On / Off | — | Inicia o detiene los cuatro enlaces simbólicos PTY bajo `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. |
| **Base** | Campo de texto | `4532` | 1024–65535 | `CatTcpPort` | Puerto TCP base usado por los servidores TCP. No afecta las rutas PTY. Los valores fuera de rango vuelven automáticamente a `4532`. |
| Filas A / B / C / D | Indicador | `(stopped)` | — | — | Cada fila muestra una insignia de canal con código de color, el estado del servidor TCP y la ruta del enlace simbólico PTY actual. |

## Consejos

- Cada uno de los cuatro canales (A–D) se corresponde con un slice de radio. Abra la ruta del canal que corresponda al slice que desea controlar.
- Puede ejecutar **Enable TTY** y **Enable TCP** al mismo tiempo. Funcionan de manera independiente.
- Para iniciar los servidores PTY automáticamente cada vez que AetherSDR se inicie, use `Settings > Autostart CAT with AetherSDR`.

## Solución de problemas

- **La ruta PTY no aparece o permanece en gris después de hacer clic en Enable TTY** — confirme que el radio esté conectado. El applet CAT Control requiere una conexión de radio activa antes de que los servidores PTY puedan iniciarse.
- **La ruta del enlace simbólico que se muestra no es `/tmp/AetherSDR-CAT-A`** — es posible que el sistema haya asignado una ruta de dispositivo esclavo diferente. Use la ruta exacta que se muestra en la fila del canal, no un valor fijo.
- **Enable TTY no tiene efecto en Windows** — los enlaces simbólicos PTY son una función de Linux/macOS. Use **Enable TCP** y una utilidad de puente TCP a serie en su lugar.

## Relacionados

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
