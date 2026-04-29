# Cambiar el tono de CW / frecuencia del sidetone

El control de tono de CW establece la frecuencia del tono utilizada para la monitorización del sidetone y la decodificación de CW. En la versión v0.9.2.1, los controles de sidetone local independientes (botón Local STn, control deslizante de volumen local, botón Follow pitch y control deslizante de tono local) han sido eliminados. El botón **Sidetone** y el control deslizante **Sidetone volume** ahora controlan de forma sincronizada tanto el monitor del radio alimentado por DAX como el generador de sidetone de baja latencia del lado del cliente. El tono y el paneo siguen siempre automáticamente los parámetros `cw_pitch` y `mon_pan_cw` del radio.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Establezca el slice activo en un modo CW. El subpanel de CW solo es visible cuando el slice activo está en modo CW; de lo contrario, se muestra el subpanel de Phone.
- Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha, si no está visible todavía.

## Pasos

### Cambiar el tono de CW del radio

1. Localice **Pitch < / >** en el subpanel de CW. Es un spinbox con dos botones de flecha.
2. Haga clic en **<** para disminuir el tono en 10 Hz, o en **>** para aumentarlo en 10 Hz.
3. El nuevo tono se envía al radio inmediatamente. Rango válido: 100–6000 Hz, paso de 10 Hz. Valor predeterminado: 600 Hz.

El generador de sidetone del lado del cliente siempre sigue este valor de tono automáticamente. No existe un control de tono local independiente.

### Activar o desactivar el sidetone

1. Haga clic en **Sidetone** en el subpanel de CW para activarlo o desactivarlo.
2. Tanto el monitor del radio alimentado por DAX como el generador de sidetone de baja latencia del lado del cliente se activan o desactivan juntos mediante este único botón.

### Ajustar el volumen del sidetone

1. Mueva el control deslizante **Sidetone volume** al nivel deseado. Rango válido: 0–100.
2. El control deslizante establece simultáneamente el volumen del monitor del radio (`mon_gain_cw`) y el volumen del generador de sidetone del lado del cliente.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Pitch < / >** | 600 Hz | 100–6000 Hz (paso 10) | — | Ajusta el tono de sidetone/decodificación de CW del radio en pasos de 10 Hz por clic; se envía al FLEX-8600. El tono del sidetone del lado del cliente siempre sigue este valor automáticamente. |
| **Sidetone** | — | On / Off | — | Activa o desactiva de forma sincronizada tanto el monitor de sidetone del radio alimentado por DAX como el generador de sidetone de baja latencia del lado del cliente. |
| **Sidetone volume** | — | 0–100 | — | Establece simultáneamente el volumen del monitor del radio (`mon_gain_cw`) y el volumen del generador de sidetone del lado del cliente. |
| **L / R pan (CW)** | 50 | 0–100 | — | Establece el paneo estéreo del monitor de CW en el radio y aplica paneo de potencia constante al generador de sidetone del lado del cliente. Sigue `mon_pan_cw` automáticamente. Doble clic recentra en 50 (centro). |

## Consejos

- El control **Pitch < / >** afecta tanto al sidetone audible en el radio como a la frecuencia utilizada por el decodificador de CW. Ajústelo según su preferencia personal de tono. El sidetone del lado del cliente siempre lo sigue automáticamente.
- Dado que el tono y el paneo siguen los parámetros del radio automáticamente, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un único lugar: tanto el monitor del radio como el generador local se actualizan juntos.
- El generador de sidetone del lado del cliente opera con una latencia de aproximadamente 10 ms y funciona con paleta, manipulador recto y transmisiones generadas por CWX. Si no escucha ningún sidetone, verifique que **Sidetone** esté activado.

## Solución de problemas

- **No se escucha ningún sidetone** — Confirme que **Sidetone** está activado y que **Sidetone volume** es mayor que cero. Tanto el monitor del radio como el generador del lado del cliente son controlados por estos dos controles.
- **El cambio de tono no tiene efecto** — Confirme que el slice activo está en un modo CW. El subpanel de CW y su control de tono solo están activos en modos CW.
- **El subpanel de CW no es visible** — El slice activo no está en modo CW. Cambie el slice a CW; el applet cambia automáticamente.

## Relacionado

- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
