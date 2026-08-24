# Cambiar el puerto de TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su software de registro o de modos digitales requiera un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Abra el applet TCI haciendo clic en el botón **TCI** de la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango vuelven automáticamente a `50001`.
3. Presione **Entrar** o mueva el foco fuera del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está actualmente en ejecución (Enable está activado), AetherSDR detiene el servidor y lo reinicia automáticamente en el nuevo puerto. No se requiere ninguna acción adicional.
5. Si el servidor no está en ejecución, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Qué hace cada control

| Control                        | Predeterminado                                                                                                                          | Rango válido                                                                                                                                                                                                                                                                                                                     |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo **Port**                 | `50001`                                                                                                                                 | 1024–65535                                                                                                                                                                                                                                                                                                                       |
| **Enable / Disabled**          | Apagado (muestra "Disabled")                                                                                                            | "Disabled" / "Enabled"                                                                                                                                                                                                                                                                                                           |
| Indicador de estado del servidor| `(stopped)`                                                                                                                            | `(stopped)`, `:<port> (N clients)`, `(port in use)`                                                                                                                                                                                                                                                                              |
| Ganancia+medidor **RX1**–**RX8**| 0.5 cada uno                                                                                                                            | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                   |
| Ganancia+medidor **TX**        | 0.5                                                                                                                                     | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                   |
| Etiquetas de asignación de slice RX/TX | —                                                                                                                                 | `—` o `Slice <letra>` (texto enriquecido)                                                                                                                                                                                                                                                                                       |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Nuevo en v26.5.3. Clip (0): limita los excesos a ±1.0 con distorsión armónica; NaNGuard (1): preserva tonos digitales exactos a nivel de bits anulando solo NaN/Inf; Measure (2): cuenta excesos para telemetría sin mutación. Se guarda como `TciTxOverflowMode` (0/1/2). El predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |

## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados se desconectarán y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(port in use)` después de hacer clic en Enable, elija un número de puerto diferente e intente nuevamente.
- Los controles deslizantes de ganancia RX y TX controlan el nivel de audio TCI para sus respectivos canales. Arrastre para ajustar; el valor se guarda en `TciRxGain1`–`TciRxGain8` y `TciTxGain`.
- Las filas RX visibles dependen de la cantidad máxima de slices de su radio. AETHER admite hasta 8 canales RX de TCI, pero en radios con menos slices (por ejemplo, una radio de 4 slices), las filas RX adicionales se ocultan automáticamente. El protocolo TCI en sí admite los canales 1–8 independientemente; el applet simplemente coincide con lo que su radio puede realmente entregar.
- Cada control deslizante de ganancia RX de TCI tiene un nombre accesible de "TCI RX 1 gain", "TCI RX 2 gain", etc., y el control deslizante de ganancia TX tiene un nombre accesible de "TCI TX gain" para compatibilidad con lectores de pantalla.
- El texto del botón Enable cambia para reflejar el estado actual: "Disabled" cuando el servidor está detenido, "Enabled" cuando está en ejecución. Si `AutoStartTCI` está configurado en `True` en los ajustes, el botón comienza como "Enabled" y el servidor se inicia automáticamente al arrancar.
- Las etiquetas de asignación de slice muestran qué slice impulsa cada fila RX/TX. La letra del slice puede aparecer en formato de texto enriquecido para una mejor visualización.
- El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado. En Windows, el TX de TCI evita por completo la ruta del dispositivo de audio SmartSDR DAX2 y utiliza una ranura de flujo dedicada `dax_tx`, por lo que funciona incluso sin PipeWire.
- Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir el selector de modo de desbordamiento TX. Elija cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modos digitales:
  - **Clip (saturación ±1.0)** — Limita firmemente los excesos a ±1.0. Valor predeterminado que introduce armónicos en excesos pero protege la conversión posterior a int16.
  - **NaN guard (anular solo NaN/Inf)** — Pasa las muestras de forma bit-exacta; solo anula los valores patológicos NaN/Inf. Preserva la fidelidad del tono en modos digitales; los flotantes fuera de rango llegan a la radio.
  - **Measure only (bypass verdadero)** — Nunca muta muestras. Cuenta excesos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa de la radio.

## Solución de problemas

- **El estado muestra `(port in use)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en Enable nuevamente.
- **El campo Port vuelve a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.
- **Algunas filas RX no están visibles** — Esto es normal en radios con menos de 8 slices. El applet oculta las filas por encima de la capacidad de slices de la radio para evitar mostrar canales que no pueden utilizarse.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Iniciar TCI automáticamente al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
