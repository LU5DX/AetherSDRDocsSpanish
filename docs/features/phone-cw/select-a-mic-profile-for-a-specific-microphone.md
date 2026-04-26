# Seleccionar un perfil de micrófono para un micrófono específico

El applet Phone/CW permite cargar un perfil de procesamiento de micrófono con nombre almacenado en el radio. Úselo cuando cambie entre micrófonos que requieran ajustes diferentes de ecualización, compresión o ganancia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El cuadro combinado "Mic profile" se llena con la lista de perfiles del radio y aparecerá vacío si no hay conexión.
- El slice activo debe estar en un modo Phone (SSB, AM, FM). En modo CW, el applet muestra los controles CW en lugar de los controles Phone.

## Pasos

1. Abra el panel de applets si no está visible. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha, o use `View > Applet Panel` para mostrar el panel.
2. Confirme que se muestra el sub-panel Phone. Si se muestran los controles CW, el slice activo está en modo CW — cambie primero el slice a un modo de voz.
3. Localice el cuadro combinado **Mic profile**. Aparece directamente debajo de los medidores Level y Compression, encima de la fila **Mic source**.
4. Haga clic en el cuadro combinado **Mic profile** y seleccione el nombre del perfil que corresponde a su micrófono.

El radio carga el perfil seleccionado de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|---|
| Mic profile | Cuadro combinado | Carga el perfil de procesamiento de micrófono con nombre en el radio. | — | Se llena desde la lista de perfiles del radio | — |

## Consejos

- Los perfiles se almacenan en el radio, no en AetherSDR. Para crear o eliminar perfiles, use `Profiles > Profile Manager...`.
- Después de cambiar de perfil, observe el medidor **Level** (−40 a +10 dBFS, rojo por encima de 0) para confirmar que la ganancia del nuevo perfil es adecuada para su micrófono.
- Si utiliza un micrófono de PC (Mic source configurado en **PC**), el valor de ganancia del micrófono se mantiene en el lado del cliente como `PcMicGain` y no se ve afectado por la carga del perfil.

## Solución de problemas

- **El cuadro combinado "Mic profile" está vacío** — El radio no tiene perfiles de micrófono guardados, o AetherSDR no está conectado. Verifique el estado de la conexión y luego use `Profiles > Profile Manager...` para crear al menos un perfil.
- **Seleccionar un perfil no produce ningún efecto audible** — Compruebe que **Mic source** esté configurado en la entrada a la que está conectado físicamente su micrófono. Un perfil cargado para una fuente no modificará el procesamiento de una fuente diferente.

## Relacionados

- [Seleccionar una fuente de micrófono (MIC, BAL, LINE, ACC, PC)](pick-a-mic-source-mic-bal-line-acc-pc.md)
- [Ajustar la ganancia del micrófono y habilitar la mezcla de accesorios](adjust-mic-gain-and-enable-the-accessory-mix.md)
- [Habilitar el procesador de voz en nivel NOR, DX o DX+](enable-speech-processor-at-nor-dx-or-dx-level.md)
