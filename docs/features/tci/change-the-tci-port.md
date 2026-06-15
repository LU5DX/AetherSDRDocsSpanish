# Cambiar el puerto TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su software de registro o modo digital requiera un número de puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa con la radio.
- Abra el applet TCI haciendo clic en el botón **TCI** de la bandeja en la barra lateral derecha si aún no está visible.

## Pasos

1. En el applet TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del applet.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango se restablecen a `50001`.
3. Presione **Enter** o mueva el foco fuera del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está funcionando actualmente (Enable está marcado), AetherSDR detiene el servidor y lo reinicia en el nuevo puerto automáticamente. No se requiere ninguna acción adicional.
5. Si el servidor no está funcionando, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Función de cada control

| Control                        | Valor predeterminado                                                                                                                   | Rango válido                                                                                                                                                                                                                                                                                                                       |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo **Port**                 | `50001`                                                                                                                                | 1024–65535                                                                                                                                                                                                                                                                                                                        |
| **Enable**                     | Desactivado                                                                                                                            | Activado / Desactivado                                                                                                                                                                                                                                                                                                            |
| Indicador de estado del servidor | `(stopped)`                                                                                                                            | `(stopped)`, `:<port> (N clients)`, `(port in use)`                                                                                                                                                                                                                                                                               |
| Ganancia+medidor **RX1**       | 0.5                                                                                                                                    | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                    |
| Ganancia+medidor **RX2**       | 0.5                                                                                                                                    | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                    |
| Ganancia+medidor **RX3**       | 0.5                                                                                                                                    | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                    |
| Ganancia+medidor **RX4**       | 0.5                                                                                                                                    | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                    |
| Ganancia+medidor **TX**        | 0.5                                                                                                                                    | 0.0–1.0 (control deslizante/medidor combinado)                                                                                                                                                                                                                                                                                    |
| Etiquetas de asignación de slice RX/TX | —                                                                                                                              | `—` o `Slice <letra>` (texto enriquecido)                                                                                                                                                                                                                                                                                         |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual seleccionando el modo de manejo de desbordamiento TX. Emite `tciTxOverflowModeChanged`. | Nuevo en v26.5.3. Clip (0): limita los picos a ±1.0 con distorsión armónica; NaNGuard (1): conserva los tonos digitales bit exactos solo anulando NaN/Inf; Measure (2): cuenta los picos para telemetría sin modificación. Se guarda como `TciTxOverflowMode` (0/1/2). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados se desconectarán y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(port in use)` después de hacer clic en **Enable**, elija un número de puerto diferente e intente nuevamente.
- Los controles deslizantes de ganancia RX y TX controlan el nivel de audio TCI para sus respectivos canales. Arrástrelos para ajustar; el valor se guarda en `TciRxGain1`–`TciRxGain4` y `TciTxGain`.
- Cada control deslizante de ganancia RX de TCI tiene un nombre accesible "TCI RX 1 gain", "TCI RX 2 gain", etc., y el control deslizante de ganancia TX tiene un nombre accesible "TCI TX gain" para compatibilidad con lectores de pantalla.
- Las etiquetas de asignación de slice muestran qué slice impulsa cada fila RX/TX. La letra del slice puede aparecer en formato de texto enriquecido para una mejor visualización.
- Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir el selector de modo de desbordamiento TX. Elija cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital:
  - **Clip (saturación ±1.0)** — Limita fuertemente los picos a ±1.0. Valor predeterminado que introduce armónicos en los picos pero protege la conversión a int16 aguas abajo.
  - **NaN guard (solo anular NaN/Inf)** — Pasa las muestras bit exactas; solo anula los valores patológicos NaN/Inf. Conserva la fidelidad de los tonos de modo digital; los valores flotantes fuera de rango llegan a la radio.
  - **Measure only (bypass real)** — Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión a int16 aguas abajo aún limita en la ruta DAX nativa de la radio.

## Solución de problemas

- **El estado muestra `(port in use)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El campo Port se restablece a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al iniciar](autostart-tci-on-launch.md)
- [Descripción general del servidor TCI](overview.md)
