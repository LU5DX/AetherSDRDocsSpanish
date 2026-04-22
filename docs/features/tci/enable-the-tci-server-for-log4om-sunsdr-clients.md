# Habilitar el servidor TCI para clientes Log4OM / SunSDR

Inicie el servidor TCI WebSocket integrado para que software de registro y SDR de terceros, como Log4OM o las herramientas SunSDR, puedan leer y controlar la radio mediante el protocolo TCI.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet TCI requiere una conexión de radio activa.
- El applet TCI debe estar visible. Si no lo ve en el panel de applets, haga clic en el botón TCI del panel lateral derecho para mostrarlo.

## Pasos

1. Haga clic en el botón TCI del panel lateral derecho para abrir el applet TCI Server.
2. Verifique el campo Port. El valor predeterminado es `50001`. Cámbielo ahora si ese puerto ya está en uso en su sistema — consulte [Cambiar el puerto TCI](change-the-tci-port.md).
3. Haga clic en Enable.
4. Confirme que el servidor se inició: el indicador de estado junto a Enable cambia de `(stopped)` a `:<port> (0 clients)`.
5. En su software de terceros (Log4OM, herramienta SunSDR, etc.), ingrese `localhost` y el número de puerto que aparece en el indicador de estado. Una vez que el cliente se conecte, el estado se actualizará a `:<port> (1 clients)` o superior.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Port | Establece el puerto TCP en el que escucha el servidor TCI WebSocket. Si se cambia el valor mientras Enable está activo, el servidor se reinicia automáticamente. Los valores fuera de rango se ajustan a `50001`. | `50001` | 1024–65535 | `TciPort` |
| Enable | Inicia o detiene el servidor TCI. | Off | — | — |
| Server status | Muestra el estado actual del servidor y la cantidad de clientes conectados. Se vuelve rojo y muestra `(port in use)` si el enlace falla. | `(stopped)` | `(stopped)`, `:<port> (N clients)`, `(port in use)` | — |
| RX1–RX4 gain+meter | Medidor de nivel y control deslizante de ganancia combinados para cada canal RX de TCI. Arrastre para ajustar la ganancia. La letra del slice (canal de recepción) asignado a cada canal se muestra a la izquierda del medidor. | 0.5 | 0.0–1.0 | `TciRxGain1`, `TciRxGain2`, `TciRxGain3`, `TciRxGain4` |
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal TX de TCI. La letra del slice TX activo se muestra a la izquierda del medidor. | 0.5 | 0.0–1.0 | `TciTxGain` |
| RX/TX slice-assignment labels | Indicadores que muestran qué slice controla cada fila RX o TX. Muestra `—` cuando no hay ningún slice asignado a ese canal. | `—` | `—` o `Slice <letter>` | — |

## Consejos

- Para que el servidor TCI se inicie automáticamente cada vez que se lance AetherSDR, habilite `Settings > Autostart TCI with AetherSDR`. Consulte [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md).
- Las asignaciones de canales RX siguen el mapeo de canales DAX. Si un canal muestra `—`, asigne un canal DAX al slice correspondiente en la configuración de la radio.

## Solución de problemas

- **Enable vuelve a Off y el estado muestra `(port in use)`** — Otra aplicación ya está enlazada a ese puerto. Cambie el valor de Port a un puerto libre (1024–65535) y haga clic en Enable nuevamente.
- **El estado permanece en `(stopped)` después de hacer clic en Enable** — Confirme que la radio esté conectada. El servidor TCI requiere una conexión de radio activa para iniciarse.
- **El software de terceros no puede conectarse** — Verifique que el número de puerto en el cliente coincida con el campo Port en AetherSDR. Compruebe que su firewall permita conexiones en ese puerto.

## Relacionado

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
