# Seleccionar un perfil de micrófono para un micrófono específico

Use el cuadro combinado "Mic profile" en el applet Phone/CW para cargar un perfil de procesamiento de micrófono con nombre almacenado en el radio. Los diferentes micrófonos suelen necesitar configuraciones distintas de ecualización y procesamiento; cambiar de perfil aplica la configuración correcta para el micrófono conectado sin ajustar cada parámetro manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro combinado "Mic profile" solo se rellena cuando hay una conexión activa.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El applet Phone/CW muestra el subpanel Phone en modos de voz; en modo CW los controles de perfil de micrófono no son visibles.

## Pasos

1. Haga clic en el botón de bandeja "P/CW" en la barra lateral derecha para abrir el applet Phone/CW, si no está visible.
2. Confirme que el subpanel Phone está visible. Si el applet muestra los controles de CW, el slice activo está en modo CW — cambie el slice a un modo de voz primero.
3. Haga clic en el cuadro combinado "Mic profile". La lista se rellena con los perfiles almacenados en el radio.
4. Seleccione el nombre de perfil que corresponde a su micrófono. El perfil se carga de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Valores válidos | Clave de ajuste |
|---|---|---|---|---|---|
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono con nombre en el radio. | — | Se rellena desde la lista de perfiles de micrófono del radio. | — |

## Consejos

- Los nombres de perfil disponibles provienen del radio, no de AetherSDR. Para crear o renombrar perfiles, use la gestión de perfiles propia del radio. En AetherSDR también puede abrir `Profiles > Profile Manager...` para administrar los perfiles de transmisión.
- Seleccionar un perfil no cambia los ajustes "Mic source" ni "Mic gain"; ajústelos por separado si es necesario.

## Comportamiento del sidetone de CW (v0.9.2.1)

En v0.9.2.1 se han eliminado el botón independiente "Local STn", el control deslizante de volumen del sidetone local, la opción "Follow" de tono y el control deslizante de tono local manual. El botón de alternancia **Sidetone** y el control deslizante **Sidetone volume** del panel CW ahora controlan de forma sincronizada tanto el monitor alimentado por DAX del radio como el generador de sidetone local de baja latencia del lado del cliente (CwSidetoneGenerator, latencia de ~10 ms). Ya no existen controles independientes de sidetone local ni las claves de ajuste asociadas (`CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow`, `CwLocalSidetonePitchHz`).

El tono y el panorama continúan siguiendo automáticamente los ajustes `cw_pitch` y `mon_pan_cw` del radio; no se necesita ni está disponible ninguna anulación manual.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
