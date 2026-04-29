# Conectarse a una radio en la LAN local

Use esta página para conectar AetherSDR a un FLEX-8600 que se encuentre en la misma LAN que su computadora. AetherSDR descubre la radio automáticamente mediante mDNS — no se requiere dirección IP.

## Antes de comenzar

- El FLEX-8600 debe estar encendido y accesible en la misma red local que su computadora.
- AetherSDR debe estar en ejecución. La pantalla de conexión aparece automáticamente antes de que se conecte cualquier radio, o después de una desconexión.
- Confirme que ninguna VPN, aislamiento de Wi-Fi de invitados o firewall del equipo esté bloqueando el tráfico mDNS/descubrimiento en su red.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente al iniciar la aplicación. También puede abrirla en cualquier momento desde `Settings > Connect to Radio...`.
2. Haga clic en **Local**. Este es el modo predeterminado, por lo que es posible que ya esté seleccionado.
3. Espere unos segundos a que se complete la lista **Available radios**. AetherSDR escucha los paquetes de descubrimiento de la radio; este proceso normalmente concluye en pocos segundos.
4. Haga clic en su radio en la lista **Available radios** para resaltarla.
5. Haga clic en **Connect Selected Radio**.

La etiqueta de estado en la parte inferior del panel se actualiza mostrando los estados de conexión en curso y luego conectado a medida que se establece el enlace.

## Qué hace cada control

| Control | Función | Configuración persistente |
|---|---|---|
| **Local / SmartLink / Manual** | Cambia el panel entre los tres modos de conexión. El modo predeterminado en el primer inicio es **Local**. | `ConnectionMode` |
| **Available radios** | Lista las radios FLEX-8600 descubiertas en la LAN mediante mDNS. Se completa automáticamente; no requiere ninguna entrada. | — |
| **Connect Selected Radio** | Se conecta a la radio resaltada. Se habilita únicamente cuando hay una radio seleccionada en la lista. | — |
| **No local radios found yet** | Aviso que se muestra cuando el descubrimiento no devuelve resultados. Reemplaza la lista hasta que se encuentra una radio o se reintenta el descubrimiento. | — |
| **Retry Discovery** | Vuelve a ejecutar el descubrimiento en la LAN de inmediato. Aparece dentro del aviso de estado vacío. | — |
| **Connect by IP** | Acceso directo al modo **Manual**. Aparece dentro del aviso de estado vacío. | `ConnectionMode` |
| **Remote with SmartLink** | Acceso directo al modo **SmartLink**. Aparece dentro del aviso de estado vacío. | `ConnectionMode` |
| **Open Network Diagnostics** | Abre la ventana de diagnóstico de red. Aparece dentro del aviso de estado vacío. | — |

## Consejos

- Si la lista tarda en completarse, espere al menos 10–15 segundos antes de usar **Retry Discovery**. La radio envía paquetes de descubrimiento periódicos y es posible que AetherSDR aún no haya recibido el primero.
- Si su computadora tiene múltiples interfaces de red, AetherSDR podría estar escuchando en la incorrecta. Si el descubrimiento falla de manera consistente, considere cambiar al modo **Manual** y especificar la interfaz con **Advanced: Source path**.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — Los paquetes de descubrimiento de la radio no están llegando a AetherSDR. Causas frecuentes: la radio y la computadora están en distintas VLANs o subredes, el aislamiento de punto de acceso Wi-Fi de invitados está habilitado, o una VPN por software está interceptando el tráfico multicast. Haga clic en **Open Network Diagnostics** para obtener detalles, o cambie al modo **Manual** si conoce la dirección IP de la radio.
- **Connect Selected Radio aparece en gris** — No hay ninguna radio seleccionada en la lista **Available radios**. Haga clic primero en una radio de la lista.
- **La etiqueta de estado muestra un error después de hacer clic en Connect Selected Radio** — La radio fue descubierta, pero la conexión TCP falló. Verifique que ningún firewall esté bloqueando el puerto del protocolo SmartSDR y que ningún otro cliente compatible con SmartSDR mantenga la conexión exclusiva.

## Relacionados

- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a una radio remota mediante SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Seleccionar la interfaz de red local para una conexión manual](pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](../../features/connection/enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectarse de la radio actual](disconnect-from-the-current-radio.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
