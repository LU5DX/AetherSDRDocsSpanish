# Configurar el retardo de break-in de CW

El retardo de break-in de CW controla cuánto tiempo espera el radio después de la última pulsación de tecla antes de volver a recibir. Ajustar este valor evita una conmutación QSK entrecortada y, al mismo tiempo, permite un regreso rápido a RX entre palabras o caracteres.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW muestra los controles únicamente cuando hay una conexión de radio activa.
- El slice activo debe estar en un modo CW. El sub-panel de CW reemplaza automáticamente al sub-panel de Phone cuando se selecciona CW en el slice activo.

## Pasos

1. Localice el botón de bandeja **P/CW** en la barra lateral derecha y confirme que el applet sea visible. Si no lo es, haga clic en el botón de bandeja **P/CW** para mostrarlo.
2. Confirme que el sub-panel de CW esté visible. Si en cambio se muestran los controles de Phone, cambie el slice activo a un modo CW mediante el selector de modo en el área principal del VFO.
3. Localice el control deslizante **Delay (CW)** en el sub-panel de CW.
4. Arrastre el control deslizante **Delay (CW)** hacia la izquierda para disminuir el retardo o hacia la derecha para aumentarlo. El valor se aplica al radio de inmediato.

## Qué hace cada control

| Control | Descripción | Rango válido | Valor predeterminado | Clave de ajuste |
|---|---|---|---|---|
| Delay (CW) | Establece el retardo de break-in de CW. El radio regresa a recepción este número de milisegundos después del último elemento emitido. | 0–2000 ms (paso 10) | — | — |
| Breakin | Activa o desactiva el break-in completo (QSK). Cuando está habilitado, el radio conmuta a recepción entre cada elemento. El control deslizante **Delay (CW)** sigue teniendo efecto cuando **Breakin** está desactivado. | On / Off | — | — |

## Consejos

- Un retardo de 0 ms con **Breakin** habilitado proporciona operación QSK completa. Aumente el retardo para reducir el desgaste del relé durante el envío rápido.
- El control deslizante **Delay (CW)** avanza en incrementos de 10 ms. Para un ajuste fino, haga clic en la pista del control deslizante y use las teclas de flecha (si los atajos de teclado están habilitados en `View > Keyboard Shortcuts`).

## Relacionado

- [Habilitar el tecleo con paleta iámbica](enable-iambic-paddle-keying.md)
- [Configurar la velocidad de tecleo CW en WPM](set-cw-keying-speed-in-wpm.md)
- [Cambiar el tono de CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Habilitar el sidetone de CW local de baja latencia (Local STn) para trabajo con paleta, manipulador recto o CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Escuchar un monitor de sidetone de TX](listen-to-a-tx-sidetone-monitor.md)
