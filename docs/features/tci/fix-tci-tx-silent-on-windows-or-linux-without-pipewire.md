# Solucionar el silencio en TX por TCI en Windows o Linux sin PipeWire

El audio de TX por TCI se enruta a través de una ranura de flujo `dax_tx` dedicada dentro del servidor TCI de AetherSDR, independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows e independiente de PipeWire. Esto significa que TX por TCI debería funcionar en todas las plataformas sin ninguna configuración especial. Esta página le ayuda a confirmar que el servidor TCI está configurado correctamente y que la ganancia de TX no es la causa del silencio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- La aplicación de terceros que envía audio TX por TCI (por ejemplo, un programa de modo digital) debe estar configurada para conectarse al servidor TCI de AetherSDR, no a SmartSDR DAX2 ni a ningún otro dispositivo de audio.
- Asegúrese de estar ejecutando AetherSDR v0.9.5.1 o posterior. Las versiones anteriores tenían una política de audio TX dependiente de la plataforma que podía bloquear el audio TX en Windows y Linux sin PipeWire.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha para abrir el applet del Servidor TCI.
2. Verifique la etiqueta de estado del servidor junto al campo **Port**.
   - Si muestra `(stopped)`, haga clic en **Enable** para iniciar el servidor.
   - Si muestra `(port in use)`, el puerto elegido ya está siendo utilizado por otro proceso. Cambie el valor en el campo **Port** a un puerto libre (rango válido: 1024–65535; predeterminado: `50001`), luego presione Enter y haga clic en **Enable**.
3. Confirme que la etiqueta de estado muestre `:<puerto> (N clients)` con al menos un cliente conectado. Si su aplicación TX no aparece como un cliente conectado, verifique su configuración de host y puerto TCI y asegúrese de que coincida con el valor del campo **Port**.
4. Observe la fila **TX** en el applet. Verifique la etiqueta de asignación de slice junto al medidor de TX.
   - Si muestra `—`, ningún slice está designado actualmente como slice TX. Use los controles de slice de la radio para asignar un slice TX.
   - Si muestra `Slice <letra>` (con la letra del slice renderizada en texto enriquecido, por ejemplo, coloreada o estilizada), la ruta TX está activa.
5. Arrastre el control deslizante **TX gain+meter** para confirmar que no está configurado en `0.0`. El valor predeterminado es `0.5` (rango válido: 0.0–1.0, persistido como `TciTxGain`). Un valor de `0.0` produce silencio independientemente de la plataforma.
6. Active el transmisor desde su aplicación de terceros y observe el medidor **TX gain+meter** para ver si hay movimiento de nivel. Si el medidor muestra actividad, el audio está llegando al servidor y la radio debería estar transmitiendo.

## Qué hace cada control

| Control            | Predeterminado | Rango válido |
|--------------------|----------------|--------------|
| **Port**           | `50001`        | 1024–65535   |
| **Enable**         | Off            | On / Off     |
| **TX gain+meter**  | `0.5`          | 0.0–1.0      |
| **RX1 gain+meter** | `0.5`          | 0.0–1.0      |
| **RX2 gain+meter** | `0.5`          | 0.0–1.0      |
| **RX3 gain+meter** | `0.5`          | 0.0–1.0      |
| **RX4 gain+meter** | `0.5`          | 0.0–1.0      |

## Consejos

- Los valores de puerto fuera del rango válido se restablecen automáticamente a `50001`.
- Si desea que el servidor TCI se inicie cada vez que se ejecute AetherSDR, active `Settings > Autostart TCI with AetherSDR`. Esto establece la marca `AutoStartTCI` y también activa **Enable** al inicio.
- El medidor TX utiliza un ataque rápido y una caída lenta, por lo que una transmisión breve mantendrá el medidor visiblemente elevado por un momento después de que el audio se detenga. La ausencia total de movimiento durante una transmisión activa confirma que el audio no está llegando desde el cliente.
- Las etiquetas de asignación de slice ahora admiten renderizado de texto enriquecido, por lo que las letras de los slices pueden aparecer con formato adicional (por ejemplo, color) para indicar las propiedades del slice.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve automáticamente a Off** — Otra aplicación está usando ese puerto. Ingrese un número de puerto diferente en el campo **Port**, presione Enter y haga clic en **Enable** nuevamente.
- **El estado muestra el puerto correcto y el recuento de clientes, pero la radio no transmite audio** — Confirme que la etiqueta del slice TX en la fila **TX** muestre `Slice <letra>` y no `—`. Si muestra `—`, designe un slice TX desde la interfaz principal. También confirme que el **TX gain+meter** esté por encima de `0.0`.
- **La aplicación de terceros no puede conectarse** — Verifique que la aplicación esté apuntando a `localhost` (o a la IP del host de AetherSDR) y que el número de puerto coincida con el campo **Port**. Confirme que ninguna regla de firewall esté bloqueando el puerto.
- **El medidor TX no muestra movimiento a pesar de que el cliente está conectado y transmitiendo** — Es posible que la aplicación cliente esté enviando audio a un dispositivo de audio del sistema en lugar de a través del WebSocket TCI. Verifique la salida de audio o la configuración de enrutamiento de audio TCI del cliente. AetherSDR no utiliza el dispositivo de audio DAX2 de Windows para TX por TCI; el audio debe llegar a través de la conexión WebSocket.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia de TX por TCI](adjust-tci-tx-gain.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
