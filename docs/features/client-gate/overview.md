# Descripción general del Noise Gate / Expander

El Noise Gate / Expander es un expansor descendente en el lado TX que atenúa el audio que cae por debajo de un nivel establecido. Úselo para suprimir el ruido de fondo, el zumbido de ventiladores y la reverberación ambiental entre palabras, sin necesidad de operar manualmente un gate de hardware.

## Antes de comenzar

- El applet GATE permanece oculto hasta que la etapa Gate se habilite desde el widget CHAIN o desde el editor flotante Gate. Habilite primero la etapa desde allí.
- El applet reside dentro del contenedor principal PooDoo Audio (TXDSP). Asegúrese de que el panel de applets sea visible (`View > Applet Panel`).

## Cómo funciona

Cuando el audio del micrófono cae por debajo del nivel **Thresh**, el gate comienza a atenuar la señal. La profundidad y la velocidad de esa atenuación se controlan mediante **Ratio**, **Attack**, **Release** y **Floor**.

Con un **Ratio** de 2.0:1 (el valor predeterminado), el gate actúa como un expansor descendente suave: el audio por debajo del umbral se reduce gradualmente. Con valores de ratio más altos (cercanos a 10.0:1), el corte se vuelve más pronunciado y el comportamiento se aproxima a un gate rígido. El control **Floor** limita la atenuación máxima para que el gate nunca genere un silencio artificialmente completo.

El applet muestra dos indicadores en tiempo real mientras transmite o monitorea:

- **Curva de transferencia** — un gráfico de curva estático con una bola animada que se desplaza al nivel de entrada actual, indicando si el gate está abierto (bola por encima del umbral) o cerrado (bola por debajo del umbral).
- **Barra de reducción de ganancia** — una franja ámbar horizontal que se rellena desde la derecha. La escala va de 0 a 40 dB de reducción de ganancia. Una marca en −15 dB indica el valor predeterminado de **Floor**.

Los cinco controles del applet están conectados directamente al motor de audio. Los cambios realizados aquí se reflejan inmediatamente en el editor flotante Gate, y viceversa. Los ajustes se guardan automáticamente después de cada modificación.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` |
| Ratio | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` |

**Thresh** — el nivel por debajo del cual el gate comienza a atenuar. Ajústelo justo por encima del nivel de ruido ambiental de la sala, para que la voz abra el gate de forma limpia.

**Ratio** — controla la intensidad del corte. Valores bajos (cercanos a 1.0:1) producen una expansión descendente suave. Valores altos (cercanos a 10.0:1) producen un corte abrupto similar a un gate rígido.

**Attack** — velocidad con la que el gate se abre cuando la entrada supera el umbral. Utiliza una escala exponencial (0.1 ms a 100.0 ms). Valores de ataque más rápidos permiten que el borde inicial de cada palabra pase de inmediato.

**Release** — velocidad con la que el gate se cierra después de que la entrada cae por debajo del umbral. Utiliza una escala exponencial (5 ms a 2000 ms). Valores de release más largos generan una caída más natural; valores muy cortos pueden producir un sonido entrecortado.

**Floor** — la reducción de ganancia máxima que el gate puede aplicar. Con el valor predeterminado de −15.0 dB, el ruido de fondo se reduce hasta 15 dB en lugar de silenciarse por completo. Establezca un valor más bajo para un corte más pronunciado, o más alto para ser más conservador.

El estado activo o en bypass de la etapa gate se guarda en `ClientGateTxEnabled`.

## Consejos

- Observe la bola de la curva de transferencia y la barra de reducción de ganancia mientras no habla. Si la barra muestra un relleno ámbar considerable en reposo, el gate está funcionando. Si la bola rara vez cruza el umbral durante la voz, es posible que **Thresh** esté configurado demasiado alto.
- El editor flotante Gate y los controles del applet GATE permanecen sincronizados. No es necesario abrir el editor para ajustes rutinarios de umbral o de Floor.
- Haga clic derecho en la barra de título del subcontenedor GATE para flotar, desprender u ocultar el applet si necesita más espacio en pantalla.

## Temas relacionados

- [Ajustar el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
- [Elegir entre comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar el attack y el release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Configurar el Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
- [Poner el gate en bypass desde la cadena](bypass-the-gate-from-the-chain.md)
