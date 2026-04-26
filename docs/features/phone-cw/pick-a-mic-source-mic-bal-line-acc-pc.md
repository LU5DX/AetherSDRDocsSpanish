# Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)

Seleccione qué entrada de micrófono física o virtual utiliza el FLEX-8600 para la transmisión. La fuente correcta depende de cómo esté conectado su micrófono o dispositivo de audio a la radio.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM) para que el subpanel Phone sea visible en el applet Phone/CW.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet Phone/CW está visible. Si no lo está, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. En el subpanel Phone, busque el cuadro combinado **Mic source** en el lado izquierdo de la fila de ganancia de micrófono.
3. Haga clic en **Mic source** y seleccione una de las opciones disponibles: **MIC**, **BAL**, **LINE**, **ACC** o **PC**.

La selección surte efecto de inmediato. La radio cambia su entrada de audio de transmisión a la fuente elegida.

## Qué hace cada control

| Control | Descripción | Predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|
| **Mic source** | Selecciona la fuente de entrada de micrófono enviada a la radio. | — | MIC, BAL, LINE, ACC, PC | — |
| **Mic gain** | Ajusta el nivel de entrada para la fuente seleccionada (0–100). Cuando se selecciona **PC**, el valor se almacena en el lado del cliente porque la radio siempre reporta `mic_level=0` para esa fuente. | 50 | 0–100 | `PcMicGain` (solo fuente PC) |

## Consejos

- Cuando selecciona **PC**, la radio no reporta un nivel de micrófono a AetherSDR. AetherSDR almacena el valor de **Mic gain** localmente usando la configuración `PcMicGain` y lo restaura en la próxima sesión.
- El cuadro combinado **Mic source** se rellena a partir de la lista de entradas disponibles de la radio. Si el firmware de su radio expone entradas adicionales, estas aparecerán junto a las cinco opciones estándar.

## Relacionados

- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Seleccionar un perfil de micrófono para un micrófono específico](select-a-mic-profile-for-a-specific-microphone.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
