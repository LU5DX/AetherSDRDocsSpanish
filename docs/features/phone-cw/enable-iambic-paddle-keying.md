# Activar el tecleo con paleta iámbica

El tecleo con paleta iámbica le permite usar una llave de doble paleta con el codificador iámbico integrado del FLEX-8600. Esta página explica cómo activar el modo iámbico desde el applet Phone/CW de AetherSDR.

## Antes de comenzar

- El radio debe estar conectado. El applet Phone/CW no está disponible sin una conexión de radio activa.
- El slice activo debe estar en un modo CW. El subpanel de CW solo aparece cuando el modo del slice es CW; en modos de voz, el applet muestra los controles de Phone en su lugar.
- La paleta debe estar físicamente conectada al jack KEY del radio.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW. Si el applet ya está visible, omita este paso.
2. Confirme que el subpanel de CW esté visible. Si ve controles de micrófono y procesador, cambie primero el slice activo a un modo CW.
3. Haga clic en **Iambic** para activarlo. El botón se resalta cuando el modo iámbico está activo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| **Iambic** | Activa o desactiva el codificador de paleta iámbica en el radio. | — | On / Off | — |
| **Speed (CW)** | Establece la velocidad de tecleo. | — | 5–100 WPM | — |
| **Delay (CW)** | Establece el retardo de break-in de CW. | — | 0–2000 ms (paso 10) | — |
| **Breakin** | Activa o desactiva el break-in completo (QSK). | — | On / Off | — |
| **Pitch < / >** | Ajusta el tono del sidetone de CW y el tono de decodificación en pasos de 10 Hz. | 600 Hz | 100–6000 Hz | — |
| **Sidetone** | Activa o desactiva el monitor de sidetone de CW del radio. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del monitor de CW del radio. | — | 0–100 | — |
| **Local STn** | Activa o desactiva un sidetone de CW de baja latencia en el lado del cliente (~10 ms de latencia). | Off | On / Off | `CwLocalSidetoneEnabled` |
| **Local sidetone volume** | Establece el volumen del sidetone local de forma independiente al monitor del radio. | 50 | 0–100 | `CwLocalSidetoneVolume` |
| **Follow (local pitch)** | Cuando está activado, el tono del sidetone local sigue el tono de CW del radio. Cuando está desactivado, se habilita el control deslizante de tono manual. | On | On / Off | `CwLocalSidetonePitchFollow` |
| **Local sidetone pitch** | Tono manual del sidetone local en Hz; solo activo cuando **Follow** está desactivado. | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

## Consejos

- Para obtener la respuesta audible más rápida mientras teclea con la paleta, active **Local STn** además de **Sidetone** o en su lugar. El sidetone local se genera en el lado del cliente con aproximadamente 10 ms de latencia, en comparación con el monitor de radio alimentado por DAX, que introduce mayor retardo en la cadena de audio.
- Si desea que el tono del sidetone local coincida con lo que el radio decodifica, deje **Follow (local pitch)** activado. Desactívelo solo si desea establecer un tono diferente para su escucha.

## Resolución de problemas

- **El subpanel de CW no está visible** — El slice activo no está en modo CW. Cambie el modo del slice a CW; el applet cambia automáticamente.
- **El botón Iambic está visible pero la paleta no teclea** — Verifique que la paleta esté conectada al jack KEY del radio y que el firmware del radio reconozca la conexión. AetherSDR solo establece el modo del codificador; la conexión física es gestionada por el radio.

## Relacionados

- [Activar el sidetone de CW local de baja latencia (Local STn) para trabajo rápido con paleta, llave recta o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Establecer la velocidad de tecleo de CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Establecer el retardo de break-in de CW](set-cw-break-in-delay.md)
- [Cambiar el tono de CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
- [Hacer que el tono del sidetone local siga el tono de CW del radio, o establecerlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
