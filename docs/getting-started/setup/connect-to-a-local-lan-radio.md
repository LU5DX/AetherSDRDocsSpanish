# Conectarse a una radio en la red LAN local

Abra la pantalla de conexión de AetherSDR y conéctese a un radio Flex que esté en la misma LAN que su computadora. Este es el método recomendado para usuarios nuevos en una estación doméstica o de club.

## Antes de comenzar

- El radio Flex está encendido y conectado a la misma red local que su computadora.
- No hay VPN ni aislamiento de Wi-Fi para invitados activo entre la radio y la computadora. Cualquiera de los dos puede bloquear el descubrimiento mDNS.
- AetherSDR está instalado y en ejecución.

## Pasos

1. Abra la pantalla de conexión. Aparece automáticamente en la ventana principal antes de conectar una radio. También puede acceder a ella en cualquier momento mediante `Settings > Connect to Radio...`.
2. Haga clic en **On This Network**. Esto selecciona el modo de descubrimiento en LAN local y establece `ConnectionMode` en `LocalMode`.
3. Espere unos segundos a que se complete la lista **Available radios**. AetherSDR descubre las radios automáticamente mediante mDNS.
4. Haga clic en su radio en la lista **Available radios** para seleccionarla.
5. Haga clic en **Connect Selected Radio**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **On This Network** | Botón de modo | Cambia a la página de descubrimiento en LAN local. Modo predeterminado. | `ConnectionMode` |
| **Remote with SmartLink** | Botón de modo | Cambia a la página de SmartLink. | `ConnectionMode` |
| **Connect by IP** | Botón de modo | Cambia a la página manual/por IP. | `ConnectionMode` |
| **Available radios** | Lista | Muestra las radios radio Flex encontradas en la LAN mediante mDNS. Se actualiza automáticamente. | — |
| **Connect Selected Radio** | Botón | Se conecta a la radio seleccionada. Deshabilitado hasta que se seleccione una radio. | — |
| **No local radios found yet** | Indicador | Se muestra en lugar de la lista cuando el descubrimiento no ha encontrado ninguna radio. | — |
| **Retry Discovery** | Botón | Vuelve a ejecutar el descubrimiento en LAN de inmediato. Visible solo cuando la lista está vacía. | — |
| **Open Network Diagnostics** | Botón | Abre el cuadro de diálogo de diagnóstico de red. Visible solo cuando la lista está vacía. | — |

## Consejos

- Si la lista permanece vacía por más de 10–15 segundos, haga clic en **Retry Discovery** antes de cambiar cualquier configuración de red.
- El software cliente de VPN que se ejecuta en la misma máquina es una causa frecuente de fallo en el descubrimiento, incluso cuando la radio está en la red local. Intente deshabilitar la VPN y luego haga clic en **Retry Discovery**.
- Si su radio está en una subred diferente o solo es accesible a través de una VPN, use **Connect by IP** en lugar de **On This Network**.

## Solución de problemas

- **Aparece "No local radios found yet" y no desaparece** — El descubrimiento mDNS está siendo bloqueado. Verifique si hay aislamiento de Wi-Fi para invitados en su punto de acceso, un firewall del sistema que bloquee UDP, o software VPN que redirija el tráfico. Haga clic en **Open Network Diagnostics** para inspeccionar la ruta de red, o cambie a **Connect by IP** si conoce la dirección IP de la radio.
- **Connect Selected Radio aparece en gris** — No hay ninguna radio seleccionada en la lista **Available radios**. Primero haga clic en una radio de la lista.

## Relacionados

- [Reintentar el descubrimiento cuando no aparecen radios](../../features/connection/retry-discovery-when-no-radios-appear.md)
- [Conectarse por IP a través de una VPN o red enrutada](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Conectarse a una radio remota mediante SmartLink](connect-to-a-remote-radio-through-smartlink.md)
- [Desconectarse de la radio actual](disconnect-from-the-current-radio.md)
- [Realizar su primer QSO con AetherSDR](../tutorials/first-qso.md)
