# Configurar el retardo de break-in en CW

El retardo de break-in en CW controla cuánto tiempo espera el radio después de la última pulsación de tecla antes de volver a recepción. Ajustar este valor evita conmutaciones QSK irregulares y, al mismo tiempo, permite un retorno rápido a RX entre palabras o caracteres.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW muestra los controles únicamente cuando hay una conexión de radio activa.
- El slice activo debe estar en un modo CW. El subpanel CW reemplaza automáticamente al subpanel Phone cuando se selecciona CW en el slice activo.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet está visible. Si no lo está, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que el subpanel CW está desplegado. Si se muestran los controles Phone en su lugar, cambie el slice activo a un modo CW usando el selector de modo en el área principal del VFO.
3. Localice el control deslizante **Delay (CW)** en el subpanel CW.
4. Arrastre el control deslizante **Delay (CW)** hacia la izquierda para reducir el retardo o hacia la derecha para aumentarlo. El valor se aplica al radio de forma inmediata.

## Qué hace cada control

| Control    | Descripción                                                                                                                                                                                         | Rango válido        |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Delay (CW) | Establece el retardo de break-in en CW. El radio vuelve a recepción este número de milisegundos después del último elemento transmitido.                                                            | 0–2000 ms (paso 10) |
| Breakin    | Activa o desactiva el break-in completo (QSK). Cuando está habilitado, el radio conmuta a recepción entre cada elemento. El control deslizante **Delay (CW)** sigue teniendo efecto cuando **Breakin** está desactivado. | On / Off            |

## Consejos

- Un retardo de 0 ms con **Breakin** habilitado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste del relé durante el envío rápido.
- El control deslizante **Delay (CW)** avanza en incrementos de 10 ms. Para un ajuste fino, haga clic en la pista del control deslizante y use las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).

## Notas para v0.9.3

- **Indicador de nivel (panel Phone):** Cuando la fuente de micrófono está configurada como **PC**, el indicador de nivel aparece de inmediato al conectarse, sin esperar a que se active la bandera `met_in_rx` del radio. Esto se debe a que la medición del micrófono PC se ejecuta del lado del cliente y es independiente de `met_in_rx`. Para todas las demás fuentes de micrófono, el comportamiento de supresión anterior no cambia: el indicador muestra −150 dBFS cuando `met_in_rx` está desactivado y el radio no está transmitiendo.
- **Actualización de VOX / panel Phone:** Los ajustadores de VOX ahora emiten `phoneStateChanged`, por lo que el subpanel Phone se actualiza de forma instantánea cuando se activa o desactiva VOX mediante un atajo de teclado. No es necesaria ninguna interacción manual con el panel para ver el estado actual de VOX.
- **Sidetone en Windows:** El flujo de sidetone CW (generador de baja latencia `CwSidetoneGenerator`) ahora se inicia de forma inmediata al conectarse en Windows. Si anteriormente tenía que activar y desactivar **Sidetone** después de conectarse para escuchar el sidetone local, ya no es necesario aplicar ese procedimiento alternativo.

## Relacionados

- [Habilitar el keying con paleta iámbica](enable-iambic-paddle-keying.md)
- [Configurar la velocidad de keying CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone en TX](listen-to-a-tx-sidetone-monitor.md)
