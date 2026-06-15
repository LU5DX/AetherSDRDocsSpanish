# Resumen de Antenna Genius

El applet Antenna Genius le permite controlar un conmutador de antenas 4O3A Antenna Genius desde AetherSDR. Úselo para seleccionar antenas por puerto de radio, seguir automáticamente los cambios de banda y ver de un vistazo qué antenas tienen permiso para TX en la banda actual.

## Antes de comenzar

- El dispositivo Antenna Genius debe estar encendido y accesible, ya sea en la LAN local (para detección automática) o en una dirección IP conocida (para conexión manual).
- El applet está oculto hasta que se detecta un dispositivo o se realiza una conexión manual. Una vez visible, ábralo con el botón de bandeja "AG" en la barra lateral derecha.

## Cómo funciona

AetherSDR busca dispositivos Antenna Genius en la LAN mediante descubrimiento UDP. Cuando se encuentra un dispositivo, el applet aparece y se conecta automáticamente. Tenga en cuenta que los dispositivos ShackSwitch descubiertos en la LAN no se conectan automáticamente aquí; son gestionados por el applet ShackSwitch. Si su dispositivo está en una red remota, ingrese su dirección IP en el campo IP manual y presione Enter; la dirección se guarda como `AG_ManualIp` y se usa para conectarse al puerto 9007.

Una vez conectado, el applet muestra dos secciones de puerto — Puerto A y Puerto B — cada una con una fila de botones de antena poblados desde la lista de antenas del dispositivo. Al hacer clic en un botón de antena se selecciona esa antena en el puerto; al hacer clic nuevamente se deselecciona (establece la antena en 0). Si un dispositivo informa solo un puerto de radio, la sección Puerto B se oculta.

Los botones de antena están codificados por colores para mostrar el permiso de TX/RX en la banda actual:

- **Azul** — TX y RX permitidos.
- **Ámbar** — Solo RX en esta banda.
- **Opaco** — Sin permiso en la banda actual.

Una antena ya seleccionada en el otro puerto está deshabilitada y no se puede seleccionar en este puerto.

La etiqueta de estado en la parte superior del applet rastrea el ciclo de vida de la conexión, y los indicadores por puerto muestran la banda activa y el nombre de la antena seleccionada en tiempo real.

El applet ahora usa el tema del sistema para todos los elementos visuales: colores de botones, colores de etiquetas y líneas separadoras se adaptan al tema activo de AetherSDR.

Cuando está desconectado, la cuadrícula de botones de antena se borra por completo: todos los botones de antena se eliminan de la pantalla y las listas internas se vacían. Al reconectarse, la cuadrícula se reconstruye desde la lista de antenas del dispositivo solo después de que el modelo haya cargado la lista, evitando una cuadrícula en blanco durante el breve período antes de que llegue la respuesta de la lista de antenas.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Combo Dispositivo | Selecciona a qué dispositivo AG descubierto conectarse. Se llena mediante descubrimiento UDP. Auto-selecciona y conecta al primer dispositivo descubierto, siempre que no sea un ShackSwitch. | — | — |
| Conectar / Desconectar | Se conecta al dispositivo seleccionado, o a la IP manual si no hay ningún dispositivo descubierto seleccionado. Se convierte en "Desconectar" cuando está conectado. | Conectar | — |
| IP manual | Ingrese una dirección IPv4 o IPv6 y presione Enter para conectarse al puerto 9007. La dirección se guarda para sesiones futuras. Una entrada inválida muestra un estado rojo "Dirección IP inválida". | — | `AG_ManualIp` |
| Botones de antena Puerto A | Haga clic para seleccionar una antena en el Puerto A. Haga clic nuevamente para deseleccionar. Deshabilitado si la antena está en uso en el Puerto B. El color refleja el permiso de TX/RX (azul = TX+RX, ámbar = solo RX, opaco = sin permiso). | — | — |
| Puerto A AUTO | Alterne para habilitar el seguimiento de banda en el Puerto A. Cuando está activo, el AG cambia las antenas automáticamente a medida que la radio cambia de banda. | — | — |
| Botones de antena Puerto B | Mismo comportamiento que los botones de antena del Puerto A, para el Puerto B. Oculto si el dispositivo conectado tiene solo un puerto de radio. | — | — |
| Puerto B AUTO | Alterne para habilitar el seguimiento de banda en el Puerto B. | — | — |

### Indicadores de estado

| Indicador | Estados | Significado |
|---|---|---|
| Etiqueta de estado | No se encontró dispositivo / Dispositivo encontrado / Conectado — \<nombre\> v\<versión\> / Desconectado / Error: \<mensaje\> / Dirección IP inválida | Estado de descubrimiento y conexión del Antenna Genius. |
| Banda Puerto A | Nombre de banda o — | Banda activa en el Puerto A, derivada del informe del AG o la frecuencia de radio. |
| Antena Puerto A | Nombre de antena / \<ant\> TX:\<alt\> / \<ant\> [INHIBIR] / — | Antena seleccionada en el Puerto A. Rojo cuando transmite; naranja cuando TX se enruta a una antena alternativa o la inhibición está activa. |
| Banda Puerto B | Nombre de banda o — | Banda activa en el Puerto B. |
| Antena Puerto B | Nombre de antena / \<ant\> TX:\<alt\> / \<ant\> [INHIBIR] / — | Antena seleccionada en el Puerto B. Mismas reglas de color que el Puerto A. |

## Relacionado

- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
- [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md)
- [Seleccionar una antena para el Puerto A o Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Identificar qué antenas no pueden TX en la banda actual (ámbar u opaco)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Intercambiar radios que comparten el AG (antenas en uso por el otro puerto están bloqueadas)](swap-radios-that-share-the-ag-antennas-in-use-by-the-other-port-are-locked-out.md)
