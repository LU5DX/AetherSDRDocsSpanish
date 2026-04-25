# Habilitar el servidor TCI para clientes Log4OM / SunSDR

El servidor TCI permite que programas de registro y de modos digitales de terceros, como Log4OM y las herramientas de SunSDR, se conecten a AetherSDR mediante el protocolo TCI basado en WebSocket. Habilite el servidor aquí para que esos clientes puedan leer la frecuencia, el modo y los datos de audio de la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Confirme que ninguna otra aplicación esté escuchando en el puerto 50001 (o en el puerto que desee utilizar).

## Pasos

1. Haga clic en el botón **TCI** del panel lateral derecho. Aparece el panel del applet TCI Server.
2. Verifique el campo **Port**. El valor predeterminado es `50001`. Cámbielo si es necesario; el rango válido es 1024–65535. Los valores fuera de ese rango vuelven automáticamente a `50001`.
3. Haga clic en **Enable**. El botón se ilumina en verde cuando el servidor está en ejecución.
4. Observe el indicador de estado del servidor junto a **Enable**. Cambia de `(stopped)` a `:<port> (N clients)` una vez que el servidor está activo. Cuando un cliente se conecta, el contador de clientes aumenta.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Port | `50001` | 1024–65535 | `TciPort` | Establece el puerto WebSocket. Si se cambia el puerto mientras el servidor está en ejecución, el servidor se reinicia en el nuevo puerto. Los valores fuera de rango vuelven a `50001`. |
| Enable | Off | On / Off | — | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el interruptor regresa a off y el estado muestra `(port in use)` en rojo. |
| RX1–RX4 gain+meter | 0.5 | 0.0–1.0 | `TciRxGain1`–`TciRxGain4` | Medidor y deslizador combinados. Arrastre para ajustar la ganancia TCI de recepción de cada canal. La letra del slice (canal de recepción) que aparece junto a cada fila refleja la asignación de canal DAX para ese slice. |
| TX gain+meter | 0.5 | 0.0–1.0 | `TciTxGain` | Medidor y deslizador combinados. Arrastre para ajustar la ganancia TCI de transmisión. La letra del slice que aparece refleja el slice actualmente asignado como TX. |
| Etiquetas de asignación de slice RX/TX | — | `—` o `Slice <letter>` | — | Indicadores de solo lectura. Muestran qué slice controla cada fila de RX o TX según la asignación de canal DAX. |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se lanza AetherSDR, habilite `Settings > Autostart TCI with AetherSDR` en lugar de hacer clic en **Enable** en cada sesión.
- Si el estado permanece en `(stopped)` inmediatamente después de hacer clic en **Enable**, es probable que el puerto esté en uso. Cambie el valor de **Port** y haga clic en **Enable** nuevamente.

## Resolución de problemas

- **El estado muestra `(port in use)` en rojo tras hacer clic en Enable** — Otro proceso está vinculado a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El contador de clientes permanece en 0 después de iniciar el servidor** — Confirme que el programa cliente apunta a la dirección de host y al puerto correctos. Verifique que un cortafuegos no esté bloqueando el puerto.
- **Las etiquetas de slice RX/TX muestran `—`** — Ningún slice tiene asignado un canal DAX. Asigne un canal DAX al slice en la configuración de slices de la radio. La etiqueta se actualiza automáticamente una vez que se asigna un canal.

## Relacionados

- [Descripción general del servidor TCI](overview.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia TCI de RX por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TCI de TX](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
