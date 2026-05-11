# Elegir colores personalizados para la señal de voz y los marcadores de QRM

Los marcadores de Historial de Señal distinguen entre las señales de anchura de voz detectadas (dorado) y las portadoras de QRM persistentes (rojo). Puede cambiar estos colores para adaptarlos al tema de su panadapter o a su preferencia personal.

## Antes de empezar

- AetherSDR debe estar conectado a una radio.
- La pestaña Display en SpotHub está abierta (`Settings > SpotHub... > Display`).

## Pasos

1. Haga clic en **Settings** > **SpotHub...** para abrir el diálogo de SpotHub.
2. Haga clic en la pestaña **Display**.
3. En la sección **Signal History** a la derecha, localice las muestras de color **Signals** y **QRM** .
4. Haga clic en la muestra de color **Signals** (dorado `#FFC800` por defecto, clave de ajuste `SHistoryColorSignals`).
5. Seleccione un nuevo color en el selector de color y haga clic en **OK**.
6. Haga clic en la muestra de color **QRM** (rojo `#FF0000` por defecto, clave de ajuste `SHistoryColorQrm`).
7. Seleccione un nuevo color en el selector de color y haga clic en **OK**.

Los cambios se aplican inmediatamente a todos los marcadores visibles de Historial de Señal y QRM en el panadapter.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Muestra de color **Signals** (Historial de Señal) | `#FFC800` | Cualquier QColor | `SHistoryColorSignals` |
| Muestra de color **QRM** (Historial de Señal) | `#FF0000` | Cualquier QColor | `SHistoryColorQrm` |

## Relacionado

- [Toggle Signal History voice markers on the panadapter](toggle-signal-history-voice-markers-on-the-panadapter.md)
- [Toggle QRM markers to see persistent carriers and interference](toggle-qrm-markers-to-see-persistent-carriers-and-interference.md)
- [Adjust S-History marker lifetime, QRM gate and edge threshold](adjust-s-history-marker-lifetime-qrm-gate-and-edge-threshold.md)
