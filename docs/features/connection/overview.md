# Descripción general del panel Connect to a Radio

El panel Connect to a Radio es el punto de partida para que AetherSDR se comunique con su FLEX-8600. Aparece automáticamente antes de que se conecte cualquier radio y cada vez que se desconecta. Úselo para elegir cómo AetherSDR accede al radio: en la red local, a través de SmartLink o mediante una dirección IP directa.

## Antes de comenzar

- AetherSDR está instalado y en ejecución.
- Su FLEX-8600 está encendido y es accesible por al menos una de las tres rutas de conexión descritas a continuación.

## Cómo funciona

El panel presenta tres modos de conexión como tarjetas seleccionables en la parte superior. Al hacer clic en una tarjeta, el área inferior cambia para mostrar los controles de ese modo. AetherSDR guarda el último modo utilizado en `ConnectionMode` y lo restaura en el siguiente inicio.

**On This Network** es el modo predeterminado. AetherSDR usa descubrimiento mDNS/Flex para encontrar radios en la misma LAN de forma automática. Los radios encontrados aparecen en la lista "Available radios". Si no se encuentra ninguno, el panel cambia a un aviso de estado vacío titulado "No local radios found yet" y ofrece accesos directos para reintentar o cambiar de modo.

**Remote with SmartLink** conecta a un radio en una ubicación remota a través de internet mediante el servicio SmartLink de FlexRadio. Inicie sesión con su cuenta de FlexRadio y los radios remotos disponibles aparecerán en la lista "Remote radios".

**Connect by IP** es para túneles VPN, redes enrutadas o cualquier situación en la que ya conozca la dirección IP del radio. Escriba la dirección directamente y, opcionalmente, elija qué interfaz de red local usar para la conexión.

Puede volver a abrir este panel en cualquier momento seleccionando `Settings > Connect to Radio...` desde la barra de menú.

## Qué hace cada control

### Selección de modo

| Control | Función | Configuración guardada |
|---|---|---|
| On This Network | Cambia al modo de descubrimiento en LAN. Modo predeterminado. | `ConnectionMode` |
| Remote with SmartLink | Cambia al inicio de sesión en SmartLink y la lista de radios remotos. | `ConnectionMode` |
| Connect by IP | Cambia a la entrada manual de IP. | `ConnectionMode` |

### Modo On This Network

| Control | Función |
|---|---|
| Available radios | Lista los radios FLEX-8600 descubiertos en la red local. |
| Connect Selected Radio | Conecta al radio resaltado en la lista. Deshabilitado hasta que se seleccione un radio. |
| No local radios found yet | Aviso que se muestra cuando el descubrimiento no ha devuelto resultados. |
| Retry Discovery | Vuelve a ejecutar el descubrimiento en LAN. |
| Remote with SmartLink | Acceso directo que cambia directamente al modo SmartLink. |
| Connect by IP | Acceso directo que cambia directamente al modo de IP manual. |
| Open Network Diagnostics | Abre el diálogo de diagnóstico de red. |

### Modo Remote with SmartLink

| Control | Función | Configuración guardada |
|---|---|---|
| SmartLink account: Email | La dirección de correo electrónico de su cuenta de FlexRadio. | `SmartLinkEmail` |
| SmartLink account: Password | La contraseña de su cuenta de FlexRadio. No se guarda entre sesiones. | — |
| Sign In | Autentica con SmartLink usando las credenciales ingresadas. | — |
| Sign Out | Cierra la sesión de SmartLink actual. | — |
| Remote radios | Lista los radios disponibles para su cuenta de SmartLink después de iniciar sesión. | — |
| Connect Remote Radio | Inicia una conexión WAN al radio remoto seleccionado. | — |

### Modo Connect by IP

| Control | Función | Configuración guardada |
|---|---|---|
| Radio IP address | La dirección IP del radio al que conectarse. | `ManualRadioIp` |
| Advanced: Source path | Selecciona qué interfaz de red local usar para la conexión. | `ManualBindSource` |
| Use low bandwidth mode | Habilita flujos de audio y datos a tasa reducida para enlaces lentos o congestionados. | `LowBandwidthMode` |
| Connect by IP (manual) | Inicia el intento de conexión a la dirección ingresada. | — |
| Network Diagnostics | Abre el diálogo de diagnóstico de red desde la página de IP manual. | — |

### Indicadores de estado

| Indicador | Significado |
|---|---|
| Status label | Muestra el estado actual de la conexión: buscando, conectando, conectado o un mensaje de error. |
| Manual result label | Muestra el resultado después de que AetherSDR sondea una dirección IP ingresada manualmente. |
| Source warning label | Advierte cuando la interfaz de red seleccionada en "Advanced: Source path" está desactualizada o no es accesible. |

### Desconexión

| Control | Función |
|---|---|
| Disconnect | Termina la conexión actual con el radio y regresa a este panel. |

## Sugerencias

- Si aparece "No local radios found yet", las causas más comunes son el aislamiento de red en Wi-Fi de invitados, software VPN o un cortafuegos que bloquea los paquetes mDNS. Haga clic en "Open Network Diagnostics" para investigar, o cambie a "Connect by IP" si el radio está en una red enrutada o VPN.
- La contraseña de SmartLink nunca se guarda en disco. Deberá ingresarla nuevamente después de reiniciar AetherSDR.
- El "Source warning label" aparece cuando la interfaz almacenada en `ManualBindSource` ya no está presente o no es accesible — por ejemplo, tras una reconfiguración de red. Seleccione una interfaz actual en "Advanced: Source path" antes de conectarse.

## Temas relacionados

- [Conectarse a un radio en LAN local](../../getting-started/setup/connect-to-a-local-lan-radio.md)
- [Reintentar el descubrimiento cuando no aparecen radios](retry-discovery-when-no-radios-appear.md)
- [Iniciar sesión en SmartLink para ver radios remotos](log-in-to-smartlink-to-see-remote-radios.md)
- [Conectarse a un radio remoto a través de SmartLink](../../getting-started/setup/connect-to-a-remote-radio-through-smartlink.md)
- [Conectarse por IP a través de una VPN o red enrutada](../../getting-started/setup/connect-by-ip-across-a-vpn-or-routed-network.md)
- [Elegir la interfaz de red local para una conexión manual](../../getting-started/setup/pick-the-local-network-interface-used-for-a-manual-connection.md)
- [Habilitar el modo de bajo ancho de banda para enlaces lentos](enable-low-bandwidth-mode-for-slow-links.md)
- [Desconectarse del radio actual](../../getting-started/setup/disconnect-from-the-current-radio.md)
