# Cambiar el puerto TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el predeterminado entre en conflicto con otra aplicación o cuando su software de registro o modo digital requiera un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Abra el applet TCI haciendo clic en el botón de bandeja **TCI** en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango se revierten automáticamente a `50001`.
3. Presione **Enter** o mueva el foco fuera del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está actualmente en ejecución (Enable está marcado), AetherSDR detiene el servidor y lo reinicia automáticamente en el nuevo puerto. No se requiere ninguna acción adicional.
5. Si el servidor no está en ejecución, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Función de cada control

| Control                        | Valor predeterminado                                                                                                                   | Rango válido                                                                                                                                                                                                                                                                                                                       |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo **Port**                 | `50001`                                                                                                                                | 1024–65535                                                                                                                                                                                                                                                                                                                        |
| **Enable**                     | Desactivado                                                                                                                            | Activado / Desactivado                                                                                                                                                                                                                                                                                                            |
| Indicador de estado del servidor| `(stopped)`                                                                                                                            | `(stopped)`, `:<puerto> (N clientes)`, `(puerto en uso)`                                                                                                                                                                                                                                                                          |
| Ganancia+medidor **RX1**       | 0.5                                                                                                                                    | 0.0–1.0 (deslizador/medidor combinado)                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor **RX2**       | 0.5                                                                                                                                    | 0.0–1.0 (deslizador/medidor combinado)                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor **RX3**       | 0.5                                                                                                                                    | 0.0–1.0 (deslizador/medidor combinado)                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor **RX4**       | 0.5                                                                                                                                    | 0.0–1.0 (deslizador/medidor combinado)                                                                                                                                                                                                                                                                                            |
| Ganancia+medidor **TX**        | 0.5                                                                                                                                    | 0.0–1.0 (deslizador/medidor combinado)                                                                                                                                                                                                                                                                                            |
| Etiquetas de asignación de slices RX/TX | —                                                                                                                              | `—` o `Slice <letra>` (texto enriquecido)                                                                                                                                                                                                                                                                                       |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/deslizador de ganancia TX para abrir un menú contextual seleccionando el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Nuevo en v26.5.3. Clip (0): sujeta los picos a ±1.0 con distorsión armónica; NaNGuard (1): preserva tonos digitales bit exactos solo anulando NaN/Inf; Measure (2): cuenta picos para telemetría sin modificación. Se persiste como `TciTxOverflowMode` (0/1/2). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |

## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados serán desconectados y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(puerto en uso)` después de hacer clic en **Enable**, elija un número de puerto diferente e intente de nuevo.
- Los deslizadores de ganancia RX y TX controlan el nivel de audio TCI para sus respectivos canales. Arrastre para ajustar; el valor se guarda en `TciRxGain1`–`TciRxGain4` y `TciTxGain`.
- Las etiquetas de asignación de slices muestran qué slice impulsa cada fila de RX/TX. La letra del slice puede aparecer en formato de texto enriquecido para una mejor visualización.
- Haga clic derecho en el medidor/deslizador de ganancia TX para abrir el selector de modo de desbordamiento TX. Elija cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:
  - **Clip (saturación ±1.0)** — Sujeta firmemente los picos a ±1.0. Valor predeterminado que introduce armónicos en los picos pero protege la conversión int16 posterior.
  - **NaN guard (solo anular NaN/Inf)** — Pasa las muestras bit exactas; solo anula valores patológicos NaN/Inf. Preserva la fidelidad del tono del modo digital; los flotantes fuera de rango llegan a la radio.
  - **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión int16 posterior aún sujeta en la ruta DAX nativa de la radio.

## Solución de problemas

- **El estado muestra `(puerto en uso)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El campo Port vuelve a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
