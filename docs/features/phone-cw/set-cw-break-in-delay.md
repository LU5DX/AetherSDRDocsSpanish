# Configurar el retardo de corte de CW

El retardo de corte de CW controla cuánto tiempo espera la radio después de la última pulsación de tecla antes de volver a recepción. Ajustar esto evita cambios QSK entrecortados mientras permite un retorno rápido a RX entre palabras o caracteres.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Phone/CW muestra controles solo cuando hay una conexión activa con la radio.
- El slice activo debe estar en un modo CW. El subpanel CW reemplaza automáticamente al subpanel Phone cuando se selecciona CW en el slice activo.

## Pasos

1. Ubique el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet sea visible. Si el applet no es visible, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que el subpanel CW esté visible. Si en su lugar se muestran los controles Phone, cambie el slice activo a un modo CW utilizando el selector de modo en el área VFO principal.
3. Ubique el regulador **Delay (CW)** en el subpanel CW.
4. Arrastre el regulador **Delay (CW)** hacia la izquierda para disminuir el retardo o hacia la derecha para aumentarlo. El valor se aplica a la radio inmediatamente.

## Qué hace cada control

| Control    | Descripción                                                                                                                                                           | Rango válido        |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| Delay (CW) | Establece el retardo de corte de CW. La radio vuelve a recepción después de esta cantidad de milisegundos desde el último elemento pulsado.                           | 0–2000 ms (paso 10) |
| Breakin    | Activa o desactiva el corte completo (QSK). Cuando está habilitado, la radio cambia a recepción entre cada elemento. El regulador **Delay (CW)** sigue teniendo efecto cuando **Breakin** está deshabilitado. | Activado / Desactivado            |

## Consejos

- Un retardo de 0 ms con **Breakin** habilitado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste de relés durante envío rápido.
- El regulador **Delay (CW)** avanza en incrementos de 10 ms. Para ajuste fino, haga clic en la pista del regulador y use las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).

## Notas para v0.9.3

- **Medidor de nivel (panel Phone):** Cuando la fuente de micrófono está configurada en **PC**, el medidor de nivel ahora aparece inmediatamente al conectar sin esperar a que la radio establezca la bandera `met_in_rx`. Esto ocurre porque la medición de micrófono de PC se ejecuta del lado del cliente e independiente de `met_in_rx`. Para todas las otras fuentes de micrófono, el comportamiento de supresión anterior se mantiene sin cambios: el medidor lee −150 dBFS cuando `met_in_rx` está desactivado y la radio no está transmitiendo.
- **Actualización de VOX / Panel Phone:** Los asignadores VOX ahora emiten `phoneStateChanged`, por lo que el subpanel Phone se actualiza al instante cuando VOX se activa/desactiva mediante un atajo de teclado. No es necesaria interacción manual en el panel para ver el estado actual de VOX.
- **Sidetone en Windows:** La secuencia de sidetone de CW (generador de baja latencia `CwSidetoneGenerator`) ahora se inicia inmediatamente al conectar en Windows. Si anteriormente tenía que activar y desactivar **Sidetone** después de conectar a la radio para escuchar el sidetone local, esta solución alternativa ya no es necesaria.

## Relacionado

- [Habilitar control de paleta iámbica](enable-iambic-paddle-keying.md)
- [Configurar la velocidad de keying CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar la frecuencia de pitch CW / sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
