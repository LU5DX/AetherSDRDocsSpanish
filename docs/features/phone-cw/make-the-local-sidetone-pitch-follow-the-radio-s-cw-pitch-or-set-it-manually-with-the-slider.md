# Hacer que el tono local de escucha CW siga el tono CW del radio, o ajustarlo manualmente con el deslizador

El generador local de tono de escucha (sidetone) en AetherSDR puede derivar su tono automáticamente del ajuste de tono CW del radio, o puede anularlo con una frecuencia fija mediante el deslizador de tono. Use esta página para cambiar entre los dos modos y ajustar el tono deseado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en un modo CW — el applet Phone/CW solo muestra los controles CW cuando CW está activo.
- Local STn debe estar habilitado. Si no lo está, habilítelo primero (consulte [Habilitar el tono local de escucha CW de baja latencia (Local STn) para trabajo con paleta / manipulador recto / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)).

## Pasos

### Para hacer que el tono siga el tono CW del radio (opción predeterminada)

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Localice el botón **Follow (local pitch)** en el subpanel de CW.
3. Haga clic en **Follow (local pitch)** para que quede marcado (activo). El tono local de escucha seguirá automáticamente el ajuste **Pitch < / >** del radio.

El deslizador **Local sidetone pitch** queda deshabilitado mientras **Follow (local pitch)** está activado.

### Para ajustar el tono manualmente

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **Follow (local pitch)** para desmarcarlo. El deslizador **Local sidetone pitch** quedará habilitado.
3. Arrastre el deslizador **Local sidetone pitch** hasta la frecuencia deseada. El rango de valores es 100–2000 Hz; el valor predeterminado es 600 Hz.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| **Follow (local pitch)** | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` |
| **Local sidetone pitch** | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

**Follow (local pitch):** Cuando está activado, el tono local de escucha refleja el tono CW del radio (ajustado mediante **Pitch < / >**). Cuando está desactivado, entra en efecto el deslizador manual **Local sidetone pitch**.

**Local sidetone pitch:** Establece la frecuencia del tono local de escucha en Hz. Solo está activo cuando **Follow (local pitch)** está desactivado. El generador subyacente limita internamente los valores al rango 100–4000 Hz, pero el deslizador expone 100–2000 Hz.

## Consejos

- El tono CW del radio se ajusta con el control giratorio **Pitch < / >** en el mismo subpanel de CW (rango 100–6000 Hz, paso 10 Hz). Cuando **Follow (local pitch)** está activado, el tono local de escucha sigue ese valor automáticamente — no es necesario actualizar el deslizador de tono por separado.
- El tono local de escucha funciona con una latencia aproximada de 10 ms, independientemente del monitor del radio alimentado por DAX. El ajuste de tono aquí no afecta al tono de escucha del radio, solo al generador en el lado del cliente.

## Solución de problemas

- **El deslizador Local sidetone pitch aparece en gris** — **Follow (local pitch)** está activado. Haga clic en **Follow (local pitch)** para desmarcarlo antes de ajustar el deslizador.
- **El tono local de escucha no cambia cuando cambia el tono CW del radio** — **Follow (local pitch)** está desactivado. Haga clic en **Follow (local pitch)** para habilitar el seguimiento automático.
- **No se escucha ningún tono local de escucha** — **Local STn** está desactivado. Habilítelo; consulte [Habilitar el tono local de escucha CW de baja latencia (Local STn) para trabajo con paleta / manipulador recto / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md).

## Relacionados

- [Cambiar el tono CW / frecuencia del tono de escucha](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el tono local de escucha CW de baja latencia (Local STn) para trabajo con paleta / manipulador recto / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Ajustar el volumen del tono local de escucha de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Escuchar un monitor de tono de escucha en TX](listen-to-a-tx-sidetone-monitor.md)
