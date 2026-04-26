# Ajustar el Umbral Justo Por Encima del Ruido de Fondo

Ajuste el mando Thresh para que el gate se abra con su voz pero permanezca cerrado durante el ruido de fondo entre palabras. Un umbral demasiado bajo deja pasar el ruido ambiental; demasiado alto, recorta los bordes iniciales del habla.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el widget CHAIN. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md) si el applet GATE no está visible.
- Tenga presente una fuente de ruido típica en su estación (ventiladores, aire acondicionado, equipos cercanos) para que la lectura del piso de ruido sea representativa.
- El subcontenedor GATE debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Abra el applet GATE. Si no está visible, haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante Gate, o haga clic derecho en la barra de título del subcontenedor GATE y seleccione la opción para mostrarlo.
2. Observe la curva de transferencia. La bola de entrada en vivo se mueve a lo largo de la curva en tiempo real, mostrando el nivel de entrada actual en relación con el umbral.
3. Observe la barra Gain-reduction mientras **no está hablando**. Si no muestra relleno ámbar, el umbral ya está por encima del piso de ruido — pase al paso 6.
4. Gire el mando Thresh lentamente en sentido horario (hacia 0 dB) mientras observa la barra Gain-reduction. Deténgase cuando el relleno ámbar aparezca de forma constante mientras el ambiente está en silencio y usted no está hablando. Este punto es su piso de ruido.
5. Continúe girando Thresh en sentido horario 2–3 dB más allá de ese punto. Esto proporciona un margen pequeño para que el ruido límite no provoque que el gate fluctúe.
6. Hable a su nivel normal de micrófono. Confirme que la bola de entrada sube por encima de la línea de umbral en la curva de transferencia y que la barra Gain-reduction cae cerca de cero mientras habla.
7. Vuelva al silencio. Confirme que la barra Gain-reduction se llena de ámbar, lo que indica que el gate está cerrado y atenuando el ruido de fondo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual el gate comienza a atenuar. Auméntelo por encima del piso de ruido. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Pendiente de la atenuación por debajo del umbral. Valores más altos producen un corte más brusco. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Velocidad con la que el gate se abre cuando la entrada supera el umbral. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Velocidad con la que el gate se cierra después de que la entrada cae por debajo del umbral. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que el gate puede aplicar. |
| Curva de transferencia | — | — | — | Representa la curva de transferencia estática. La bola en vivo muestra el nivel de entrada actual e indica si el gate está abierto o cerrado. |
| Barra Gain-reduction | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. La marca en -15 dB señala el valor predeterminado de Floor. |

## Consejos

- Ajuste el umbral mientras la radio está en una sesión de operación típica, no en un ambiente inusualmente silencioso. El piso de ruido que importa es el presente durante el uso real.
- La escala de la barra Gain-reduction llega hasta 40 dB. Si la barra se llena completamente durante el ruido, el gate está aplicando la atenuación máxima; disminuya `ClientGateTxFloorDb` (valor más negativo) solo si necesita cortes más profundos.
- Los cambios en Thresh tienen efecto inmediato y se guardan automáticamente. No se requiere ningún paso de confirmación.
- Si el editor flotante Gate y el applet GATE están abiertos al mismo tiempo, los cambios en los mandos de cualquiera de las dos vistas se sincronizan con la otra en aproximadamente 33 ms.

## Solución de problemas

- **La bola de entrada nunca supera la línea de umbral al hablar** — Thresh está ajustado demasiado alto. Gire el mando Thresh en sentido antihorario (hacia -80 dB) hasta que la bola cruce el umbral durante el habla normal.
- **La barra Gain-reduction no muestra relleno ni en silencio** — Thresh está por debajo del piso de ruido. Aumente Thresh en sentido horario hasta que la barra muestre relleno ámbar cuando el ambiente esté en silencio.
- **El gate fluctúa rápidamente entre abierto y cerrado** — El umbral está exactamente sobre el piso de ruido. Aumente Thresh 2–3 dB adicionales, o incremente Release para ralentizar el tiempo de cierre. Consulte [Ajustar attack / release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md).
- **El applet GATE no está visible** — Es posible que la etapa Gate esté omitida u oculta. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Observar GR en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Ajustar attack / release para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir comportamiento de gate vs expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md)
