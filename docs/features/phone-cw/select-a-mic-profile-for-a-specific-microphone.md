# Seleccionar un perfil de micrófono para un micrófono específico

El applet Phone/CW permite cargar un perfil de procesamiento de micrófono con nombre almacenado en el radio. Úselo cuando cambie entre micrófonos que requieren diferentes características de ecualización o ganancia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro combinado "Mic profile" solo se rellena cuando hay una conexión de radio activa.
- El slice activo debe estar en un modo Phone (SSB, AM, FM). En modo CW el panel Phone está oculto y "Mic profile" no es visible.
- Los perfiles de micrófono deben existir previamente en el radio. AetherSDR lee la lista desde el radio; no crea ni edita perfiles.

## Pasos

1. Haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el panel Phone está visible (no el panel CW). Si el panel CW está visible, cambie el slice activo a un modo de voz.
3. Haga clic en el cuadro combinado **Mic profile** en la parte superior del panel Phone.
4. Seleccione el nombre del perfil que corresponde a su micrófono.

El radio carga el perfil seleccionado de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento | Valor predeterminado | Valores válidos | Clave de configuración |
|---|---|---|---|---|---|
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono con nombre en el radio. La lista se obtiene del radio. | — | Nombres proporcionados por el radio | — |

## Sugerencias

- La lista "Mic profile" refleja los perfiles almacenados en el radio. Si falta un perfil que espera encontrar, créelo mediante SmartSDR o la gestión de perfiles del propio radio antes de conectar AetherSDR.
- Cambiar el perfil no afecta el valor del control deslizante **Mic gain**. Si utiliza la fuente **PC**, la ganancia se almacena localmente como `PcMicGain` (valor predeterminado 50, rango 0–100) y es independiente del perfil.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
