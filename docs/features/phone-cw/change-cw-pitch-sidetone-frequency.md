# Cambiar el tono CW / frecuencia de la señal de escucha lateral

El control de tono CW establece la frecuencia del tono usado para la monitorización de la señal de escucha lateral (sidetone) y la decodificación CW. En la versión v0.9.2.1, los controles locales independientes de sidetone (botón Local STn, deslizador de volumen local, botón Follow pitch y deslizador de tono local) han sido eliminados. El botón **Sidetone** y el deslizador **Sidetone volume** controlan ahora de forma sincronizada tanto el monitor del equipo alimentado por DAX como el generador de sidetone de baja latencia del lado del cliente. El tono y el balance panorámico siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` del equipo.

## Antes de comenzar

- Conéctese a un equipo FLEX-8600. El applet Phone/CW requiere una conexión activa con el equipo.
- Configure el slice activo en un modo CW. El subpanel CW solo es visible cuando el slice activo está en modo CW; de lo contrario se muestra el subpanel Phone.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha, si no está visible.

## Pasos

### Cambiar el tono CW del equipo

1. Ubique **Pitch < / >** en el subpanel CW. Es un control giratorio con dos botones de flecha.
2. Haga clic en **<** para reducir el tono 10 Hz, o en **>** para aumentarlo 10 Hz.
3. El nuevo tono se envía al equipo de forma inmediata. Rango válido: 100–6000 Hz, paso de 10 Hz. Valor predeterminado: 600 Hz.

El generador de sidetone del lado del cliente siempre sigue este valor de tono de forma automática. No existe un control de tono local independiente.

### Activar o desactivar el sidetone

1. Haga clic en **Sidetone** en el subpanel CW para activarlo o desactivarlo.
2. Este único botón habilita o deshabilita simultáneamente el monitor del equipo alimentado por DAX y el generador de sidetone de baja latencia del lado del cliente.

En Windows, el flujo de sidetone ahora comienza de inmediato al conectarse (v0.9.3, #2105).

### Ajustar el volumen del sidetone

1. Mueva el deslizador **Sidetone volume** al nivel deseado. Rango válido: 0–100.
2. El deslizador ajusta simultáneamente el volumen del monitor del equipo (`mon_gain_cw`) y el volumen del generador de sidetone del lado del cliente.

## Qué hace cada control

| Control             | Valor predeterminado | Rango válido          |
|---------------------|----------------------|-----------------------|
| **Pitch < / >**     | 600 Hz               | 100–6000 Hz (paso 10) |
| **Sidetone**        | —                    | On / Off              |
| **Sidetone volume** | —                    | 0–100                 |
| **L / R pan (CW)**  | 50                   | 0–100                 |

## Consejos

- El control **Pitch < / >** afecta tanto al sidetone audible en el equipo como a la frecuencia utilizada por el decodificador CW. Ajústelo según su preferencia personal de tono. El sidetone del lado del cliente siempre lo sigue de forma automática.
- Dado que el tono y el balance panorámico siguen automáticamente los parámetros del equipo, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un único lugar — tanto el monitor del equipo como el generador local se actualizan juntos.
- El generador de sidetone del lado del cliente opera con una latencia de aproximadamente 10 ms y funciona con paleta, manipulador recto y transmisiones generadas por CWX. Si no escucha ningún sidetone, verifique que **Sidetone** esté habilitado.
- Cuando **Mic source** está configurado como **PC**, el medidor **Level** refleja la medición del lado del cliente y permanece activo independientemente del parámetro met_in_rx del equipo.

## Solución de problemas

- **No se escucha sidetone** — Confirme que **Sidetone** esté habilitado y que **Sidetone volume** sea mayor que cero. Estos dos controles gestionan tanto el monitor del equipo como el generador del lado del cliente.
- **El sidetone no comienza al conectarse (Windows)** — Este problema fue resuelto en v0.9.3 (#2105). Asegúrese de estar ejecutando v0.9.3 o una versión posterior.
- **El medidor Level no aparece al conectarse** — Si **Mic source** está configurado como **PC**, el medidor debe aparecer de inmediato al conectarse a partir de v0.9.3 (#2086). Para otras fuentes de micrófono, el medidor se suprime cuando met_in_rx está desactivado y el equipo no está transmitiendo.
- **El cambio de tono no tiene efecto** — Confirme que el slice activo esté en un modo CW. El subpanel CW y su control de tono solo están activos en modos CW.
- **El subpanel CW no es visible** — El slice activo no está en modo CW. Cambie el slice a CW; el applet cambia automáticamente.

## Relacionado

- [Escuchar el monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
