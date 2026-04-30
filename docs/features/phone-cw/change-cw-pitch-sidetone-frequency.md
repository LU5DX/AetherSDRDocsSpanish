# Cambiar la frecuencia de pitch/sidetone en CW

El control de pitch en CW establece la frecuencia de tono utilizada para monitoreo de sidetone y decodificación CW. En v0.9.2.1, se han eliminado los controles de sidetone local separados (botón Local STn, deslizador de volumen local, botón Follow pitch y deslizador de pitch local). El único toggle **Sidetone** y el deslizador **Sidetone volume** ahora controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente de forma sincronizada. El pitch y el pan siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El applet Phone/CW requiere una conexión activa a la radio.
- Establezca el slice activo en un modo CW. El sub-panel CW solo es visible cuando el slice activo está en modo CW; de lo contrario, se muestra el sub-panel Phone.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** en la bandeja derecha si aún no está visible.

## Pasos

### Cambiar el pitch CW de la radio

1. Ubique **Pitch < / >** en el sub-panel CW. Es un spinbox con dos botones de flecha.
2. Haga clic en **<** para disminuir el pitch en 10 Hz, o en **>** para aumentarlo en 10 Hz.
3. El nuevo pitch se envía a la radio inmediatamente. Rango válido: 100–6000 Hz, paso 10 Hz. Valor predeterminado: 600 Hz.

El generador de sidetone del lado del cliente siempre sigue este valor de pitch automáticamente. No hay un control de pitch local separado.

### Habilitar o deshabilitar el sidetone

1. Haga clic en **Sidetone** en el sub-panel CW para activarlo o desactivarlo.
2. Tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente se habilitan o deshabilitan juntos mediante este único botón.

En Windows, la secuencia de sidetone ahora se inicia inmediatamente al conectarse (v0.9.3, #2105).

### Ajustar el volumen del sidetone

1. Mueva el deslizador **Sidetone volume** al nivel deseado. Rango válido: 0–100.
2. El deslizador establece simultáneamente el volumen del monitor de la radio (`mon_gain_cw`) y el volumen del generador de sidetone del lado del cliente.

## Qué hace cada control

| Control             | Predeterminado | Rango válido           |
|---------------------|---------|-----------------------|
| **Pitch < / >**     | 600 Hz  | 100–6000 Hz (paso 10) |
| **Sidetone**        | —       | On / Off              |
| **Sidetone volume** | —       | 0–100                 |
| **L / R pan (CW)**  | 50      | 0–100                 |

## Consejos

- El control **Pitch < / >** afecta tanto al sidetone audible en la radio como a la frecuencia utilizada por el decodificador CW. Ajústelo para que coincida con su preferencia de pitch personal. El sidetone del lado del cliente siempre lo sigue automáticamente.
- Dado que el pitch y el pan siguen los parámetros de la radio automáticamente, solo necesita ajustar **Pitch < / >** y **L / R pan (CW)** en un solo lugar — tanto el monitor de la radio como el generador local se actualizan juntos.
- El generador de sidetone del lado del cliente opera con una latencia aproximada de 10 ms y funciona con transmisiones generadas por paddle, straight key y CWX. Si no escucha sidetone en absoluto, verifique que **Sidetone** esté habilitado.
- Cuando **Mic source** está configurado en **PC**, el medidor **Level** refleja metering del lado del cliente y permanece activo independientemente del parámetro met_in_rx de la radio.

## Solución de problemas

- **No se escucha sidetone** — Confirme que **Sidetone** está habilitado y **Sidetone volume** está por encima de cero. Estos dos controles regulan tanto el monitor de la radio como el generador del lado del cliente.
- **El sidetone no se inicia al conectarse (Windows)** — Esto se resolvió en v0.9.3 (#2105). Asegúrese de ejecutar v0.9.3 o superior.
- **El medidor Level no aparece al conectarse** — Si **Mic source** está configurado en **PC**, el medidor debería aparecer inmediatamente al conectarse a partir de v0.9.3 (#2086). Para otras fuentes de micrófono, el medidor se suprime cuando met_in_rx está desactivado y la radio no está transmitiendo.
- **El cambio de pitch no tiene efecto** — Confirme que el slice activo está en un modo CW. El sub-panel CW y su control de pitch solo están activos en modos CW.
- **El sub-panel CW no es visible** — El slice activo no está en un modo CW. Cambie el slice a CW; el applet se cambia automáticamente.

## Relacionado

- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
