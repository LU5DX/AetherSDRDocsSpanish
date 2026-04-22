# Inicio automático de servidores CAT con AetherSDR

Configure AetherSDR para iniciar los servidores TCP CAT y los puertos TTY automáticamente cada vez que se ejecute, de modo que el software externo de registro y concursos se conecte sin intervención manual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio antes de que el applet CAT sea funcional. El inicio automático lanza los servidores al arrancar, pero estos requieren una conexión con el radio para operar.
- Decida si necesita TCP, TTY (PTY) o ambos. TTY solo está disponible en Linux y macOS.
- Confirme que su puerto base (`CatTcpPort`, predeterminado `4532`) esté configurado correctamente antes de habilitar el inicio automático. Consulte [Cambiar el puerto TCP base](change-the-base-tcp-port.md).

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Para iniciar automáticamente los servidores TCP, haga clic en `Autostart CAT with AetherSDR`. Aparece una marca de verificación junto al elemento cuando está habilitado.
3. Reinicie AetherSDR. En el siguiente arranque, AetherSDR inicia los cuatro servidores TCP rigctld en los puertos `Base` hasta `Base+3` automáticamente, como si hubiera hecho clic en `Enable TCP` manualmente.

Para verificar que los servidores se iniciaron, abra el applet CAT:

4. Haga clic en el botón `CAT` de la bandeja en la barra lateral derecha. Se abre el applet CAT Control.
5. Revise cada fila de canal (A, B, C, D). Un servidor en ejecución muestra `:<port> (0 clients)` o `:<port> (N clients)` en lugar de `(stopped)`.

## Qué hace cada control

| Control | Tipo | Predeterminado | Comportamiento | Clave de configuración |
|---|---|---|---|---|
| `Enable TCP` | Botón de alternancia | Desactivado | Inicia o detiene los cuatro servidores TCP rigctld en `Base`, `Base+1`, `Base+2`, `Base+3`. | — |
| `Enable TTY` | Botón de alternancia | Desactivado | Inicia o detiene los cuatro enlaces simbólicos PTY en `/tmp/AetherSDR-CAT-A` hasta `/tmp/AetherSDR-CAT-D`. Solo en Linux/macOS. | — |
| `Base` | Campo de texto | `4532` | Establece el puerto TCP base. Rango válido: 1024–65535. Los valores fuera de rango vuelven a `4532`. Reinicia los servidores en ejecución al cambiar el valor. | `CatTcpPort` |
| Filas de canal A/B/C/D | Indicador | `(stopped)` | Muestra el estado TCP y la ruta PTY por canal. El estado TCP muestra el puerto y el número de clientes conectados cuando está en ejecución. | — |

## Consejos

- `Settings > Autostart CAT with AetherSDR` controla el inicio automático de TCP. Esto es independiente de `Settings > Autostart rigctld with AetherSDR`, que es un mecanismo de servidor CAT distinto.
- El inicio automático solo inicia los servidores; no abre el panel del applet CAT automáticamente. Ábralo manualmente con el botón `CAT` de la bandeja cuando necesite verificar el estado.
- Si cambia el puerto base en el campo `Base` mientras los servidores están en ejecución, los cuatro servidores se reinician inmediatamente en los nuevos puertos sin necesidad de desactivar y volver a activar `Enable TCP`.

## Solución de problemas

- **Las filas de canal siguen mostrando `(stopped)` después del inicio automático** — La conexión con el radio no se estableció antes de que AetherSDR intentara iniciar los servidores. Verifique que el radio sea accesible y vuelva a conectarlo. Luego haga clic en `Enable TCP` manualmente en el applet CAT para iniciar los servidores.
- **El elemento de menú `Autostart CAT with AetherSDR` no aparece o está desactivado** — Este elemento controla el CAT basado en PTY en Linux y macOS. Verifique que esté ejecutando una compilación para una plataforma compatible.
- **Conflicto de puerto al iniciar** — Otra aplicación ya está utilizando uno de los cuatro puertos. Cambie `Base` a un rango de puertos disponible antes de habilitar el inicio automático.

## Temas relacionados

- [Habilitar CAT TCP para que N1MM, Log4OM, WSJT-X puedan controlar el radio](enable-cat-tcp-so-n1mm-log4om-wsjt-x-can-control-the-radio.md)
- [Habilitar CAT PTY para que aplicaciones de Linux/macOS puedan abrir un puerto CAT de estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Verificar cuántos clientes externos están conectados a cada canal](../../getting-started/setup/check-how-many-external-clients-are-connected-to-each-channel.md)
