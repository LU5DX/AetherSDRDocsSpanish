# Seleccionar un perfil de micrófono para un micrófono específico

Use el cuadro combinado "Mic profile" en el applet Phone/CW para cargar un perfil de procesamiento de micrófono con nombre almacenado en el radio. Los distintos micrófonos suelen requerir ajustes de ecualización y procesamiento diferentes; cambiar de perfil aplica la configuración correcta para el micrófono conectado sin necesidad de ajustar cada parámetro de forma manual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro combinado "Mic profile" solo se rellena cuando hay una conexión activa.
- El slice (segmento de frecuencia) activo debe estar en un modo de voz (SSB, AM, FM). El applet Phone/CW muestra el subpanel Phone en modos de voz; en modo CW los controles de perfil de micrófono no son visibles.

## Pasos

1. Haga clic en el botón de bandeja "P/CW" en la barra lateral derecha para abrir el applet Phone/CW, si no está visible ya.
2. Confirme que se muestra el subpanel Phone. Si el applet muestra controles de CW, el slice activo está en modo CW — cambie el slice a un modo de voz primero.
3. Haga clic en el cuadro combinado "Mic profile". La lista se rellena con los perfiles almacenados en el radio.
4. Seleccione el nombre de perfil que corresponde a su micrófono. El perfil se carga de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|---|
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono con nombre indicado en el radio. | — | Obtenido de la lista de perfiles de micrófono del radio. | — |

## Consejos

- Los nombres de perfil disponibles provienen del radio, no de AetherSDR. Para crear o renombrar perfiles, use la gestión de perfiles propia del radio. En AetherSDR también puede abrir `Profiles > Profile Manager...` para administrar los perfiles de transmisión.
- Seleccionar un perfil no modifica los ajustes de "Mic source" ni de "Mic gain"; ajústelos por separado si es necesario.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Activar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
