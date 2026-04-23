# Reintentar el descubrimiento cuando no aparecen radios

Cuando AetherSDR se abre en modo local y no aparece ninguna radio en la lista, use el aviso "No local radios found yet" para volver a ejecutar el descubrimiento o cambiar a una ruta de conexión alternativa.

## Antes de comenzar

- El radio Flex está encendido y conectado a la misma LAN que su computadora.
- AetherSDR está en ejecución y muestra el panel "Connect to a Radio". Si no es visible, haga clic en `Settings > Connect to Radio...`.

## Pasos

1. Abra el panel "Connect to a Radio". Si ya hay una radio conectada, aparecerá después de desconectarla.
2. Haga clic en `Local` (etiquetado como **On This Network**) si aún no está seleccionado. Este es el modo predeterminado (`ConnectionMode` = `LocalMode`).
3. Espere unos segundos. AetherSDR escucha paquetes de descubrimiento automáticamente. Si no se encuentran radios, el aviso **No local radios found yet** aparece en lugar de la lista de radios.
4. Haga clic en **Retry Discovery** para volver a ejecutar el descubrimiento en la LAN de inmediato.
5. Si ahora aparece una radio en la lista **Available radios**, selecciónela y haga clic en **Connect Selected Radio**.
6. Si no aparece ninguna radio después de reintentar, use uno de los botones alternativos del aviso:
   - Haga clic en **Connect by IP** para ir a la página Manual e ingresar la dirección IP de la radio directamente.
   - Haga clic en **Remote with SmartLink** para ir a la página de SmartLink y conectarse a través de internet.
   - Haga clic en **Open Network Diagnostics** para inspeccionar el estado de la red e identificar qué está bloqueando el descubrimiento.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **On This Network** | Botón de modo | Selecciona el modo de descubrimiento en la LAN local. | `ConnectionMode` |
| **No local radios found yet** | Indicador | Se muestra cuando el descubrimiento no devuelve resultados. | — |
| **Retry Discovery** | Botón | Vuelve a ejecutar el descubrimiento en la LAN sin reiniciar la aplicación. | — |
| **Available radios** | Lista | Muestra las radios encontradas mediante descubrimiento mDNS/Flex. | — |
| **Connect Selected Radio** | Botón | Se conecta a la radio resaltada en la lista. | — |
| **Connect by IP** | Botón | Cambia a la página Manual para ingresar la IP directamente. | `ManualRadioIp` |
| **Remote with SmartLink** | Botón | Cambia a la página de SmartLink. | `SmartLinkEmail` |
| **Open Network Diagnostics** | Botón | Abre el diálogo de diagnóstico de red. | — |

## Consejos

- El descubrimiento depende de paquetes mDNS y de descubrimiento Flex. Las redes Wi-Fi de invitados, el software VPN y las reglas del firewall suelen bloquear estos paquetes, lo que provoca que el aviso **No local radios found yet** aparezca incluso cuando la radio es accesible. Si reintentar no ayuda, verifique que su computadora y la radio estén en la misma subred y que ninguna VPN esté redirigiendo el tráfico fuera de la interfaz local.
- Si la radio está en una subred diferente o detrás de una VPN, **Retry Discovery** no tendrá éxito. Use **Connect by IP** en su lugar.

## Solución de problemas

- **Retry Discovery no tiene efecto y la lista permanece vacía** — Es probable que la radio y la computadora estén en segmentos de red diferentes, o que un firewall esté bloqueando el tráfico de descubrimiento. Cambie a **Connect by IP** e ingrese la dirección IP de la radio, o conéctese a través de SmartLink si la radio se encuentra en una ubicación remota.
- **La radio apareció una vez pero desapareció de la lista** — Una interrupción de red descartó el paquete de descubrimiento. Haga clic en **Retry Discovery**. Si esto se repite, verifique si hay cambios de dirección IP en la radio o una conexión Wi-Fi inestable.

## Relacionados

- [Conectarse a una radio en la LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a una radio remota a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Iniciar sesión en SmartLink para ver radios remotas](log-in-to-smartlink-to-see-remote-radios.md)
- [Seleccionar la interfaz de red local para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
