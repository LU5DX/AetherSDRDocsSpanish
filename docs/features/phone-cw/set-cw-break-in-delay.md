# Ajustar el retardo de break-in de CW

El retardo de break-in de CW controla cuánto tiempo espera el equipo después de la última pulsación de la tecla antes de volver a recepción. Ajustar este valor evita una conmutación QSK entrecortada y, al mismo tiempo, permite un retorno rápido a RX entre palabras o caracteres.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El applet Phone/CW muestra los controles únicamente cuando hay una conexión de radio activa.
- El slice activo debe estar en un modo CW. El subpanel CW reemplaza automáticamente al subpanel Phone cuando se selecciona CW en el slice activo.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet es visible. Si el applet no está visible, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que el subpanel CW está visible. Si en cambio se muestran los controles Phone, cambie el slice activo a un modo CW mediante el selector de modo en el área principal del VFO.
3. Localice el control deslizante **Delay (CW)** en el subpanel CW.
4. Arrastre el control deslizante **Delay (CW)** hacia la izquierda para disminuir el retardo o hacia la derecha para aumentarlo. El valor se aplica al equipo de inmediato.

## Qué hace cada control

| Control | Descripción | Rango válido | Valor predeterminado | Clave de ajuste |
|---|---|---|---|---|
| Delay (CW) | Establece el retardo de break-in de CW. El equipo vuelve a recepción esta cantidad de milisegundos después del último elemento transmitido. | 0–2000 ms (paso 10) | — | — |
| Breakin | Activa o desactiva el break-in total (QSK). Cuando está habilitado, el equipo conmuta a recepción entre cada elemento. El control deslizante **Delay (CW)** sigue teniendo efecto cuando **Breakin** está desactivado. | On / Off | — | — |

## Consejos

- Un retardo de 0 ms con **Breakin** habilitado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste de los relés durante el envío rápido.
- El control deslizante **Delay (CW)** avanza en incrementos de 10 ms. Para un ajuste fino, haga clic en la pista del control deslizante y utilice las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).

## Temas relacionados

- [Habilitar el manipulador iámbico](enable-iambic-paddle-keying.md)
- [Ajustar la velocidad de manipulación CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono de CW / frecuencia del sidetone](change-cw-pitch-sidetone-frequency.md)
- [Escuchar el monitor de sidetone en TX](listen-to-a-tx-sidetone-monitor.md)
