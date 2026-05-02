# Seleccionar un perfil de micrófono para un micrófono específico

Use el combo box "Mic profile" en el applet Phone/CW para cargar un perfil de procesamiento de micrófono con nombre almacenado en la radio. Los diferentes micrófonos suelen necesitar configuraciones distintas de ecualización y procesamiento; cambiar de perfil aplica la configuración correcta para el micrófono conectado sin ajustar cada parámetro manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El combo box "Mic profile" solo se llena cuando hay una conexión activa.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El applet Phone/CW muestra el subpanel Phone en modos de voz; en modo CW los controles de perfil de micrófono no son visibles.

## Pasos

1. Haga clic en el botón de bandeja "P/CW" en la barra lateral derecha para abrir el applet Phone/CW, si aún no está visible.
2. Confirme que el subpanel Phone está visible. Si el applet muestra los controles de CW, el slice activo está en modo CW — cambie primero el slice a un modo de voz.
3. Haga clic en el combo box "Mic profile". La lista se llena con los perfiles almacenados en la radio.
4. Seleccione el nombre del perfil que corresponde a su micrófono. El perfil se carga inmediatamente.

## Qué hace cada control

| Control     | Tipo      | Comportamiento                                                   |
|-------------|-----------|------------------------------------------------------------------|
| Mic profile | Combo box | Carga el perfil de procesamiento de micrófono indicado en la radio. |

## Consejos

- Los nombres de perfil disponibles provienen de la radio, no de AetherSDR. Para crear o renombrar perfiles, utilice la gestión de perfiles propia de la radio. En AetherSDR también puede abrir `Profiles > Profile Manager...` para administrar perfiles de transmisión.
- Seleccionar un perfil no cambia los ajustes "Mic source" ni "Mic gain"; ajústelos por separado si es necesario.

## Comportamiento del sidetone de CW (v0.9.2.1)

En v0.9.2.1 se han eliminado el botón independiente "Local STn", el control deslizante de volumen del sidetone local, el toggle "Follow" de tono y el control deslizante manual de tono local. El toggle **Sidetone** y el control deslizante **Sidetone volume** en el panel CW ahora controlan de forma sincronizada tanto el monitor DAX de la radio como el generador de sidetone local de baja latencia del lado del cliente (CwSidetoneGenerator, latencia de ~10 ms). Ya no existen controles de sidetone local independientes ni claves de configuración asociadas (`CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow`, `CwLocalSidetonePitchHz`).

El tono y el paneo continúan siguiendo automáticamente los ajustes `cw_pitch` y `mon_pan_cw` de la radio; no se requiere ni está disponible ninguna anulación manual.

## Cambios en v0.9.3

### Medidor de nivel — excepción para la fuente de micrófono PC

Anteriormente, el medidor de nivel se suprimía a −150 dBFS siempre que `met_in_rx` estaba desactivado y la radio no estaba transmitiendo, independientemente de la fuente de micrófono. A partir de v0.9.3, esta supresión ya no se aplica cuando la fuente de micrófono seleccionada es **PC**. Dado que la medición con fuente PC está impulsada por el audio del lado del cliente en lugar del indicador `met_in_rx` de la radio, el medidor ahora aparece inmediatamente al conectarse cuando la fuente de micrófono está configurada como PC (#2086).

No hay cambio de comportamiento para las fuentes de micrófono por hardware (MIC, BAL, LINE, ACC); estas continúan siendo suprimidas cuando `met_in_rx` está desactivado y la radio no está transmitiendo.

### El toggle de VOX ahora actualiza el panel Phone instantáneamente

Activar o desactivar VOX mediante un atajo de teclado ahora provoca que el panel Phone se actualice de inmediato. Anteriormente, el panel no se actualizaba hasta que ocurría algún otro evento en la interfaz. Esto se corrigió haciendo que los setters de VOX emitan `phoneStateChanged` (#2084).

### Flujo de sidetone en Windows

En Windows, el flujo de sidetone del lado del cliente (CwSidetoneGenerator) ahora se inicia correctamente en cuanto AetherSDR se conecta a la radio. Un error en el orden de inicialización de AudioEngine impedía que el flujo se iniciara hasta que el applet era operado manualmente (#2105).

## Relacionado

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla del accesorio](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
