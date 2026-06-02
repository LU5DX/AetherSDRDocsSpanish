# Applet de Antenna Genius

El applet de Antenna Genius (AG) controla un conmutador 4O3A Antenna Genius. Detecta dispositivos en la LAN, permite la conexión manual por IP y le permite seleccionar antenas por puerto de radio con codificación de colores de permisos TX/RX sensibles a la banda y modo AUTO.

## Abrir el Applet

Haga clic en el botón de la bandeja AG en la barra lateral derecha. El applet se abre como un panel estrecho.

## Conectarse a un Antenna Genius

El applet admite dos métodos de conexión:

- **Detección automática en la LAN**: El applet escucha las transmisiones de detección UDP. Cuando se encuentra un dispositivo, aparece en el combo Dispositivo y se selecciona y conecta automáticamente. La etiqueta de estado muestra "Dispositivo encontrado" durante la detección y luego "Conectado — <nombre> v<versión>" una vez conectado.

- **Conexión IP manual**: Si el dispositivo no está en la red local, ingrese su dirección IPv4 o IPv6 en el campo IP manual y presione Enter. El applet se conecta al puerto 9007. Las direcciones no válidas producen un estado "Dirección IP no válida" en rojo. La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura en el próximo inicio.

Para conectarse a una IP ingresada manualmente, presione Enter después de escribir la dirección. Para desconectarse, haga clic en el botón Desconectar (que reemplaza al botón Conectar cuando está conectado).

**Nota**: Los dispositivos ShackSwitch detectados en la LAN se excluyen de la conexión automática en el applet de Antenna Genius. Son manejados por el applet de ShackSwitch. Seleccione el dispositivo Antenna Genius correcto del combo Dispositivo y haga clic en Conectar, o ingrese su IP en IP manual y presione Enter.

## Seleccionar una Antena

Cada puerto de radio (Puerto A y Puerto B) tiene una fila de botones de antena. La lista de antenas se obtiene del dispositivo AG.

- **Para seleccionar una antena**: Haga clic en su botón en el puerto al que desea asignarla. El botón se ilumina.
- **Para anular la selección de una antena**: Vuelva a hacer clic en un botón iluminado. El puerto muestra sin antena ("—").
- **Si un botón está atenuado**: La antena ya está seleccionada en el otro puerto. Anule su selección allí primero.
- **Colores de los botones**: Azul = TX y RX permitidos en la banda actual. Ámbar = solo RX en la banda actual. Atenuado = sin permiso en la banda actual.

## Usar el Modo AUTO

Cada puerto tiene un botón de alternancia AUTO. Cuando está activado, el AG sigue automáticamente los cambios de banda de la radio, seleccionando la antena adecuada para cada banda.

- **Para activar AUTO**: Haga clic en el botón de alternancia AUTO del Puerto A o AUTO del Puerto B. El botón permanece en la posición de encendido.
- **Para desactivar AUTO**: Vuelva a hacer clic en el botón de alternancia.

Desactive AUTO en un puerto antes de reasignar antenas manualmente si necesita un control explícito. Si ambas radios están en modo AUTO, la resolución manual de bloqueo puede ser anulada inmediatamente por el siguiente cambio de banda.

## Leer los Indicadores

| Indicador | Muestra | Notas |
|---|---|---|
| Etiqueta de estado | "No se encontró dispositivo", "Dispositivo encontrado", "Conectado — <nombre> v<versión>", "Desconectado", "Error: <msg>" o "Dirección IP no válida" | El texto rojo indica un error o una IP no válida. |
| Banda del Puerto A | Nombre de la banda activa o "—" | Banda informada por el AG o derivada de la frecuencia. |
| Antena del Puerto A | Nombre de la antena seleccionada | Rojo durante TX, naranja cuando TX se enruta a una antena alternativa o se afirma la inhibición. Muestra "—" cuando no hay ninguna antena seleccionada. |
| Banda del Puerto B | Nombre de la banda activa o "—" | Igual que el Puerto A, para el Puerto B. |
| Antena del Puerto B | Nombre de la antena seleccionada | Igual que el Puerto A, para el Puerto B. |

## Intercambiar Radios Que Comparten el AG (Antenas en Uso por el Otro Puerto Están Bloqueadas)

Cuando dos radios comparten un Antenna Genius, cada radio se conecta a un puerto separado (Puerto A o Puerto B). Cualquier antena ya seleccionada en un puerto está bloqueada (su botón aparece atenuado) en el otro puerto. Esta sección explica cómo reasignar antenas entre puertos para que ninguna radio esté bloqueada.

### Antes de comenzar

- El applet de Antenna Genius debe estar visible. Si el botón de la bandeja AG está ausente, conéctese primero a su dispositivo; consulte [Detectar automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectarse manualmente a un AG a través de una red remota](../../getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe decir "Conectado — <nombre> v<versión>". No intente cambios de antena mientras esté desconectado.
- Su dispositivo AG debe informar dos puertos de radio. Si informa solo uno, la sección del Puerto B está oculta y este procedimiento no aplica.

### Pasos

1. Haga clic en el botón de la bandeja AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Observe los botones de antena del Puerto A y los botones de antena del Puerto B. Los botones atenuados en un puerto ya están seleccionados en el otro puerto y no se pueden elegir hasta que se liberen.
3. Para liberar una antena bloqueada, haga clic en su botón actualmente iluminado en el puerto que la tiene. Hacer clic en un botón de antena seleccionada por segunda vez anula su selección (establece ese puerto sin antena). El botón vuelve a su estado sin iluminar.
4. Una vez que la antena se anula en el puerto que la tenía, su botón se vuelve activo en el otro puerto.
5. Haga clic en el botón ahora disponible de la antena en el puerto al que desea asignarla. El botón se ilumina y el nombre de la antena aparece en el indicador de antena del puerto en la parte superior de la sección de ese puerto.
6. Confirme la asignación: el indicador de antena junto a "Puerto A" o "Puerto B" muestra el nombre de la antena. Si la antena admite TX en la banda actual, el botón es azul; si solo RX en la banda actual, es ámbar.

### Consejos

- **Anular la selección antes de reasignar**: debe liberar la antena de su puerto actual antes de que el botón esté disponible en el otro puerto. No hay intercambio por arrastrar y soltar; el paso de liberación es obligatorio.
- Si ambas radios están en modo AUTO, el AG seguirá la banda de cada radio de forma independiente. En ese caso, la resolución manual de bloqueo puede ser anulada inmediatamente por el siguiente cambio de banda. Desactive AUTO en el puerto correspondiente antes de realizar cambios manuales.

### Solución de Problemas

- **Un botón de antena permanece atenuado incluso después de hacer clic en el botón del otro puerto para anular su selección**: confirme que la anulación de selección surtió efecto verificando que el indicador de antena para el otro puerto ahora muestre "—". Si el indicador aún muestra el nombre de la antena, es posible que el clic no se haya registrado; vuelva a hacer clic en el botón iluminado del otro puerto una vez más.
- **La sección del Puerto B no está visible**: el dispositivo AG conectado informa solo un puerto de radio. El uso compartido del Puerto B no está disponible en dispositivos de un solo puerto.
- **La etiqueta de estado muestra "Desconectado" o "Error: <msg>"**: los botones de antena no se pueden cambiar mientras esté desconectado. Vuelva a conectarse usando Conectar o volviendo a ingresar la IP en IP manual y presionando Enter. Las direcciones no válidas producen un estado "Dirección IP no válida" en rojo. La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura en el próximo inicio.
- **Aparece un dispositivo ShackSwitch en el combo Dispositivo pero no se conecta automáticamente**: los dispositivos ShackSwitch detectados en la LAN se excluyen de la conexión automática en el applet de Antenna Genius. Son manejados por el applet de ShackSwitch. Seleccione el dispositivo Antenna Genius correcto del combo Dispositivo y haga clic en Conectar, o ingrese su IP en IP manual y presione Enter.

## Soporte de Temas

A partir de v26.6.1, el applet de Antenna Genius es totalmente compatible con temas a través del sistema ThemeManager. Todos los colores de los widgets (fondos, bordes, texto, colores de acento e indicadores de estado) ahora se derivan del tema activo en lugar de estar codificados. Esto significa que la apariencia del applet se adapta automáticamente cuando cambia de tema en AetherSDR.

## Relacionados

- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden TX en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Activar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Detectar automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
