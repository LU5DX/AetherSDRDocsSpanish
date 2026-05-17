# Cambiar el puerto de TCI

El servidor TCI escucha en un puerto configurable. Cambie el puerto cuando el valor predeterminado entre en conflicto con otra aplicación o cuando su software de registro o modo digital requiera un número de puerto específico.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El miniaplicativo TCI requiere una conexión activa con la radio.
- Abra el miniaplicativo TCI haciendo clic en el botón de la bandeja **TCI** en la barra lateral derecha, si aún no está visible.

## Pasos

1. En el miniaplicativo TCI, localice el campo **Port** junto a la etiqueta "Port:" en la parte inferior del miniaplicativo.
2. Haga clic en el campo **Port** y escriba el nuevo número de puerto. Los valores válidos son 1024–65535. El valor predeterminado es `50001`. Los valores fuera de este rango se restablecen a `50001`.
3. Presione **Enter** o aleje el foco del campo para confirmar. El valor se guarda en `TciPort`.
4. Si el servidor está en funcionamiento (Enable está marcado), AetherSDR detiene el servidor y lo reinicia automáticamente en el nuevo puerto. No se requiere ninguna acción adicional.
5. Si el servidor no está en funcionamiento, haga clic en **Enable** para iniciarlo en el nuevo puerto.

## Qué hace cada control

| Control                         | Predeterminado | Rango válido                                       |
|---------------------------------|----------------|-----------------------------------------------------|
| Campo **Port**                  | `50001`        | 1024–65535                                          |
| **Enable**                      | Apagado        | Encendido / Apagado                                 |
| Indicador de estado del servidor| `(stopped)`    | `(stopped)`, `:<puerto> (N clientes)`, `(port in use)` |
| Ganancia+medidor de **RX1**     | 0.5            | 0.0–1.0 (control deslizante/medidor combinado)      |
| Ganancia+medidor de **RX2**     | 0.5            | 0.0–1.0 (control deslizante/medidor combinado)      |
| Ganancia+medidor de **RX3**     | 0.5            | 0.0–1.0 (control deslizante/medidor combinado)      |
| Ganancia+medidor de **RX4**     | 0.5            | 0.0–1.0 (control deslizante/medidor combinado)      |
| Ganancia+medidor de **TX**      | 0.5            | 0.0–1.0 (control deslizante/medidor combinado)      |
| Etiquetas de asignación de slice RX/TX | —          | `—` o `Slice <letra>` (texto enriquecido)           |

## Consejos

- Si cambia el puerto mientras el servidor está habilitado, el reinicio es inmediato. Los clientes conectados serán desconectados y deberán reconectarse al nuevo puerto.
- Si el estado muestra `(port in use)` después de hacer clic en **Enable**, elija un número de puerto diferente e inténtelo de nuevo.
- Los controles deslizantes de ganancia de RX y TX controlan el nivel de audio TCI para sus respectivos canales. Arrastre para ajustar; el valor se conserva en `TciRxGain1`–`TciRxGain4` y `TciTxGain`.
- Las etiquetas de asignación de slice muestran qué slice impulsa cada fila de RX/TX. La letra del slice puede aparecer en formato de texto enriquecido para una mejor visualización.

## Solución de problemas

- **El estado muestra `(port in use)` después de habilitar** — Otra aplicación ya está vinculada a ese puerto. Ingrese un número de puerto diferente en el campo **Port** y haga clic en **Enable** nuevamente.
- **El campo Port vuelve a `50001`** — El valor ingresado estaba fuera del rango 1024–65535. Ingrese un valor dentro del rango válido.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Resumen del servidor TCI](overview.md)
