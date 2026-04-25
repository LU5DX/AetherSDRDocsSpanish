# Habilitar CAT TCP para que N1MM, Log4OM y WSJT-X controlen el radio

El applet CAT Control ejecuta hasta cuatro servidores TCP compatibles con rigctld, uno por canal de slice (A–D). Habilitar TCP permite que software externo de registro y concursos, como N1MM+, Log4OM y WSJT-X, se conecte al radio a través de un puerto de red estándar.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet CAT requiere una conexión de radio activa.
- Decida qué puerto base utilizar. El valor predeterminado es `4532`. Los canales A, B, C y D se vinculan al puerto base, base+1, base+2 y base+3, respectivamente.
- Asegúrese de que ninguna otra aplicación (incluida una instancia independiente de rigctld) esté escuchando en esos puertos.

## Pasos

1. Haga clic en el botón **CAT** de la barra lateral derecha. Aparece el applet CAT Control.
2. Verifique el valor en el campo **Base**. El valor predeterminado es `4532`. Cámbielo si es necesario — los valores válidos son 1024–65535. Presione Enter o Tab para confirmar; los valores fuera de rango vuelven automáticamente a `4532`.
3. Haga clic en **Enable TCP**. El botón se resalta en verde cuando está activo.
4. Observe las filas de canales. Cada fila que esté en servicio muestra su puerto y el número de clientes conectados, por ejemplo `:4532 (0 clients)`. Las filas que no están en servicio muestran `(stopped)`.
5. En su software de registro o de modos digitales, configure la conexión CAT/control de radio para usar `localhost` (o la dirección IP del equipo con AetherSDR) y el puerto correspondiente al canal que desea controlar: el puerto base para el canal A, base+1 para el canal B, y así sucesivamente. Seleccione **Hamlib NET rigctl** o **rigctld** como tipo de radio si su software ofrece esa opción.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Enable TCP** | Desactivado | — | — | Inicia o detiene los cuatro servidores TCP rigctld. Al activarlo también se guarda el puerto base actual en `CatTcpPort`. |
| **Base** | `4532` | 1024–65535 | `CatTcpPort` | Establece el puerto TCP base. El canal A usa este puerto; B, C y D usan base+1, base+2 y base+3. Si los servidores ya están en ejecución, se reinician en los nuevos puertos inmediatamente después de confirmar el valor. |
| **Filas A/B/C/D** | `(stopped)` | — | — | Solo indicadores. Muestran el estado TCP actual de cada canal y el número de clientes conectados. |

## Consejos

- Cada canal corresponde a un slice. Si solo usa un slice, únicamente el canal A necesita ser conectado por su software; los demás servidores se ejecutan pero permanecen inactivos.
- Si cambia el puerto **Base** mientras **Enable TCP** ya está activo, los servidores se reinician automáticamente en los nuevos puertos. No es necesario desactivar y volver a activar **Enable TCP**.
- Para iniciar los servidores TCP cada vez que AetherSDR se inicia, use `Settings > Autostart rigctld with AetherSDR`.

## Solución de problemas

- **Enable TCP se activa pero la fila sigue mostrando `(stopped)`** — Es probable que otro proceso esté ocupando ese puerto. Detenga el proceso en conflicto o elija un puerto base diferente, luego desactive y reactive **Enable TCP**.
- **El software se conecta pero el radio no responde a los comandos** — Confirme que el software esté configurado como **Hamlib NET rigctl** (no como un tipo de radio serie por hardware) y que el número de puerto coincida con la fila del canal correspondiente al slice que desea controlar.
- **Los números de puerto son incorrectos después de reiniciar** — AetherSDR guarda el puerto base en `CatTcpPort` cuando confirma el valor o activa **Enable TCP**. Si el campo no fue confirmado antes de cerrar, el valor guardado puede diferir del que se mostraba. Vuelva a ingresar y confirme el puerto base.

## Relacionado

- [Descripción general de CAT Control](overview.md)
- [Iniciar automáticamente los servidores CAT con AetherSDR](autostart-cat-servers-with-aethersdr.md)
- [Cambiar el puerto TCP base](change-the-base-tcp-port.md)
- [Habilitar CAT PTY para que aplicaciones en Linux/macOS puedan abrir un puerto CAT estilo serie](enable-cat-pty-so-linux-macos-apps-can-open-a-serial-style-cat-port.md)
- [Configuración de modos digitales (FT8, WSJT-X, fldigi)](../../operating/digital-modes/digital-modes-setup.md)
