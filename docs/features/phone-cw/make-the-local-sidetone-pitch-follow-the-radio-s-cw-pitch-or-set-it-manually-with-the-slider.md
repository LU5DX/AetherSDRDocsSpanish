# Hacer que el tono local de escucha CW siga el tono CW del radio, o ajustarlo manualmente con el deslizador

Controle si el tono local de escucha CW del lado del cliente utiliza automáticamente el tono CW actual del radio, o si suena a una frecuencia fija que usted elige con un deslizador. Esto es útil cuando desea que el tono local de escucha permanezca sincronizado con el tono de decodificación del radio, o cuando prefiere un tono específico independientemente de la configuración del radio.

## Antes de comenzar

- El slice activo debe estar en un modo CW para que el subpanel CW sea visible en el applet Phone/CW.
- Local STn debe estar habilitado. Si no lo está, haga clic en Local STn en el applet Phone/CW para activarlo. Consulte [Habilitar el tono local de escucha CW de baja latencia (Local STn) para trabajo con paddle rápido / manipulador directo / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md).

## Pasos

### Para hacer que el tono siga el tono CW del radio

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Confirme que **Follow (local pitch)** esté marcado (encendido). Este es el estado predeterminado.
3. No se requiere ninguna acción adicional. El tono local de escucha ahora sigue el valor establecido en el control giratorio **Pitch < / >**.

### Para ajustar el tono manualmente

1. Abra el applet Phone/CW haciendo clic en el botón de bandeja **P/CW** en la barra lateral derecha.
2. Haga clic en **Follow (local pitch)** para desactivarlo. El deslizador **Local sidetone pitch** quedará habilitado.
3. Arrastre el deslizador **Local sidetone pitch** hasta la frecuencia deseada. El rango válido es de 100–2000 Hz; el valor predeterminado es 600 Hz.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Follow (local pitch)** | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` | Cuando está activado, el tono local de escucha sigue el tono CW del radio. Cuando está desactivado, se habilita el deslizador manual. |
| **Local sidetone pitch** | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` | Establece la frecuencia del tono local de escucha en Hz. Solo es ajustable cuando Follow (local pitch) está desactivado. |

## Consejos

- El tono CW del radio se ajusta con el control giratorio **Pitch < / >**, que avanza en incrementos de 10 Hz en el rango de 100–6000 Hz. Si usa Follow (local pitch), el tono local de escucha reflejará los cambios en ese control giratorio de forma inmediata.
- El generador de tono local de escucha limita internamente su tono a 100–4000 Hz, por lo que los valores superiores a 4000 Hz establecidos mediante el tono del radio serán limitados cuando Follow esté activado.

## Solución de problemas

- **El deslizador Local sidetone pitch aparece en gris y no se puede mover** — Follow (local pitch) está activado. Haga clic en **Follow (local pitch)** para desactivarlo y habilitar el deslizador.
- **El tono no cambia al mover el control giratorio Pitch < / > del radio** — Es posible que Follow (local pitch) esté desactivado. Haga clic en **Follow (local pitch)** para activarlo.

## Temas relacionados

- [Habilitar el tono local de escucha CW de baja latencia (Local STn) para trabajo con paddle rápido / manipulador directo / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Ajustar el volumen del tono local de escucha de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Cambiar la frecuencia del tono CW / tono de escucha](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de tono de escucha en TX](listen-to-a-tx-sidetone-monitor.md)
