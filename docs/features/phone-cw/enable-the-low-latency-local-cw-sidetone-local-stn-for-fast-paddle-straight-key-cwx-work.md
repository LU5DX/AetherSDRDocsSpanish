# Activar el tono lateral CW local de baja latencia (Local STn) para trabajo con paddle, manipulador recto o CWX

La función Local STn genera un tono lateral (sidetone) de CW completamente en su computadora con una latencia aproximada de 10 ms, independiente del monitor DAX del radio. Úsela cuando el retardo de ida y vuelta del tono lateral integrado del radio sea perceptible durante la operación rápida con paddle, manipulador recto o CWX.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión activa con el radio.
- Configure el slice activo en un modo CW. El subpanel de CW solo se muestra cuando el slice activo está en modo CW; en modos de voz, el applet muestra los controles Phone en su lugar.
- Confirme que la salida de audio del sistema esté configurada y funcionando: el tono lateral local se reproduce a través de la salida de audio de su computadora.

## Pasos

1. Haga clic en el botón **P/CW** de la bandeja en la barra lateral derecha para abrir el applet Phone/CW.
2. Cambie el slice activo a un modo CW si aún no lo ha hecho. El applet cambia automáticamente al subpanel de CW.
3. Haga clic en **Local STn** para activar el tono lateral local. El botón se activa y el generador de tono lateral del lado del cliente inicia. La configuración se guarda como `CwLocalSidetoneEnabled`.
4. Ajuste el control deslizante **Local sidetone volume** a un nivel cómodo. El valor predeterminado es 50; el rango es 0–100. Este valor se guarda como `CwLocalSidetoneVolume`.
5. De manera predeterminada, **Follow** está activado, lo que significa que el tono del tono lateral local sigue automáticamente la configuración de tono CW del radio. Si prefiere un tono fijo, haga clic en **Follow** para desactivarlo y luego ajuste el control deslizante **Local sidetone pitch** a la frecuencia deseada.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave guardada | Comportamiento |
|---|---|---|---|---|
| **Local STn** | Desactivado | Activado / Desactivado | `CwLocalSidetoneEnabled` | Activa el tono lateral CW de baja latencia del lado del cliente (~10 ms de latencia). Funciona con paddle, manipulador recto y transmisiones generadas por CWX. Independiente del monitor DAX del radio. |
| **Local sidetone volume** | 50 | 0–100 | `CwLocalSidetoneVolume` | Establece el volumen del tono lateral local. No afecta la ganancia del tono lateral del radio. |
| **Follow** | Activado | Activado / Desactivado | `CwLocalSidetonePitchFollow` | Cuando está activado, el tono del tono lateral local sigue el tono CW del radio. Cuando está desactivado, el control deslizante **Local sidetone pitch** se habilita para control manual. |
| **Local sidetone pitch** | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` | Establece la frecuencia de tono del tono lateral local en Hz. Solo está activo cuando **Follow** está desactivado. |

## Consejos

- El tono lateral local funciona tanto para transmisiones de texto CWX como para manipulación con paddle y manipulador recto. No es necesario cambiar ninguna configuración de CWX para recibir retroalimentación de tono lateral durante los envíos CWX.
- El botón **Sidetone** y el control deslizante **Sidetone volume** del radio controlan la ruta del monitor alimentado por DAX y son independientes de Local STn. Puede ejecutar ambos simultáneamente o usar cualquiera de los dos por separado.
- Si **Follow** está activado, cambiar el tono CW del radio mediante el cuadro giratorio **Pitch < / >** (100–6000 Hz, paso 10) también actualizará automáticamente el tono del tono lateral local.
- `CwLocalSidetoneEnabled` se guarda como `True` o `False` y se restaura en el siguiente inicio de la aplicación, por lo que Local STn permanece activado entre sesiones una vez habilitado.

## Solución de problemas

- **No se escucha sonido del tono lateral local al manipular** — Confirme que **Local STn** esté activo (botón marcado), que el control deslizante **Local sidetone volume** esté por encima de 0 y que la salida de audio del sistema funcione correctamente. El tono lateral local se reproduce a través de la salida de audio de la computadora, no a través del altavoz del radio.
- **El tono del tono lateral local no coincide con lo que escucha en recepción** — Verifique que **Follow** esté activado. Si está desactivado, el control deslizante **Local sidetone pitch** controla el tono de forma independiente a la configuración de tono CW del radio. Active **Follow** para volver a vincularlos.
- **El subpanel de CW no es visible** — El applet solo muestra los controles de CW cuando el slice activo está en modo CW. Cambie el modo del slice a CW y el panel aparecerá automáticamente.

## Relacionados

- [Escuchar un monitor de tono lateral TX](listen-to-a-tx-sidetone-monitor.md)
- [Hacer que el tono del tono lateral local siga el tono CW del radio, o configurarlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Ajustar el volumen del tono lateral local de forma independiente al monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Cambiar el tono CW / frecuencia del tono lateral](change-cw-pitch-sidetone-frequency.md)
- [Activar la manipulación con paddle iámbico](enable-iambic-paddle-keying.md)
