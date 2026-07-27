# Solucionar TX silencioso por TCI en Windows o Linux sin PipeWire

El audio de TX por TCI se enruta a través de un slot dedicado `dax_tx` dentro del servidor TCI de AetherSDR, independiente de la ruta del dispositivo de audio DAX2 de SmartSDR en Windows y de PipeWire. Esto significa que TX por TCI debería funcionar en todas las plataformas sin configuración especial. Esta página le ayuda a confirmar que el servidor TCI está configurado correctamente y que la ganancia de TX no es la causa del silencio.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- La aplicación de terceros que envía audio TX por TCI (por ejemplo, un programa de modos digitales) debe configurarse para conectarse al servidor TCI de AetherSDR, no a SmartSDR DAX2 ni a ningún otro dispositivo de audio.
- Asegúrese de estar ejecutando AetherSDR v0.9.5.1 o posterior. Las versiones anteriores tenían una política de audio TX dependiente de la plataforma que podía bloquear el audio TX en Windows y Linux sin PipeWire.

## Pasos

1. Haga clic en el botón **TCI** de la barra lateral derecha para abrir el applet del servidor TCI.
2. Verifique la etiqueta de estado del servidor junto al campo **Port**.
   - Si muestra `(stopped)`, haga clic en **Enabled** para iniciar el servidor. El texto del botón cambia a **Enabled** cuando el servidor está en ejecución.
   - Si muestra `(port in use)`, el puerto elegido ya está ocupado por otro proceso. Cambie el valor en el campo **Port** a un puerto libre (rango válido: 1024–65535; predeterminado: `50001`), luego presione Enter y haga clic en **Enabled**.
3. Confirme que la etiqueta de estado muestra `:<port> (N clients)` con al menos un cliente conectado. Si su aplicación TX no aparece como cliente conectado, verifique su configuración de host y puerto TCI y asegúrese de que coincidan con el valor del campo **Port**.
4. Observe la fila **TX** en el applet. Verifique la etiqueta de asignación de slice junto al medidor de TX.
   - Si muestra `—`, ningún slice está designado como slice de TX. Use los controles de slice de la radio para asignar un slice de TX.
   - Si muestra `Slice <letra>` (con la letra del slice renderizada en texto enriquecido, por ejemplo, coloreada o estilizada), la ruta de TX está activa.
5. Arrastre el control deslizante **TX gain+meter** para confirmar que no está en `0.0`. El valor predeterminado es `0.5` (rango válido: 0.0–1.0, persistido como `TciTxGain`). Un valor de `0.0` produce silencio independientemente de la plataforma.
6. Active el transmisor desde su aplicación de terceros y observe el medidor **TX gain+meter** para ver movimiento de nivel. Si el medidor muestra actividad, el audio está llegando al servidor y la radio debería estar transmitiendo.
7. Si está usando un modo digital que requiere fidelidad de tono bit-exacta, haga clic derecho en el control deslizante **TX gain+meter** para abrir el menú de manejo de desbordamiento de TX. Seleccione el modo deseado para controlar cómo se procesan las muestras fuera de rango (>1.0) de los clientes TCI.

## Función de cada control

| Control                            | Predeterminado | Rango válido |
|------------------------------------|----------------|--------------|
| **Port**                           | `50001`        | 1024–65535   |
| **Enable**                         | Apagado        | Encendido / Apagado |
| **TX gain+meter**                  | `0.5`          | 0.0–1.0      |
| **RX1 gain+meter**                 | `0.5`          | 0.0–1.0      |
| **RX2 gain+meter**                 | `0.5`          | 0.0–1.0      |
| **RX3 gain+meter**                 | `0.5`          | 0.0–1.0      |
| **RX4 gain+meter**                 | `0.5`          | 0.0–1.0      |
| **Modo de desbordamiento TX (clic derecho)** | Clip | Clip (0), NaNGuard (1), Measure (2) |

El botón **Enable** muestra **Enabled** cuando el servidor está en ejecución y **Disabled** cuando está detenido. Si la configuración **AutoStartTCI** está habilitada en Settings, el botón se inicia como **Enabled** al abrir.

## Modos de manejo de desbordamiento TX

Haga clic derecho en el control deslizante **TX gain+meter** para abrir el menú contextual de manejo de desbordamiento TX. Esto controla cómo se procesan las muestras fuera de rango (>1.0) de los clientes de modos digitales por TCI antes de llegar a la radio. El valor predeterminado es **Clip** para mantener la compatibilidad hacia atrás.

| Modo | Valor | Descripción |
|------|-------|-------------|
| **Clip (saturación ±1.0)** | 0 | Limita bruscamente los picos a ±1.0. Valor predeterminado defensivo; introduce armónicos en los picos pero protege la conversión a int16 posterior. |
| **NaN guard (solo cero NaN/Inf)** | 1 | Pasa las muestras sin cambios; solo pone a cero los valores NaN/Inf patológicos. Preserva la fidelidad de tono de los modos digitales; los flotantes fuera de rango llegan a la radio. |
| **Measure only (bypass real)** | 2 | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 posterior aún limita en la ruta DAX nativa de la radio. |

## Indicadores

| Indicador | Estados posibles | Significado |
|-----------|------------------|-------------|
| **Estado del servidor** | `(stopped)` | El servidor no está en ejecución. |
| | `:<port> (N clients)` | El servidor está en ejecución en el puerto especificado con N clientes conectados. |
| | `(port in use)` | El puerto elegido ya está ocupado por otro proceso. |
| **Etiquetas de asignación de slice RX/TX** | `—` | Ningún slice está asignado actualmente. |
| | `Slice <letra>` | El slice especificado está asignado a este canal. |

## Consejos

- Los valores de puerto fuera de rango vuelven automáticamente a `50001`.
- Si desea que el servidor TCI se inicie cada vez que AetherSDR se abra, active `Settings > Autostart TCI with AetherSDR`. Esto establece la marca `AutoStartTCI` y también marca **Enable** al inicio.
- El medidor de TX usa suavizado de ataque rápido y decaimiento lento, por lo que una transmisión breve mantendrá el medidor visiblemente elevado por un momento después de que el audio se detenga. Ningún movimiento durante una transmisión activa confirma que el audio no está llegando del cliente.
- Las etiquetas de asignación de slice ahora admiten renderizado de texto enriquecido, por lo que las letras de slice pueden aparecer con formato adicional (por ejemplo, color) para indicar propiedades del slice.
- Para modos digitales que requieren fidelidad de tono bit-exacta, use los modos **NaN guard** o **Measure only** para evitar la distorsión armónica por recorte.
- El contenedor del applet usa el sistema de temas (`applet/tci`) para un estilo consistente en todos los temas.
- El servidor TCI se cierra explícitamente cuando AetherSDR se cierra para evitar una condición de use-after-free, corregida en v0.9.7.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable vuelve a apagado** — Otra aplicación está usando ese puerto. Ingrese un número de puerto diferente en el campo **Port**, presione Enter y haga clic en **Enabled** nuevamente.
- **El estado muestra el puerto correcto y el conteo de clientes, pero la radio no transmite audio** — Confirme que la etiqueta de slice de TX en la fila **TX** muestra `Slice <letra>` y no `—`. Si muestra `—`, designe un slice de TX desde la interfaz principal. También confirme que **TX gain+meter** está por encima de `0.0`.
- **La aplicación de terceros no puede conectarse** — Verifique que la aplicación apunte a `localhost` (o a la IP del host de AetherSDR) y que el número de puerto coincida con el campo **Port**. Confirme que ninguna regla de cortafuegos esté bloqueando el puerto.
- **El medidor de TX no muestra movimiento a pesar de que el cliente está conectado y activo** — La aplicación cliente puede estar enviando audio a un dispositivo de audio del sistema en lugar de a través del WebSocket TCI. Verifique la salida de audio o la configuración de enrutamiento de audio TCI del cliente. AetherSDR no usa el dispositivo de audio DAX2 de Windows para TX por TCI; el audio debe llegar a través de la conexión WebSocket.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia de TX por TCI](adjust-tci-tx-gain.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al abrir](autostart-tci-on-launch.md)
