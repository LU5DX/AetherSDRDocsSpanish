# Seleccionar una antena para la Entrada B de ShackSwitch

Use el applet de ShackSwitch para asignar una antena a la Entrada B. La Entrada B es el segundo puerto en los dispositivos ShackSwitch de varios puertos y no está disponible en los modelos de un solo puerto (R4).

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar detectado en la LAN o conectado mediante la pestaña Peripherals en Radio Setup. El applet aparece automáticamente cuando un dispositivo está activo.
- El applet de ShackSwitch debe estar visible en el Panel de Applets. Si no está visible, haga clic en el botón SS del panel lateral derecho.
- Confirme que la tarjeta INPUT B se muestra en el applet. Si está oculta, su dispositivo es un modelo de un solo puerto (R4) y la Entrada B no está disponible.

## Pasos

1. Abra el Panel de Applets y localice el applet de ShackSwitch.
2. Encuentre la fila de antena que desea asignar a la Entrada B. Los nombres de las antenas aparecen en la columna ANTENNA.
3. Haga clic en el botón **[B]** de esa fila de antena. El botón se resalta en naranja para confirmar la selección.
4. Confirme que la tarjeta INPUT B en la parte superior del applet se actualiza para mostrar el nombre de la antena seleccionada.

Para deseleccionar la antena activa de la Entrada B, haga clic nuevamente en su botón **[B]** activo.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena asignada al Puerto B. Oculta en dispositivos de un solo puerto (R4). | — |
| Botón **[B]** (por fila de antena) | Selecciona esta antena para la Entrada B. Haga clic de nuevo para deseleccionar. Parpadea en ámbar cuando el Puerto A y el Puerto B están asignados a la misma antena. | — |
| Selector de carga ficticia | Abre un menú para designar una antena como carga ficticia (dummy load). Cuando está configurado, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |

## Consejos

- Si el botón **[B]** parpadea en ámbar después de seleccionar una antena, ambas entradas están asignadas a la misma antena. Consulte [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md).
- Si hay una carga ficticia configurada y el Puerto B se enruta automáticamente hacia ella, el botón **[B]** de la fila de su antena deseada parpadea en ámbar y el botón **[B]** de la fila de la carga ficticia parpadea en naranja. Para anular este comportamiento, elimine la asignación de la carga ficticia usando el Dummy load selector.

## Solución de problemas

- **La tarjeta INPUT B y los botones [B] no están visibles** — Su dispositivo ShackSwitch es un modelo de un solo puerto (R4). La Entrada B no está disponible en ese hardware.
- **Hacer clic en [B] no tiene efecto** — La etiqueta de estado del applet muestra "Not connected". El dispositivo ShackSwitch no es accesible. Verifique que el dispositivo esté encendido y en el mismo segmento de red. Compruebe `SS_ManualIp` y `SS_ControlPort` en Radio Setup si el descubrimiento automático no funciona.

## Relacionados

- [Seleccionar una antena para la Entrada A de ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Abrir la interfaz de configuración web de ShackSwitch](open-the-shackswitch-web-configuration-interface.md)
