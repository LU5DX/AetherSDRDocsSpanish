# Seleccione un perfil de micrófono para un micrófono específico

Utilice el cuadro combinado "Mic profile" en el applet Phone/CW para cargar un perfil de procesamiento de micrófono nombrado almacenado en la radio. Los diferentes micrófonos a menudo requieren diferentes configuraciones de EQ y procesamiento; cambiar de perfil aplica la configuración correcta para el micrófono conectado sin ajustar cada parámetro manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El cuadro combinado "Mic profile" solo se rellena cuando hay una conexión activa.
- El slice activo debe estar en un modo de voz (SSB, AM, FM). El applet Phone/CW muestra el subpanel Phone en modos de voz; en modo CW los controles de perfil de micrófono no son visibles.

## Pasos

1. Haga clic en el botón de bandeja "P/CW" en la barra lateral derecha para abrir el applet Phone/CW, si no está ya visible.
2. Confirme que se muestra el subpanel Phone. Si el applet muestra controles CW, el slice activo está en un modo CW — cambie primero el slice a un modo de voz.
3. Haga clic en el cuadro combinado "Mic profile". La lista se rellena a partir de los perfiles almacenados en la radio.
4. Seleccione el nombre del perfil que coincida con su micrófono. El perfil se carga inmediatamente.

## Qué hace cada control

| Control     | Tipo      | Comportamiento                                             |
|-------------|-----------|------------------------------------------------------|
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono nombrado en la radio. |

## Consejos

- Los nombres de perfil disponibles provienen de la radio, no de AetherSDR. Para crear o renombrar perfiles, utilice la gestión de perfiles de la propia radio. En AetherSDR también puede abrir `Profiles > Profile Manager...` para gestionar perfiles de transmisión.
- Seleccionar un perfil no cambia la configuración de "Mic source" o "Mic gain"; ajuste esos parámetros por separado si es necesario.

## Comportamiento del sidetone CW (v0.9.2.1)

En v0.9.2.1 se han eliminado el botón separado "Local STn", el regulador de volumen de sidetone local, el botón de alternancia "Follow" de pitch y el regulador manual de pitch local. El único botón **Sidetone** y el regulador **Sidetone volume** en el panel CW ahora controlan tanto el monitor alimentado por DAX de la radio como el generador de sidetone de baja latencia del lado del cliente (CwSidetoneGenerator, ~10 ms de latencia) en sincronía. Ya no hay controles de sidetone local independientes ni claves de configuración asociadas (`CwLocalSidetoneEnabled`, `CwLocalSidetoneVolume`, `CwLocalSidetonePitchFollow`, `CwLocalSidetonePitchHz`).

El pitch y el pan continúan siguiendo automáticamente la configuración `cw_pitch` y `mon_pan_cw` de la radio; no se necesita ni está disponible ningún anulación manual.

## Cambios en v0.9.3

### Medidor de nivel — excepción de fuente de micrófono PC

Anteriormente el medidor de nivel se suprimía a −150 dBFS cada vez que `met_in_rx` estaba apagado y la radio no estaba transmitiendo, independientemente de la fuente de micrófono. A partir de v0.9.3, esta supresión ya no se aplica cuando la fuente de micrófono seleccionada es **PC**. Como la medición de origen PC se controla mediante audio del lado del cliente en lugar del indicador `met_in_rx` de la radio, el medidor ahora aparece inmediatamente al conectarse cuando la fuente de micrófono está configurada en PC (#2086).

No ocurre ningún cambio en el comportamiento de las fuentes de micrófono de hardware (MIC, BAL, LINE, ACC); estas continúan siendo suprimidas cuando `met_in_rx` está apagado y la radio no está transmitiendo.

### El botón VOX ahora actualiza el panel Phone instantáneamente

Alternar VOX mediante un atajo de teclado ahora causa que el panel Phone se actualice inmediatamente. Anteriormente, el panel no se actualizaba hasta que ocurría algún otro evento de interfaz de usuario. Esto se corrigió haciendo que los setters VOX emitan `phoneStateChanged` (#2084).

### Flujo de sidetone en Windows

En Windows, el flujo de sidetone del lado del cliente (CwSidetoneGenerator) ahora se inicia correctamente tan pronto como AetherSDR se conecta a la radio. Un error en el orden de inicialización de AudioEngine impidió que el flujo se iniciara hasta que el applet fue interactuado manualmente (#2105).

## Relacionado

- [Elija una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajuste la ganancia del micrófono y habilite la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilite el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
