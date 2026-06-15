# Applet de Antenna Genius

El applet de Antenna Genius (AG) controla un conmutador 4O3A Antenna Genius. Descubre dispositivos en la LAN, permite la conexión manual por IP y le permite seleccionar antenas por puerto de radio con codificación cromática de permisos de TX/RX consciente de la banda y modo AUTO.

## Abrir el Applet

Haga clic en el botón de la bandeja AG en la barra lateral derecha. El applet se abre como un panel estrecho.

## Conectarse a un Antenna Genius

El applet admite dos métodos de conexión:

- **Detección automática en la LAN**: El applet escucha las difusiones de descubrimiento UDP. Cuando se encuentra un dispositivo, aparece en el combo Dispositivo y se selecciona y conecta automáticamente. La etiqueta de estado muestra "Dispositivo encontrado" durante el descubrimiento y luego "Conectado — <nombre> v<versión>" una vez conectado.

- **Conexión IP manual**: Si el dispositivo no está en la red local, introduzca su dirección IPv4 o IPv6 en el campo IP manual y presione Enter. El applet se conecta al puerto 9007. Las direcciones no válidas producen un estado rojo de "Dirección IP no válida". La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura en el próximo inicio.

Para conectarse a una IP introducida manualmente, presione Enter después de escribir la dirección. Para desconectarse, haga clic en el botón Desconectar (que reemplaza al botón Conectar cuando está conectado).

**Nota**: Los dispositivos ShackSwitch descubiertos en la LAN se excluyen de la conexión automática en el applet de Antenna Genius. Estos son gestionados por el applet de ShackSwitch. Seleccione el dispositivo Antenna Genius correcto del combo Dispositivo y haga clic en Conectar, o introduzca su IP en IP manual y presione Enter.

## Seleccionar una Antena

Cada puerto de radio (Puerto A y Puerto B) tiene una fila de botones de antena. La lista de antenas se obtiene del dispositivo AG.

- **Para seleccionar una antena**: Haga clic en su botón en el puerto al que desea asignarla. El botón se ilumina.
- **Para deseleccionar una antena**: Haga clic en un botón iluminado nuevamente. El puerto no muestra ninguna antena ("—").
- **Si un botón está atenuado**: La antena ya está seleccionada en el otro puerto. Deseléctela allí primero.
- **Colores de los botones**: Azul = TX y RX permitidos en la banda actual. Ámbar = Solo RX en la banda actual. Atenuado = Sin permiso en la banda actual.

## Usar el Modo AUTO

Cada puerto tiene un botón de activación/desactivación AUTO. Cuando está habilitado, el AG sigue los cambios de banda de la radio automáticamente, seleccionando la antena apropiada para cada banda.

- **Para habilitar AUTO**: Haga clic en el botón de activación AUTO del Puerto A o Puerto B. El botón permanece en la posición de encendido.
- **Para deshabilitar AUTO**: Haga clic en el botón de activación nuevamente.

Deshabilite AUTO en un puerto antes de reasignar antenas manualmente si necesita un control explícito. Si ambas radios están en modo AUTO, la resolución de bloqueo manual puede ser anulada inmediatamente por el siguiente cambio de banda.

## Leer los Indicadores

| Indicador | Muestra | Notas |
|---|---|---|
| Etiqueta de estado | "Ningún dispositivo encontrado", "Dispositivo encontrado", "Conectado — <nombre> v<versión>", "Desconectado", "Error: <msg>" o "Dirección IP no válida" | El texto rojo indica un error o una IP no válida. |
| Banda del Puerto A | Nombre de la banda activa o "—" | Banda reportada por el AG o derivada de la frecuencia. |
| Antena del Puerto A | Nombre de la antena seleccionada | Rojo durante TX, naranja cuando TX se enruta a una antena alternativa o se afirma la inhibición. Muestra "—" cuando no hay ninguna antena seleccionada. |
| Banda del Puerto B | Nombre de la banda activa o "—" | Igual que el Puerto A, para el Puerto B. |
| Antena del Puerto B | Nombre de la antena seleccionada | Igual que el Puerto A, para el Puerto B. |

## Intercambiar Radios Que Comparten el AG (Las Antenas en Uso por el Otro Puerto Están Bloqueadas)

Cuando dos radios comparten un Antenna Genius, cada radio se conecta a un puerto separado (Puerto A o Puerto B). Cualquier antena ya seleccionada en un puerto está bloqueada (su botón está atenuado) en el otro puerto. Esta sección explica cómo reasignar antenas entre puertos para que ninguna radio quede bloqueada.

### Antes de comenzar

- El applet de Antenna Genius debe estar visible. Si el botón de la bandeja AG está ausente, conéctese primero a su dispositivo; consulte [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md) o [Conectarse manualmente a un AG a través de una red remota](../..//getting-started/setup/manually-connect-to-an-ag-over-a-remote-network.md).
- La etiqueta de estado debe mostrar "Conectado — <nombre> v<versión>". No intente cambios de antena mientras esté desconectado.
- Su dispositivo AG debe reportar dos puertos de radio. Si solo reporta uno, la sección del Puerto B está oculta y este procedimiento no aplica.

### Pasos

1. Haga clic en el botón de la bandeja AG en la barra lateral derecha para abrir el applet de Antenna Genius.
2. Observe los botones de antena del Puerto A y del Puerto B. Los botones atenuados en un puerto ya están seleccionados en el otro puerto y no se pueden elegir hasta que se liberen.
3. Para liberar una antena bloqueada, haga clic en su botón actualmente iluminado en el puerto que la tiene. Al hacer clic en un botón de antena seleccionado por segunda vez se deselecciona (establece ese puerto sin antena). El botón vuelve a su estado no iluminado.
4. Una vez que la antena se deselecciona en el puerto que la tenía, su botón se vuelve activo en el otro puerto.
5. Haga clic en el botón de antena ahora disponible en el puerto al que desea asignarla. El botón se ilumina y el nombre de la antena aparece en el indicador de antena del puerto en la parte superior de esa sección del puerto.
6. Confirme la asignación: el indicador de antena junto a "Puerto A" o "Puerto B" muestra el nombre de la antena. Si la antena admite TX en la banda actual, el botón es azul; si solo RX en la banda actual, es ámbar.

### Consejos

- **Deseleccione antes de reasignar**: debe liberar la antena de su puerto actual antes de que el botón esté disponible en el otro puerto. No hay intercambio de arrastrar y soltar: el paso de liberación es necesario.
- Si ambas radios están en modo AUTO, el AG seguirá la banda de cada radio de forma independiente. En ese caso, la resolución de bloqueo manual puede ser anulada inmediatamente por el siguiente cambio de banda. Deshabilite AUTO en el puerto relevante antes de realizar cambios manuales.

### Solución de problemas

- **Un botón de antena permanece atenuado incluso después de hacer clic en el botón del otro puerto para deseleccionarlo**: confirme que la deselección surtió efecto verificando que el indicador de antena del otro puerto ahora muestre "—". Si el indicador aún muestra el nombre de la antena, es posible que el clic no se haya registrado; haga clic en el botón iluminado del otro puerto una vez más.
- **La sección del Puerto B no es visible**: el dispositivo AG conectado reporta solo un puerto de radio. El uso compartido del Puerto B no está disponible en dispositivos de un solo puerto.
- **La etiqueta de estado muestra "Desconectado" o "Error: <msg>"**: los botones de antena no se pueden cambiar mientras esté desconectado. Vuelva a conectarse usando Conectar o reintroduciendo la IP en IP manual y presionando Enter. Las direcciones no válidas producen un estado rojo de "Dirección IP no válida". La última IP manual utilizada se almacena en `AG_ManualIp` y se restaura en el próximo inicio.
- **Aparece un dispositivo ShackSwitch en el combo Dispositivo pero no se conecta automáticamente**: los dispositivos ShackSwitch descubiertos en la LAN se excluyen de la conexión automática en el applet de Antenna Genius. Estos son gestionados por el applet de ShackSwitch. Seleccione el dispositivo Antenna Genius correcto del combo Dispositivo y haga clic en Conectar, o introduzca su IP en IP manual y presione Enter.

## Al Desconectarse se Limpian los Botones de Antena

Cuando se desconecta de un dispositivo Antenna Genius, la cuadrícula de botones de antena se limpia inmediatamente. Todos los botones de antena desaparecen de las secciones del Puerto A y del Puerto B. Este es un comportamiento esperado: la lista de antenas solo está disponible mientras está conectado al dispositivo.

Cuando se vuelve a conectar, los botones de antena se reconstruyen a partir de la lista de antenas del dispositivo tan pronto como llega la respuesta. Si la lista aún no está disponible, los botones existentes permanecen en su lugar hasta que lleguen los datos nuevos.

## Soporte de Temas

A partir de la v26.6.1, el applet de Antenna Genius es totalmente compatible con temas a través del sistema ThemeManager. Todos los colores de los widgets (fondos, bordes, texto, colores de acento e indicadores de estado) ahora se derivan del tema activo en lugar de estar codificados de forma fija. Esto significa que la apariencia del applet se adapta automáticamente cuando cambia de tema en AetherSDR.

## Relacionado

- [Seleccionar una antena para el Puerto A o el Puerto B](select-an-antenna-for-port-a-or-port-b.md)
- [Identificar qué antenas no pueden transmitir en la banda actual (ámbar o atenuado)](spot-which-antennas-cannot-tx-on-the-current-band-amber-or-dim.md)
- [Habilitar el modo AUTO para que el AG siga los cambios de banda de la radio](enable-auto-mode-so-the-ag-follows-radio-band-changes.md)
- [Descubrir automáticamente un Antenna Genius en la LAN](auto-discover-an-antenna-genius-on-the-lan.md)
