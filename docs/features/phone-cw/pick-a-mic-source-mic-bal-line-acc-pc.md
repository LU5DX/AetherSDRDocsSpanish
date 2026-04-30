# Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza la radio como fuente de micrófono para transmisiones de voz. La selección determina de dónde obtiene la FLEX-8600 su audio de TX: del conector de micrófono del panel frontal, entrada balanceada, entrada de línea, puerto de accesorios o del sistema de audio de la PC.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra el subpanel Phone automáticamente en modos de voz.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el cuadro desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección entra en vigencia inmediatamente en la radio.

## Qué hace cada control

| Control        | Descripción                                                                                                                                                | Valor predeterminado |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada a la radio.                                                                                                     | —       |
| **Mic gain**   | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena en el lado del cliente porque la radio siempre reporta un nivel de 0 para fuentes PC. | 50      |

**Descripciones de fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono del puerto de accesorios.
- **PC** — Sistema de audio de la computadora. La radio no reporta el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Controles de sidetone de CW (v0.9.1+)

Cuando el slice activo está en un modo CW, el applet cambia al subpanel CW. El toggle **Sidetone** y el deslizador **Sidetone volume** controlan simultáneamente tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente (~10 ms de latencia). No hay controles de sidetone locales separados; un único conjunto de controles rige ambas rutas.

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Sidetone** | Habilita o deshabilita el sidetone de CW. Controla simultáneamente tanto el monitor alimentado por DAX de la radio como el generador de sidetone del cliente. | — | On / Off | — |
| **Sidetone volume** | Establece el volumen del sidetone tanto para el lado de la radio (`mon_gain_cw`) como para el generador del cliente. | — | 0–100 | — |
| **L / R pan (CW)** | Establece el paneo estéreo para el monitor CW y aplica paneo de potencia constante al generador de sidetone local. Haga doble clic para recentralizar en 50. | 50 | 0–100 | — |
| **Pitch < / >** | Ajusta el sidetone de CW y la frecuencia de decodificación en incrementos de 10 Hz. | 600 Hz | 100–6000 Hz | — |

La frecuencia y el paneo siempre siguen automáticamente los parámetros `cw_pitch` y `mon_pan_cw` de la radio. No hay toggle "Follow" separado ni deslizador de anulación manual de frecuencia; estos controles se eliminaron en v0.9.2.1.

## Consejos

- Cuando usa `PC` como fuente, el medidor **Level** aparece inmediatamente cuando AetherSDR se conecta a la radio, porque la medición de micrófono PC se ejecuta del lado del cliente independientemente de la configuración `met_in_rx` de la radio. El medidor no se suprime entre transmisiones para fuentes PC.
- Para mezclar el puerto de accesorios junto con su fuente principal, habilite el botón toggle **+ACC** después de seleccionar su fuente principal.
- A velocidades de CW más altas, la ruta de sidetone del lado del cliente (~10 ms de latencia) es más útil que el monitor alimentado por DAX de la radio. Dado que el toggle **Sidetone** controla ambas rutas juntas, habilitar sidetone siempre activa automáticamente la ruta de baja latencia.
- Cuando VOX se activa mediante atajo de teclado, el panel Phone se actualiza instantáneamente para reflejar el nuevo estado de VOX (v0.9.3).
- En Windows, la transmisión de sidetone de CW se inicia inmediatamente al conectarse (v0.9.3). Si sidetone está habilitado antes de conectarse, no se requieren pasos adicionales después de que se establezca la conexión.

## Solución de problemas

- **El combo de fuente de micrófono no muestra selección o se reinicia** — La lista se completa a partir de las entradas reportadas por la radio. Si el combo está vacío, verifique que la conexión de radio esté activa (`Settings > Connect to Radio...`).
- **El medidor de nivel no lee nada cuando la fuente es PC** — Este no es el comportamiento esperado en v0.9.3. El indicador **Level** debe aparecer inmediatamente al conectarse cuando la fuente de micrófono es `PC`. Si no aparece, verifique que AetherSDR ejecuta v0.9.3 o posterior. Para fuentes que no sean PC, el medidor se suprime a −150 dBFS cuando no se transmite y `met_in_rx` está desactivado; esto es normal.
- **La frecuencia del sidetone no coincide con lo esperado** — La frecuencia sigue automáticamente la configuración `cw_pitch` de la radio. Ajuste la frecuencia usando el cuadro de incremento **Pitch < / >**, que escribe directamente en la radio.
- **El sidetone no se inicia al conectarse (Windows)** — Este era un problema conocido en versiones anteriores a v0.9.3 causado por el orden de inicialización de AudioEngine. Actualice a v0.9.3 o posterior para resolverlo.

## Relacionado

- [Ajustar ganancia de micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
