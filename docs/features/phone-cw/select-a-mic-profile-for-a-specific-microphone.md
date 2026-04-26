# Seleccionar un perfil de micrófono para un micrófono específico

El cuadro combinado **Mic profile** carga un perfil de procesamiento de transmisión con nombre almacenado en el radio, lo que permite cambiar rápidamente entre preajustes de ecualización y procesamiento optimizados para distintos micrófonos.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La lista **Mic profile** se obtiene del radio y aparece vacía cuando no hay conexión.
- El slice activo debe estar en un modo de voz (USB, LSB, AM, FM). El panel Phone no se muestra cuando el slice está en modo CW.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW, si no está visible todavía.
2. Confirme que el panel Phone está visible. Si en su lugar se muestra el panel CW, cambie el slice activo a un modo de voz.
3. Haga clic en el cuadro combinado **Mic profile**. La lista se completa con los perfiles almacenados en el radio.
4. Seleccione el nombre de perfil que corresponde a su micrófono. AetherSDR carga ese perfil en el radio de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango | Clave de ajuste |
|---|---|---|---|---|---|
| **Mic profile** | Cuadro combinado | Carga el perfil de procesamiento de micrófono indicado en el radio. | — | Se obtiene del radio | — |

## Consejos

- Los nombres de los perfiles se definen en el radio, no en AetherSDR. Para crear, renombrar o eliminar perfiles, use `Profiles > Profile Manager...`.
- Tras seleccionar un perfil, verifique el indicador **Level** (−40 a +10 dBFS, rojo por encima de 0) y el indicador **Compression** (−25 a 0 dB) para comprobar que los ajustes del perfil son adecuados para su micrófono.
- Si la fuente de micrófono es **PC**, el radio siempre reporta un nivel de micrófono de 0. Use el control deslizante **Mic gain** (0–100, predeterminado 50) para ajustar la ganancia en el lado del cliente; este valor se guarda como `PcMicGain`.

## Solución de problemas

- **El cuadro combinado Mic profile está vacío** — El radio no tiene perfiles de micrófono definidos, o AetherSDR no está conectado. Verifique la conexión mediante `Settings > Connect to Radio...` y, a continuación, cree un perfil con `Profiles > Profile Manager...`.
- **El panel Phone no está visible; se muestra el panel CW en su lugar** — El slice activo está en modo CW. Cambie el slice a un modo de voz para mostrar el panel Phone y el control **Mic profile**.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
