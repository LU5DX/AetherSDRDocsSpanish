# Cambiar el puerto TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su software de registro o modo digital requiera un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- Abra el applet TCI haciendo clic en el botón de bandeja **TCI** en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango se restablecen a `50001`.
3. Presione **Enter** o mueva el foco fuera del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está actualmente en ejecución (Enable está marcado), AetherSDR detiene el servidor y lo reinicia automáticamente en el nuevo puerto. No se requiere ninguna acción adicional.
5. Si el servidor no está en ejecución, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Qué hace cada control

| Control                        | Predeterminado                                                                                                                       | Rango válido                                                                                                                                                                                                                                    |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo **Port**                 | `50001`                                                                                                                              | 1024–65535                                                                                                                                                                                                                                     |
| **Enable**                     | Apagado                                                                                                                              | Encendido / Apagado                                                                                                                                                                                                                           |
| Indicador de estado del servidor | `(detenido)`                                                                                                                         | `(detenido)`, `:<puerto> (N clientes)`, `(puerto en uso)`                                                                                                                                                                                     |
| Ganancia+medidor **RX1**       | 0.5                                                                                                                                  | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                               |
| Ganancia+medidor **RX2**       | 0.5                                                                                                                                  | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                               |
| Ganancia+medidor **RX3**       | 0.5                                                                                                                                  | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                               |
| Ganancia+medidor **RX4**       | 0.5                                                                                                                                  | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                               |
| Ganancia+medidor **TX**        | 0.5                                                                                                                                  | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                               |
| Etiquetas de asignación de slice RX/TX | —                                                                                                                            | `—` o `Slice <letra>` (texto enriquecido)                                                                                                                                                                                                     |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Nuevo en v26.5.3. Clip (0): limita los sobreimpulsos a ±1.0 con distorsión armónica; NaNGuard (1): preserva los tonos digitales bit exactos solo poniendo a cero NaN/Inf; Measure (2): cuenta los sobreimpulsos para telemetría sin mutación. Se conserva como `TciTxOverflowMode` (0/1/2). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |

## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados se desconectarán y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(puerto en uso)` después de hacer clic en **Enable**, elija un número de puerto diferente e intente nuevamente.
- Los controles deslizantes de ganancia RX y TX controlan el nivel de audio TCI para sus respectivos canales. Arrastre para ajustar; el valor se conserva en `TciRxGain1`–`TciRxGain4` y `TciTxGain`.
- Las etiquetas de asignación de slice muestran qué slice impulsa cada fila RX/TX. La letra del slice puede aparecer en formato de texto enriquecido para una mejor visualización.
- Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir el selector de modo de desbordamiento TX. Elija cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:
  - **Clip (saturación ±1.0)** — Limita los sobreimpulsos a ±1.0. Valor predeterminado que introduce armónicos en el sobreimpulso pero protege la conversión int16 descendente.
  - **NaN guard (solo poner a cero NaN/Inf)** — Pasa las muestras bit exactas; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad del tono del modo digital; los flotantes fuera de rango llegan a la radio.
  - **Measure only (bypass verdadero)** — Nunca muta las muestras. Cuenta los sobreimpulsos para telemetría; la conversión int16 descendente aún limita en la ruta DAX nativa de la radio.

## Solución de problemas

- **El estado muestra `(puerto en uso)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El campo Port se restablece a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
