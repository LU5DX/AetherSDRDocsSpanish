# Habilitar CAT PTY para que las aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie

La función CAT PTY crea enlaces simbólicos de puertos serie virtuales en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`, uno por canal. Úsela cuando su software de registro o de modos digitales necesite abrir un dispositivo serie en lugar de un socket TCP para el control CAT.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet CAT Control requiere una conexión de radio activa.
- Los enlaces simbólicos PTY solo se crean en Linux y macOS. Esta función no está disponible en Windows.
- El applet CAT Control está oculto de forma predeterminada. Debe activarlo antes de poder usarlo.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha para mostrar el applet CAT Control.
2. Haga clic en **Enable TTY**.

El botón se ilumina en verde cuando está activo. Cada fila de canal muestra inmediatamente su ruta de enlace simbólico. La ruta de cada canal se actualiza desde el marcador estático a la ruta activa una vez que el PTY está en funcionamiento.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Enable TTY** | Inicia o detiene los enlaces simbólicos PTY para los cuatro canales (A–D). | Off | — | — |
| **Enable TCP** | Inicia o detiene los servidores TCP de rigctld. Independiente del PTY. | Off | — | — |
| **Base** | Puerto TCP base para los servidores rigctld. Los canales se vinculan a Base, Base+1, Base+2, Base+3. No afecta las rutas PTY. | `4532` | 1024–65535 | `CatTcpPort` |
| Filas A/B/C/D | Muestran la insignia de cada canal, el estado del servidor TCP y la ruta de enlace simbólico PTY actual. Indicadores de solo lectura. | `(stopped)` | — | — |

Las rutas de los enlaces simbólicos PTY son fijas: `/tmp/AetherSDR-CAT-A`, `/tmp/AetherSDR-CAT-B`, `/tmp/AetherSDR-CAT-C` y `/tmp/AetherSDR-CAT-D`. Cada una corresponde al slice (canal) respectivo (canal A = slice 0, B = slice 1, y así sucesivamente).

## Consejos

- Abra su aplicación externa apuntando a la ruta del enlace simbólico que se muestra en la fila del canal, por ejemplo `/tmp/AetherSDR-CAT-A`. Trátela exactamente igual que un puerto serie de hardware.
- PTY y TCP pueden funcionar simultáneamente. Si su software admite ambos, puede activar **Enable TTY** y **Enable TCP** al mismo tiempo sin conflictos.
- Para iniciar los enlaces simbólicos PTY automáticamente cada vez que se inicie AetherSDR, use `Settings > Autostart CAT with AetherSDR`.

## Solución de problemas

- **El botón Enable TTY está presente, pero los enlaces simbólicos nunca aparecen** — Confirme que está ejecutando Linux o macOS. La creación de PTY no es compatible con Windows.
- **El software externo no puede abrir el enlace simbólico** — Verifique que AetherSDR esté conectado a la radio. El applet CAT Control requiere una conexión de radio activa; es posible que los PTY no funcionen mientras la radio esté desconectada.
- **La fila del canal sigue mostrando la ruta de marcador tras hacer clic en Enable TTY** — Es posible que el PTY no haya podido iniciarse. Intente hacer clic en **Enable TTY** nuevamente para desactivarlo y volver a activarlo.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar la radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
