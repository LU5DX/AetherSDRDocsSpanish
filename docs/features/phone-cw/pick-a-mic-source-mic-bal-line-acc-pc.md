# Seleccionar la fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada física o virtual utiliza el radio como fuente de micrófono para las transmisiones de voz. La elección determina de dónde toma el FLEX-8600 el audio de TX: el conector de micrófono del panel frontal, la entrada balanceada, la entrada de línea, el puerto accesorio o el sistema de audio del PC.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM, etc.). El applet Phone/CW muestra el subpanel Phone automáticamente en los modos de voz.

## Pasos

1. Haga clic en el botón de bandeja `P/CW` en la barra lateral derecha para abrir el applet Phone/CW.
2. Localice el menú desplegable **Mic source** en el subpanel Phone.
3. Haga clic en **Mic source** y seleccione una de las fuentes disponibles: `MIC`, `BAL`, `LINE`, `ACC` o `PC`.

La selección surte efecto inmediatamente en el radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada al radio. | — | `MIC`, `BAL`, `LINE`, `ACC`, `PC` | — |
| **Mic gain** | Ajusta el nivel de entrada del micrófono. Cuando la fuente es `PC`, el valor se almacena en el lado del cliente porque el radio siempre reporta un nivel de 0 para las fuentes PC. | 50 | 0–100 | `PcMicGain` |

**Descripción de las fuentes:**

- **MIC** — Conector de micrófono del panel frontal.
- **BAL** — Entrada de micrófono balanceada.
- **LINE** — Entrada de nivel de línea.
- **ACC** — Entrada de micrófono por el puerto accesorio.
- **PC** — Sistema de audio del computador. El radio no reporta el nivel de micrófono para esta fuente; AetherSDR almacena el valor de ganancia localmente en `PcMicGain`.

## Consejos

- Al usar `PC` como fuente, el medidor **Level** del applet se suprime cuando no se está transmitiendo. Transmita brevemente para confirmar que el audio está pasando.
- Para mezclar el puerto accesorio junto con su fuente principal, active el botón de alternar **+ACC** después de seleccionar la fuente principal.

## Solución de problemas

- **El menú desplegable Mic source no muestra selección o se restablece** — La lista se llena a partir de las entradas reportadas por el radio. Si el menú está vacío, verifique que la conexión con el radio esté activa (`Settings > Connect to Radio...`).
- **El medidor de nivel no indica nada cuando la fuente es PC** — Esto es normal. El radio reporta `mic_level=0` para las fuentes PC; la ganancia es gestionada por `PcMicGain` en el lado del cliente.

## Temas relacionados

- [Ajustar la ganancia del micrófono y habilitar la mezcla del accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
