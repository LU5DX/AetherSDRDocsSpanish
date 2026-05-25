# Solucionar TX silencioso por TCI en Windows o Linux sin PipeWire

El audio TX de TCI se enruta a través de un slot de flujo `dax_tx` dedicado dentro del servidor TCI de AetherSDR, independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows y de PipeWire. Esto significa que el TX de TCI debería funcionar en todas las plataformas sin necesidad de configuración especial. Esta página lo ayuda a confirmar que el servidor TCI está configurado correctamente y que la ganancia TX no es la causa del silencio.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- La aplicación de terceros que envía audio TX por TCI (por ejemplo, un programa de modos digitales) debe estar configurada para conectarse al servidor TCI de AetherSDR, no a SmartSDR DAX2 ni a ningún otro dispositivo de audio.
- Asegúrese de estar ejecutando AetherSDR v0.9.5.1 o posterior. Las versiones anteriores tenían una política de audio TX dependiente de la plataforma que podía bloquear el audio TX en Windows y Linux sin PipeWire.

## Pasos

1. Haga clic en el botón de la bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Verifique la etiqueta de estado del servidor junto al campo **Port**.
   - Si muestra `(stopped)`, haga clic en **Enable** para iniciar el servidor.
   - Si muestra `(port in use)`, el puerto elegido ya está en uso por otro proceso. Cambie el valor en el campo **Port** a un puerto libre (rango válido: 1024–65535; predeterminado: `50001`), luego presione Enter y haga clic en **Enable**.
3. Confirme que la etiqueta de estado muestre `:<puerto> (N clientes)` con al menos un cliente conectado. Si su aplicación TX no aparece como cliente conectado, revise su configuración de host y puerto TCI y asegúrese de que coincidan con el valor del campo **Port**.
4. Observe la fila **TX** en el applet. Verifique la etiqueta de asignación de slice junto al medidor TX.
   - Si muestra `—`, no hay ningún slice designado actualmente como slice TX. Use los controles de slice de la radio para asignar un slice TX.
   - Si muestra `Slice <letra>` (con la letra del slice renderizada en texto enriquecido, por ejemplo, coloreada o estilizada), la ruta TX está activa.
5. Arrastre el control deslizante **TX gain+meter** para confirmar que no está en `0.0`. El valor predeterminado es `0.5` (rango válido: 0.0–1.0, persistido como `TciTxGain`). Un valor de `0.0` produce silencio independientemente de la plataforma.
6. Active el transmisor desde su aplicación de terceros y observe el medidor **TX gain+meter** para detectar movimiento de nivel. Si el medidor muestra actividad, el audio está llegando al servidor y la radio debería estar transmitiendo.
7. Si usa un modo digital que requiere fidelidad de tono bit exacta, haga clic derecho en el control deslizante **TX gain+meter** para abrir el menú de manejo de desbordamiento TX. Seleccione el modo deseado para controlar cómo se procesan las muestras fuera de rango (>1.0) provenientes de clientes TCI.

## Qué hace cada control

| Control                        | Predeterminado | Rango válido | Comportamiento |
|--------------------------------|---------|-------------|----------|
| **Port**                       | `50001` | 1024–65535 | Cambiar el puerto reinicia el servidor si está habilitado. Los valores fuera de rango se ajustan a 50001. |
| **Enable**                     | Off     | On / Off    | Inicia o detiene el servidor TCI; emite tciToggled. Si la vinculación falla, el interruptor vuelve a Off y el estado muestra '(port in use)'. |
| **TX gain+meter**              | `0.5`   | 0.0–1.0     | Arrastrar establece la ganancia TX de TCI y emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX. |
| **RX1 gain+meter**             | `0.5`   | 0.0–1.0     | Medidor/control deslizante combinado; arrastrar establece la ganancia RX de TCI para el canal 1 y emite tciRxGainChanged. Se persiste como `TciRxGain1`. |
| **RX2 gain+meter**             | `0.5`   | 0.0–1.0     | Medidor/control deslizante combinado; arrastrar establece la ganancia RX de TCI para el canal 2 y emite tciRxGainChanged. Se persiste como `TciRxGain2`. |
| **RX3 gain+meter**             | `0.5`   | 0.0–1.0     | Medidor/control deslizante combinado; arrastrar establece la ganancia RX de TCI para el canal 3 y emite tciRxGainChanged. Se persiste como `TciRxGain3`. |
| **RX4 gain+meter**             | `0.5`   | 0.0–1.0     | Medidor/control deslizante combinado; arrastrar establece la ganancia RX de TCI para el canal 4 y emite tciRxGainChanged. Se persiste como `TciRxGain4`. |
| **Modo de desbordamiento TX (clic derecho)** | Clip | Clip (0), NaNGuard (1), Measure (2) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged. Nuevo en v26.5.3. |

## Modos de manejo de desbordamiento TX

Haga clic derecho en el control deslizante **TX gain+meter** para abrir el menú contextual de manejo de desbordamiento TX. Esto controla cómo se procesan las muestras fuera de rango (>1.0) de clientes TCI de modos digitales antes de llegar a la radio. El valor predeterminado es **Clip** para mantener la compatibilidad con versiones anteriores.

| Modo | Valor | Descripción |
|------|-------|-------------|
| **Clip (saturación ±1.0)** | 0 | Recorta con límite duro los picos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos pero protege la conversión a int16 posterior. |
| **NaN guard (solo poner a cero NaN/Inf)** | 1 | Pasa las muestras bit exactas; solo pone a cero valores patológicos NaN/Inf. Preserva la fidelidad del tono de modos digitales; los flotantes fuera de rango llegan a la radio. |
| **Measure only (bypass real)** | 2 | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 posterior aún recorta en la ruta DAX nativa de la radio. |

## Indicadores

| Indicador | Estados posibles | Significado |
|-----------|-----------------|---------|
| **Estado del servidor** | `(stopped)` | El servidor no está en ejecución. |
| | `:<puerto> (N clientes)` | El servidor se está ejecutando en el puerto especificado con N clientes conectados. |
| | `(port in use)` | El puerto elegido ya está en uso por otro proceso. |
| **Etiquetas de asignación de slice RX/TX** | `—` | No hay ningún slice asignado actualmente. |
| | `Slice <letra>` | El slice especificado está asignado a este canal. |

## Consejos

- Los valores de puerto fuera de rango se ajustan automáticamente a `50001`.
- Si desea que el servidor TCI se inicie cada vez que se lance AetherSDR, habilite `Settings > Autostart TCI with AetherSDR`. Esto establece la bandera `AutoStartTCI` y también activa **Enable** al inicio.
- El medidor TX utiliza un suavizado de ataque rápido y caída lenta, por lo que una transmisión breve mantendrá el medidor visiblemente elevado durante un momento después de que el audio se detenga. Si no hay movimiento durante una transmisión activada, confirma que el audio no está llegando desde el cliente.
- Las etiquetas de asignación de slice ahora admiten renderizado de texto enriquecido, por lo que las letras de slice pueden aparecer con formato adicional (por ejemplo, color) para indicar propiedades del slice.
- Para modos digitales que requieren fidelidad de tono bit exacta, use los modos **NaN guard** o **Measure only** para evitar la distorsión armónica por recorte.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a Off** — Otra aplicación está usando ese puerto. Ingrese un número de puerto diferente en el campo **Port**, presione Enter y haga clic en **Enable** nuevamente.
- **El estado muestra el puerto correcto y la cantidad de clientes, pero la radio no transmite audio** — Confirme que la etiqueta de slice TX en la fila **TX** muestre `Slice <letra>` y no `—`. Si muestra `—`, designe un slice TX desde la interfaz principal. También confirme que **TX gain+meter** esté por encima de `0.0`.
- **La aplicación de terceros no puede conectarse** — Verifique que la aplicación esté apuntando a `localhost` (o la IP del host de AetherSDR) y que el número de puerto coincida con el campo **Port**. Confirme que ninguna regla de firewall esté bloqueando el puerto.
- **El medidor TX no muestra movimiento a pesar de que el cliente está conectado y activado** — La aplicación cliente puede estar enviando audio a un dispositivo de audio del sistema en lugar de a través del WebSocket de TCI. Revise la configuración de salida de audio o enrutamiento de audio TCI del cliente. AetherSDR no utiliza el dispositivo de audio DAX2 de Windows para TX por TCI; el audio debe llegar a través de la conexión WebSocket.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al lanzar](autostart-tci-on-launch.md)
