# Seleccionar una antena para la entrada B del ShackSwitch

Use el applet ShackSwitch para asignar una antena a la entrada B. La entrada B es el segundo puerto en dispositivos ShackSwitch multipuerto y no está disponible en los modelos de un solo puerto (R4).

## Antes de comenzar

- Debe descubrirse un dispositivo ShackSwitch en la LAN o conectarse mediante la pestaña Periféricos en Configuración de radio. El applet aparece automáticamente cuando un dispositivo está activo.
- El applet ShackSwitch debe estar visible en el Panel de applets. Si no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha.
- Confirme que la tarjeta INPUT B se muestra en el applet. Si está oculta, su dispositivo es un modelo de un solo puerto (R4) y la entrada B no está disponible.

## Pasos

1. Abra el Panel de applets y localice el applet ShackSwitch.
2. Busque la fila de antena que desea asignar a la entrada B. Los nombres de las antenas aparecen listados bajo la columna ANTENNA.
3. Haga clic en el botón **[B]** de esa fila de antena. El botón se resalta en naranja para confirmar la selección.
4. Confirme que la tarjeta INPUT B en la parte superior del applet se actualiza para mostrar el nombre de la antena seleccionada.

Para anular la selección de la antena actual de la entrada B, haga clic nuevamente en su botón **[B]** activo.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena asignada al puerto B. Oculta en dispositivos de un solo puerto (R4). | — |
| Botón **[B]** (por fila de antena) | Selecciona esta antena para la entrada B. Haga clic nuevamente para anular la selección. Parpadea en ámbar cuando el puerto A y el puerto B están asignados a la misma antena. | — |
| Selector de carga ficticia | Abre un menú para designar una antena como carga ficticia. Cuando está configurada, el puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |

## Consejos

- Si el botón **[B]** parpadea en ámbar después de seleccionar una antena, ambas entradas están ahora asignadas a la misma antena. Consulte [Resolver un conflicto de antena entre la entrada A y la entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md).
- Si hay una carga ficticia configurada y el puerto B se enruta automáticamente hacia ella, el botón **[B]** en la fila de la antena deseada parpadeará en ámbar y el botón **[B]** de la fila de la carga ficticia parpadeará en naranja. Para anular este comportamiento, elimine la asignación de la carga ficticia usando el selector de carga ficticia.

## Solución de problemas

- **La tarjeta INPUT B y los botones [B] no están visibles** — Su dispositivo ShackSwitch es un modelo de un solo puerto (R4). La entrada B no está disponible en ese hardware.
- **Hacer clic en [B] no tiene efecto** — La etiqueta de estado del applet muestra "Not connected". El dispositivo ShackSwitch no es accesible. Verifique que el dispositivo esté encendido y en el mismo segmento de red. Revise `SS_ManualIp` y `SS_ControlPort` en Configuración de radio si la detección automática no funciona.

## Relacionados

- [Seleccionar una antena para la entrada A del ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Resolver un conflicto de antena entre la entrada A y la entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web del ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
