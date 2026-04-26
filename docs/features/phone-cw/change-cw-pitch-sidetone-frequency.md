# Cambiar el tono CW / frecuencia del sidetone

Esta página explica cómo ajustar el tono CW — la frecuencia de tono utilizada para el sidetone y la decodificación CW — tanto en el radio como para el sidetone local del lado del cliente. Realice este ajuste para coincidir con su tono de escucha preferido o para alinear el sidetone local con un tono de radio distinto al predeterminado.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a los controles CW cuando el modo CW está activo.
- Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha, si no está visible todavía.

## Pasos

### Cambiar el tono CW del radio

1. En el subpanel CW, ubique el spinbox **Pitch < / >**.
2. Haga clic en **<** para reducir el tono en 10 Hz, o en **>** para aumentarlo en 10 Hz.
3. El rango válido es de 100–6000 Hz en pasos de 10 Hz. El valor predeterminado es 600 Hz.

Este ajuste de tono se envía al radio y también controla la decodificación CW.

### Cambiar el tono del sidetone local

El tono del sidetone local puede seguir automáticamente el tono del radio o configurarse con un valor independiente.

**Para seguir el tono del radio (predeterminado):**

1. Confirme que **Follow (local pitch)** esté activado (el botón aparece activo). Este es el estado predeterminado.
2. El tono del sidetone local seguirá automáticamente el valor de **Pitch < / >** del radio. No se requiere ninguna acción adicional.

**Para establecer un tono de sidetone local manual:**

1. Haga clic en **Follow (local pitch)** para desactivarlo.
2. El control deslizante **Local sidetone pitch** quedará habilitado.
3. Arrastre el control deslizante **Local sidetone pitch** hasta la frecuencia deseada. El rango válido es de 100–2000 Hz. El valor predeterminado es 600 Hz.

## Qué hace cada control

| Control | Tipo | Predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|---|
| **Pitch < / >** | Spinbox | 600 Hz | 100–6000 Hz (paso 10 Hz) | — |
| **Follow (local pitch)** | Botón de alternancia | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` |
| **Local sidetone pitch** | Control deslizante | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

## Consejos

- El control deslizante **Local sidetone pitch** está deshabilitado mientras **Follow (local pitch)** esté activado. Desactive **Follow (local pitch)** primero para habilitar el control deslizante.
- El tono del sidetone local es independiente del monitor de sidetone del radio. Si utiliza el sidetone local (Local STn) para monitoreo de baja latencia, configure el tono aquí en lugar de hacerlo a través de la ruta de sidetone del radio.
- El generador de tono interno limita el tono a 100–4000 Hz independientemente de lo que muestre el control deslizante por encima de 4000 Hz.

## Relacionados

- [Hacer que el tono del sidetone local siga el tono CW del radio, o configurarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Habilitar el sidetone CW local de baja latencia (Local STn) para trabajo con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Escuchar un monitor de sidetone TX](listen-to-a-tx-sidetone-monitor.md)
- [Ajustar el volumen del sidetone local de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
