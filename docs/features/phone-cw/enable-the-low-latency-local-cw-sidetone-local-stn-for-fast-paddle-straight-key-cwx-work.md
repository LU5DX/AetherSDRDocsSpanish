# Habilitar la señal de monitoreo CW local de baja latencia (Local STn) para trabajo con paddle, manipulador recto o CWX

La señal de monitoreo CW local genera un tono de audio en el lado del cliente con aproximadamente 10 ms de latencia, independiente del monitor alimentado por DAX del radio. Úsela cuando la ruta de monitoreo del radio introduce demasiado retardo para operar cómodamente con paddle, manipulador recto o CWX.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600.
- El slice activo debe estar en un modo CW. El applet Phone/CW cambia automáticamente a su subpanel CW cuando hay un slice CW activo.
- El applet Phone/CW debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha.

## Pasos

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha. El subpanel CW aparece automáticamente cuando el slice activo está en modo CW.
2. Haga clic en **Local STn** para habilitar la señal de monitoreo local. El botón se activa cuando está habilitado. Esta configuración persiste como `CwLocalSidetoneEnabled`.
3. Ajuste el control deslizante **Local sidetone volume** a un nivel de escucha cómodo (0–100, predeterminado 50). Esta configuración persiste como `CwLocalSidetoneVolume`.
4. Elija una opción de tono:
   - Deje habilitado **Follow (local pitch)** (predeterminado) para que el tono de la señal de monitoreo local siga automáticamente la configuración de tono CW del radio. Esta configuración persiste como `CwLocalSidetonePitchFollow`.
   - O haga clic en **Follow (local pitch)** para desactivarlo y luego arrastre el control deslizante **Local sidetone pitch** hasta su frecuencia preferida (100–2000 Hz, predeterminado 600 Hz). Esta configuración persiste como `CwLocalSidetonePitchHz`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| **Local STn** | Apagado | Encendido / Apagado | `CwLocalSidetoneEnabled` | Habilita la señal de monitoreo CW de baja latencia en el lado del cliente (~10 ms). Funciona para transmisiones con paddle, manipulador recto y CWX. Independiente del monitor alimentado por DAX del radio. |
| **Local sidetone volume** | 50 | 0–100 | `CwLocalSidetoneVolume` | Establece el volumen de reproducción de la señal de monitoreo local. Independiente de la ganancia de monitoreo del radio. |
| **Follow (local pitch)** | Encendido | Encendido / Apagado | `CwLocalSidetonePitchFollow` | Cuando está encendido, el tono de la señal de monitoreo local sigue la configuración de tono CW del radio. Cuando está apagado, el control deslizante de tono manual está activo. |
| **Local sidetone pitch** | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` | Ajuste manual del tono de la señal de monitoreo local. Solo se puede ajustar cuando **Follow (local pitch)** está apagado. |

## Consejos

- La señal de monitoreo local funciona tanto para texto generado por CWX como para entrada de paddle y manipulador recto — no se necesita una configuración separada para CWX.
- El botón **Sidetone** y el control deslizante **Sidetone volume** del radio controlan el monitor del radio alimentado por DAX y son independientes de **Local STn**. Puede usar ambos simultáneamente o cualquiera de los dos por separado.
- Si usa **Follow (local pitch)**, al cambiar el tono del radio con el spinbox **Pitch < / >** (100–6000 Hz, paso 10) también se actualizará automáticamente el tono de la señal de monitoreo local.

## Resolución de problemas

- **El botón Local STn no es visible** — El subpanel CW solo aparece cuando el slice activo está en modo CW. Cambie el modo del slice a CW y el applet se actualizará automáticamente.
- **Sin audio de la señal de monitoreo local aunque Local STn esté habilitado** — Verifique que el dispositivo de salida de audio del sistema esté configurado y no silenciado. La señal de monitoreo local se reproduce a través del audio del sistema cliente, no a través del altavoz del radio.
- **El tono de la señal de monitoreo local no cambia al mover el control deslizante** — Confirme que **Follow (local pitch)** esté apagado. El control deslizante de tono solo está activo cuando Follow está deshabilitado.

## Relacionado

- [Cambiar la frecuencia de tono CW / señal de monitoreo](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de señal de monitoreo TX](listen-to-a-tx-sidetone-monitor.md)
- [Hacer que el tono de la señal de monitoreo local siga el tono CW del radio, o ajustarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Ajustar el volumen de la señal de monitoreo local independientemente del monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Habilitar la manipulación con paddle iámbico](enable-iambic-paddle-keying.md)
