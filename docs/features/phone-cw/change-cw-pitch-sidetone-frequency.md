# Cambiar el tono CW / frecuencia del sidetone

Los controles de tono CW establecen la frecuencia del tono utilizado para la monitorización del sidetone y la decodificación CW. Existen dos configuraciones de tono independientes: el tono del radio (enviado al FLEX-8600) y el tono del sidetone local (generado en el cliente por AetherSDR).

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión activa con el radio.
- Configure el slice activo en un modo CW. El subpanel CW solo es visible cuando el slice activo está en modo CW; de lo contrario, se muestra el subpanel Phone.
- Abra el applet Phone/CW haciendo clic en el botón **P/CW** de la bandeja en la barra lateral derecha, si aún no está visible.

## Pasos

### Cambiar el tono CW del radio

1. Localice **Pitch < / >** en el subpanel CW. Es un campo numérico con dos botones de flecha.
2. Haga clic en **<** para disminuir el tono 10 Hz, o en **>** para aumentarlo 10 Hz.
3. El nuevo tono se envía al radio de forma inmediata. Rango válido: 100–6000 Hz, paso de 10 Hz. Valor predeterminado: 600 Hz.

### Cambiar el tono del sidetone local

El sidetone local tiene su propio control de tono, que por defecto sigue automáticamente el tono del radio.

1. Compruebe si **Follow (local pitch)** está habilitado (el botón aparece resaltado/marcado). Si está activado, el tono del sidetone local sigue automáticamente el tono del radio — no se requiere ninguna acción adicional.
2. Para establecer un tono manual, haga clic en **Follow (local pitch)** para desactivarlo.
3. Ajuste el control deslizante **Local sidetone pitch** a la frecuencia deseada. Rango válido: 100–2000 Hz. Valor predeterminado: 600 Hz. La configuración se guarda como `CwLocalSidetonePitchHz`.
4. Para restaurar el seguimiento automático, haga clic de nuevo en **Follow (local pitch)** para activarlo. La configuración se guarda como `CwLocalSidetonePitchFollow`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave guardada | Comportamiento |
|---|---|---|---|---|
| **Pitch < / >** | 600 Hz | 100–6000 Hz (paso 10) | — | Ajusta el tono de sidetone/decodificación CW del radio en pasos de 10 Hz por clic; se envía al FLEX-8600. |
| **Follow (local pitch)** | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` | Cuando está activado, el tono del sidetone local refleja el tono del radio. Cuando está desactivado, el control deslizante **Local sidetone pitch** se habilita para ajuste manual. |
| **Local sidetone pitch** | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` | Establece la frecuencia del tono del sidetone en el cliente, en Hz. Solo está activo cuando **Follow (local pitch)** está desactivado. |

## Consejos

- El control **Pitch < / >** afecta tanto al sidetone audible en el radio como a la frecuencia utilizada por el decodificador CW. Ajústelo según su preferencia personal de tono.
- Cuando **Follow (local pitch)** está activado, solo necesita cambiar el tono del radio con **Pitch < / >** — el sidetone local se actualiza automáticamente.
- El sidetone local (**Local STn**) opera con una latencia aproximada de 10 ms y funciona con paleta, manipulador recto y transmisiones generadas por CWX. Si no escucha el sidetone local, verifique que **Local STn** esté habilitado.

## Solución de problemas

- **El control deslizante de tono del sidetone local está desactivado (gris)** — **Follow (local pitch)** está activado. Haga clic en **Follow (local pitch)** para desactivarlo antes de ajustar el control deslizante.
- **Pitch < / > no tiene efecto en el tono del sidetone local** — **Follow (local pitch)** está desactivado. Active de nuevo **Follow (local pitch)**, o actualice manualmente **Local sidetone pitch** para que coincida.
- **El subpanel CW no es visible** — El slice activo no está en modo CW. Cambie el slice a CW; el applet cambia automáticamente.

## Relacionados

- [Habilitar el sidetone CW local de baja latencia (Local STn) para trabajo con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Hacer que el tono del sidetone local siga el tono CW del radio, o ajustarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Ajustar el volumen del sidetone local de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
