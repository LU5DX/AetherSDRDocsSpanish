# Seleccionar una antena para la Entrada B del ShackSwitch

Utilice el applet ShackSwitch para asignar una antena a la Entrada B. La Entrada B es el segundo puerto en dispositivos ShackSwitch multipuerto y no está disponible en modelos de un solo puerto (R4).

## Antes de comenzar

- Debe descubrir un dispositivo ShackSwitch en la LAN o conectarlo mediante la pestaña Periféricos en Configuración de Radio. El applet aparece automáticamente cuando un dispositivo está activo.
- El applet ShackSwitch debe estar visible en el Panel de Applets. Si no está visible, haga clic en el botón de la bandeja SS en la barra lateral derecha.
- Confirme que la tarjeta INPUT B se muestre en el applet. Si está oculta, su dispositivo es un modelo de un solo puerto (R4) y la Entrada B no está disponible.

## Pasos

1. Abra el Panel de Applets y localice el applet ShackSwitch.
2. Busque la fila de la antena que desea asignar a la Entrada B. Los nombres de las antenas aparecen bajo la columna ANTENNA.
3. Haga clic en el botón **[B]** de esa fila de antena. El botón se resalta en naranja para confirmar la selección.
4. Confirme que la tarjeta INPUT B en la parte superior del applet se actualice para mostrar el nombre de la antena seleccionada.

Para anular la selección de la antena actual de la Entrada B, vuelva a hacer clic en su botón **[B]** activo.

## Función de cada control

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | — |
| Tarjeta INPUT B | Muestra la banda y el nombre de la antena asignados al Puerto B. Resaltada en naranja. Oculto en dispositivos de un solo puerto (R4). | — |
| Botón **[A]** (por fila de antena) | Selecciona esta antena para la Entrada A. Vuelva a hacer clic para anular la selección. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena (conflicto). | — |
| Botón **[B]** (por fila de antena) | Selecciona esta antena para la Entrada B. Vuelva a hacer clic para anular la selección. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena. Cuando se configura una carga ficticia y el Puerto B se enruta automáticamente allí, el botón **[B]** de la fila prevista parpadea en ámbar y la fila de la carga ficticia parpadea en naranja. | — |
| Selector de carga ficticia | Selecciona o anula la selección de una antena como carga ficticia. Cuando está configurada, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Botón de configuración | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza la dirección del peer activo cuando está conectado; de lo contrario, usa `SS_ManualIp`. El puerto se determina mediante `SS_WebPort`, el puerto web de la baliza o el valor predeterminado 5000. | — |

## Consejos

- Si el botón **[B]** parpadea en ámbar después de seleccionar una antena, ambas entradas están ahora asignadas a la misma antena. Consulte [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md).
- Si se configura una carga ficticia y el Puerto B se enruta automáticamente allí, el botón **[B]** de la fila de antena prevista parpadea en ámbar y el botón **[B]** de la fila de la carga ficticia parpadea en naranja. Para anular este comportamiento, elimine la asignación de la carga ficticia mediante el selector de carga ficticia.

## Solución de problemas

- **La tarjeta INPUT B y los botones [B] no están visibles** — Su dispositivo ShackSwitch es un modelo de un solo puerto (R4). La Entrada B no está disponible en ese hardware.
- **Hacer clic en [B] no tiene efecto** — La etiqueta de estado del applet muestra "No conectado". El dispositivo ShackSwitch no es accesible. Verifique que el dispositivo esté encendido y en el mismo segmento de red. Revise `SS_ManualIp` y `SS_ControlPort` en Configuración de Radio si la detección automática no funciona.

## Relacionados

- [Seleccionar una antena para la Entrada A del ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web del ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
