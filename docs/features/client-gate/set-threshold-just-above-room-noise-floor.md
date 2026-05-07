# Ajuste el umbral justo por encima del nivel de ruido ambiente

Ajuste el mando Thresh para que la compuerta se abra con su voz pero permanezca cerrada durante el ruido de fondo entre palabras. Un umbral demasiado bajo deja pasar el ruido ambiente; demasiado alto, recorta los inicios de la voz.

## Antes de empezar

- La etapa Gate debe estar habilitada en el widget CHAIN. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) si el applet GATE no es visible.
- Asegúrese de que haya una fuente de ruido típica presente en su estación (ventiladores, aire acondicionado, equipos cercanos) para que la lectura del piso de ruido sea representativa.
- El subcontenedor GATE debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).

## Pasos

1. Abra el applet GATE. Si no es visible, haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante, o haga clic derecho en la barra de título del subcontenedor GATE y seleccione la opción para mostrarlo.
2. Observe la curva de transferencia. La bola de entrada en vivo se mueve a lo largo de la curva en tiempo real, mostrando el nivel de entrada actual con relación al umbral.
3. Mire la barra de reducción de ganancia mientras **no habla**. Si no muestra relleno ámbar, el umbral ya está por encima del piso de ruido — continúe con el paso 6.
4. Gire lentamente el mando Thresh en sentido horario (hacia 0 dB) mientras observa la barra de reducción de ganancia. Deténgase cuando el relleno ámbar aparezca de forma constante mientras la sala está en silencio y usted no habla. Este punto es su piso de ruido.
5. Continúe girando Thresh en sentido horario 2–3 dB más allá de ese punto. Esto da un pequeño margen para que el ruido límite no haga que la compuerta oscile.
6. Hable a su nivel normal de micrófono. Confirme que la bola de entrada se eleva por encima de la línea de umbral en la curva de transferencia y que la barra de reducción de ganancia baja a casi cero mientras habla.
7. Vuelva al silencio. Confirme que la barra de reducción de ganancia se llena de ámbar, indicando que la compuerta está cerrada y atenuando el ruido de fondo.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la compuerta comienza a atenuar. Ajústelo por encima del piso de ruido. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Pendiente de atenuación por debajo del umbral. Valores más altos producen un corte más abrupto. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Velocidad con que la compuerta se abre cuando la entrada supera el umbral. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Velocidad con que la compuerta se cierra después de que la entrada cae por debajo del umbral. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la compuerta puede aplicar. |
| Curva de transferencia | — | — | — | Representa la curva de transferencia estática. La bola en vivo muestra el nivel de entrada actual y si la compuerta está abierta o cerrada. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. La marca en -15 dB señala el valor predeterminado de Floor. |

## Consejos

- Ajuste el umbral mientras el equipo está en una sesión de operación típica, no en una sala inusualmente silenciosa. El piso de ruido que importa es el presente durante el uso real.
- La escala de la barra de reducción de ganancia llega hasta 40 dB. Si la barra se llena completamente durante el ruido, la compuerta está aplicando la atenuación máxima; reduzca `ClientGateTxFloorDb` (más negativo) solo si necesita cortes más profundos.
- Los cambios en Thresh tienen efecto inmediato y se guardan automáticamente. No se requiere un paso de aplicación.
- Si el editor flotante de Gate y el applet GATE están ambos abiertos, los cambios de mando en una vista se sincronizan con la otra en aproximadamente 33 ms.

## Solución de problemas

- **La bola de entrada nunca supera la línea de umbral al hablar** — Thresh está demasiado alto. Gire el mando Thresh en sentido antihorario (hacia -80 dB) hasta que la bola cruce el umbral durante el habla normal.
- **La barra de reducción de ganancia no muestra relleno ni en silencio** — Thresh está por debajo del piso de ruido. Suba Thresh en sentido horario hasta que la barra muestre relleno ámbar cuando la sala esté en silencio.
- **La compuerta oscila rápidamente entre abierta y cerrada** — El umbral está exactamente sobre el piso de ruido. Suba Thresh otros 2–3 dB, o aumente Release para ralentizar el cierre. Consulte [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md).
- **El applet GATE no es visible** — La etapa Gate puede estar desactivada u oculta. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Noise Gate / Expander overview](overview.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Tune attack / release for natural open/close](tune-attack-release-for-natural-open-close.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md)
