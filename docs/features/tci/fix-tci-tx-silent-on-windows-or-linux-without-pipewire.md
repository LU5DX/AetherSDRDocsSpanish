# Solucionar el silencio en TCI TX en Windows o Linux sin PipeWire

El audio TCI TX se enruta a través de un slot de flujo `dax_tx` dedicado dentro del servidor TCI de AetherSDR, independiente de la ruta de audio del dispositivo SmartSDR DAX2 de Windows e independiente de PipeWire. Esto significa que TCI TX debería funcionar en todas las plataformas sin ninguna configuración especial. Esta página le ayuda a confirmar que el servidor TCI está configurado correctamente y que la ganancia de TX no es la causa del silencio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión de radio activa.
- La aplicación de terceros que envía audio TCI TX (por ejemplo, un programa de modos digitales) debe estar configurada para conectarse al servidor TCI de AetherSDR, no a SmartSDR DAX2 ni a ningún otro dispositivo de audio.
- Asegúrese de estar ejecutando AetherSDR v0.9.5.1 o posterior. Las versiones anteriores tenían una política de audio TX dependiente de la plataforma que podía bloquear el audio TX en Windows y Linux sin PipeWire.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet TCI Server.
2. Verifique la etiqueta de estado del servidor junto al campo Port.
   - Si muestra `(stopped)`, haga clic en **Enable** para iniciar el servidor.
   - Si muestra `(port in use)`, el puerto seleccionado ya está en uso por otro proceso. Cambie el valor en el campo **Port** a un puerto libre (rango válido: 1024–65535; valor predeterminado: `50001`), luego presione Enter y haga clic en **Enable**.
3. Confirme que la etiqueta de estado muestre `:<port> (N clients)` con al menos un cliente conectado. Si su aplicación TX no aparece como cliente conectado, verifique su configuración de host y puerto TCI y asegúrese de que coincidan con el valor del campo **Port**.
4. Observe la fila **TX** en el applet. Verifique la etiqueta de asignación de slice (receptor virtual) junto al medidor TX.
   - Si muestra `—`, ningún slice está designado actualmente como slice TX. Use los controles de slice del radio para asignar un slice TX.
   - Si muestra `Slice <letter>`, la ruta TX está activa.
5. Arrastre el control deslizante **TX gain+meter** para confirmar que no esté en `0.0`. El valor predeterminado es `0.5` (rango válido: 0.0–1.0, guardado como `TciTxGain`). Un valor de `0.0` produce silencio independientemente de la plataforma.
6. Active el transmisor desde su aplicación de terceros y observe el **TX gain+meter** para detectar movimiento de nivel. Si el medidor muestra actividad, el audio está llegando al servidor y el radio debería estar transmitiendo.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave guardada |
|---|---|---|---|
| **Port** | `50001` | 1024–65535 | `TciPort` |
| **Enable** | Off | On / Off | — |
| **TX gain+meter** | `0.5` | 0.0–1.0 | `TciTxGain` |
| **RX1 gain+meter** | `0.5` | 0.0–1.0 | `TciRxGain1` |
| **RX2 gain+meter** | `0.5` | 0.0–1.0 | `TciRxGain2` |
| **RX3 gain+meter** | `0.5` | 0.0–1.0 | `TciRxGain3` |
| **RX4 gain+meter** | `0.5` | 0.0–1.0 | `TciRxGain4` |

## Consejos

- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.
- Si desea que el servidor TCI se inicie cada vez que AetherSDR se ejecuta, active `Settings > Autostart TCI with AetherSDR`. Esto establece el indicador `AutoStartTCI` y también marca **Enable** al inicio.
- El medidor TX utiliza suavizado de ataque rápido y decaimiento lento, por lo que una transmisión breve mantendrá el medidor visiblemente elevado por un momento después de que el audio se detenga. La ausencia total de movimiento durante una transmisión con la clave activa confirma que el audio no está llegando desde el cliente.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a desactivarse** — Otra aplicación está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port**, presione Enter y haga clic en **Enable** nuevamente.
- **El estado muestra el puerto y el número de clientes correctos, pero el radio no transmite audio** — Confirme que la etiqueta de slice TX en la fila **TX** muestre `Slice <letter>` y no `—`. Si muestra `—`, designe un slice TX desde la interfaz principal. Confirme también que el **TX gain+meter** esté por encima de `0.0`.
- **La aplicación de terceros no puede conectarse** — Verifique que la aplicación apunte a `localhost` (o a la IP del host de AetherSDR) y que el número de puerto coincida con el campo **Port**. Confirme que ninguna regla de firewall esté bloqueando el puerto.
- **El medidor TX no muestra movimiento aunque el cliente esté conectado y con la clave activa** — Es posible que la aplicación cliente esté enviando audio a un dispositivo de audio del sistema en lugar de hacerlo a través del WebSocket TCI. Verifique la salida de audio del cliente o la configuración de enrutamiento de audio TCI. AetherSDR no utiliza el dispositivo de audio DAX2 de Windows para TCI TX; el audio debe llegar a través de la conexión WebSocket.

## Relacionados

- [Activar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
