# Referencia del applet del servidor TCI

El applet **TCI Server** ejecuta un servidor WebSocket TCI de estilo Expert para que software de registro, modos digitales y SDR de terceros (Log4OM, herramientas SunSDR, etc.) puedan leer y controlar la radio mediante el protocolo TCI. El audio de TX por TCI se recibe a través del WebSocket y se introduce en una ranura de flujo `dax_tx` dedicada que es independiente de la ruta del dispositivo de audio DAX2 de Windows SmartSDR, por lo que el TX por TCI funciona en todas las plataformas, incluidos Windows y Linux, sin PipeWire.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- La aplicación de terceros que envía audio de TX por TCI (por ejemplo, un programa de modos digitales) debe configurarse para conectarse al servidor TCI de AetherSDR, no a SmartSDR DAX2 ni a ningún otro dispositivo de audio.
- Asegúrese de estar ejecutando AetherSDR v0.9.5.1 o posterior. Las versiones anteriores tenían una política de audio de TX dependiente de la plataforma que podía bloquear el audio de TX en Windows y Linux sin PipeWire.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Verifique la etiqueta de estado del servidor junto al campo **Port**.
   - Si indica `(stopped)`, haga clic en **Enable** para iniciar el servidor. El texto del botón cambia a **Enabled** cuando el servidor está en ejecución.
   - Si indica `(port in use)`, el puerto elegido ya está en uso por otro proceso. Cambie el valor del campo **Port** a un puerto libre (rango válido: 1024–65535; predeterminado: `50001`), presione Intro y haga clic en **Enable**.
3. Confirme que la etiqueta de estado muestra `:<puerto> (N clients)` con al menos un cliente conectado. Si su aplicación de TX no aparece como cliente conectado, verifique su configuración de host y puerto TCI y asegúrese de que coincida con el valor del campo **Port**.
4. Observe la fila **TX** en el applet. Verifique la etiqueta de asignación de slice junto al medidor de TX.
   - Si muestra `—`, no hay ningún slice designado como slice de TX. Use los controles de slice de la radio para asignar un slice de TX.
   - Si muestra `Slice <letra>` (con la letra del slice renderizada en texto enriquecido, por ejemplo, con color o estilo), la ruta de TX está activa.
5. Arrastre el control deslizante **TX gain+meter** para confirmar que no está en `0.0`. El valor predeterminado es `0.5` (rango válido: 0.0–1.0, persistido como `TciTxGain`). Un valor de `0.0` produce silencio independientemente de la plataforma.
6. Keyee el transmisor desde su aplicación de terceros y observe el **TX gain+meter** para ver movimiento de nivel. Si el medidor muestra actividad, el audio está llegando al servidor y la radio debería estar transmitiendo.
7. Si utiliza un modo digital que requiere fidelidad de tono bit-exacta, haga clic con el botón derecho en el control deslizante **TX gain+meter** para abrir el menú de manejo de desbordamiento de TX. Seleccione el modo deseado para controlar cómo se procesan las muestras fuera de rango (>1.0) de los clientes TCI.

## Qué hace cada control

| Control                            | Predeterminado | Rango válido |
|------------------------------------|---------|-------------|
| **Port**                           | `50001` | 1024–65535  |
| **Enable**                         | Off     | On / Off    |
| **TX gain+meter**                  | `0.5`   | 0.0–1.0     |
| **RX1 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX2 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX3 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX4 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX5 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX6 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX7 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **RX8 gain+meter**                 | `0.5`   | 0.0–1.0     |
| **TX overflow mode (clic derecho)** | Clip    | Clip (0), NaNGuard (1), Measure (2) |

El botón **Enable** muestra **Enabled** cuando el servidor está en ejecución y **Disabled** cuando está detenido. Si la opción **AutoStartTCI** está habilitada en Settings, el botón se inicia como **Enabled** al abrir el programa.

Las filas **RX** muestran el índice del receptor (trx) como un índice posicional de slice limitado por la capacidad de slices de la radio (hasta 8 en una Flex-6700). Las filas por encima del número máximo de slices de la radio se ocultan automáticamente. Cada fila RX muestra la etiqueta de asignación de slice que refleja el mapeo de canales DAX — los canales RX de TCI 1–8 transportan los mismos canales DAX que el applet DAX, con el audio distribuido tanto a DaxBridge como a TciServer.

## Modos de manejo de desbordamiento de TX

Haga clic con el botón derecho en el control deslizante **TX gain+meter** para abrir el menú contextual de manejo de desbordamiento de TX. Esto controla cómo se procesan las muestras fuera de rango (>1.0) de los clientes de modos digitales TCI antes de llegar a la radio. El valor predeterminado es **Clip** para mantener compatibilidad con versiones anteriores.

| Modo | Valor | Descripción |
|------|-------|-------------|
| **Clip (saturación ±1.0)** | 0 | Recorta firmemente los excesos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los excesos pero protege la conversión int16 posterior. |
| **NaN guard (solo anula NaN/Inf)** | 1 | Pasa las muestras bit-exactas; solo anula valores patológicos NaN/Inf. Preserva la fidelidad de tono de los modos digitales; los flotantes fuera de rango llegan a la radio. |
| **Measure only (bypass verdadero)** | 2 | Nunca modifica las muestras. Cuenta los excesos para telemetría; la conversión int16 posterior aún recorta en la ruta DAX nativa de la radio. |

## Indicadores

| Indicador | Estados posibles | Significado |
|-----------|-----------------|-------------|
| **Estado del servidor** | `(stopped)` | El servidor no está en ejecución. |
| | `:<puerto> (N clients)` | El servidor está en ejecución en el puerto especificado con N clientes conectados. |
| | `(port in use)` | El puerto elegido ya está en uso por otro proceso. |
| **Etiquetas de asignación de slice RX/TX** | `—` | No hay ningún slice asignado actualmente. |
| | `Slice <letra>` | El slice especificado está asignado a este canal. |

## Consejos

- Los valores de puerto fuera de rango se restablecen automáticamente a `50001`.
- Si desea que el servidor TCI se inicie cada vez que AetherSDR se abre, habilite `Settings > Autostart TCI with AetherSDR`. Esto activa la opción `AutoStartTCI` y también marca **Enable** al inicio.
- El medidor de TX usa un suavizado de ataque rápido y caída lenta, por lo que una transmisión breve mantendrá el medidor visiblemente elevado durante un momento después de que el audio se detenga. Ningún movimiento durante una transmisión con key confirma que el audio no está llegando desde el cliente.
- Las etiquetas de asignación de slice ahora admiten renderizado de texto enriquecido, por lo que las letras de slice pueden aparecer con formato adicional (por ejemplo, color) para indicar propiedades del slice.
- Para modos digitales que requieren fidelidad de tono bit-exacta, use los modos **NaN guard** o **Measure only** para evitar distorsión armónica por recorte.
- El contenedor del applet usa el sistema de temas (`applet/tci`) para un estilo coherente en todos los temas.
- El servidor TCI se cierra explícitamente cuando AetherSDR se cierra para evitar una condición de uso después de liberación (use-after-free), corregida en v0.9.7.
- Las filas RX se ocultan automáticamente cuando superan la capacidad de slices de la radio (reflejando el comportamiento del applet DAX). Solo se muestran las filas correspondientes a los slices disponibles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a Off** — Otra aplicación está usando ese puerto. Escriba un número de puerto diferente en el campo **Port**, presione Intro y haga clic en **Enable** nuevamente.
- **El estado muestra el puerto correcto y el número de clientes, pero la radio no transmite audio** — Confirme que la etiqueta de slice de TX en la fila **TX** muestra `Slice <letra>` y no `—`. Si muestra `—`, designe un slice de TX desde la interfaz principal. También confirme que **TX gain+meter** está por encima de `0.0`.
- **La aplicación de terceros no puede conectarse** — Verifique que la aplicación apunte a `localhost` (o a la IP del host de AetherSDR) y que el número de puerto coincida con el campo **Port**. Confirme que ninguna regla de firewall esté bloqueando el puerto.
- **El medidor de TX no muestra movimiento a pesar de que el cliente está conectado y con key** — La aplicación del cliente puede estar enviando audio a un dispositivo de audio del sistema en lugar de a través del WebSocket TCI. Verifique la salida de audio o la configuración de enrutamiento de audio TCI del cliente. AetherSDR no usa el dispositivo de audio DAX2 de Windows para el TX por TCI; el audio debe llegar a través de la conexión WebSocket.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia de TX por TCI](adjust-tci-tx-gain.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al abrir](autostart-tci-on-launch.md)
