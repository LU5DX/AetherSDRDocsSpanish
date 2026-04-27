# Ajuste el umbral TX justo por encima del nivel de ruido de la sala

Configurar Thresh correctamente indica a la compuerta TX dónde termina el ruido de fondo de su sala y dónde comienza su voz. Un umbral justo por encima del nivel de ruido mantiene el silencio entre transmisiones, suprimiendo el siseo del micrófono y el sonido ambiente, mientras que deja pasar su voz con claridad.

## Antes de comenzar

- La etapa de compuerta TX debe estar habilitada en el widget CHAIN del lado TX. Si no está habilitada, el applet queda oculto y los cambios en los controles no tienen efecto. Consulte [Omitir la compuerta desde la cadena](bypass-the-gate-from-the-chain.md).
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".

## Pasos

1. Póngase los auriculares y deje la sala en sus condiciones ambiente normales: ventilador encendido, ruido del equipo presente, lo que sea habitual cuando opera.
2. No hable. Observe la bola de entrada en vivo sobre la curva de transferencia (Transfer curve). La bola indica dónde se sitúa el ruido de su sala sobre el eje de entrada.
3. Observe la barra de reducción de ganancia (Gain-reduction). Si la barra no muestra relleno ámbar mientras guarda silencio, Thresh ya está por debajo del nivel de ruido y la compuerta no se cierra — suba Thresh.
4. Gire el control Thresh lentamente en sentido horario hasta que la barra ámbar de reducción de ganancia comience a llenarse de forma consistente mientras guarda silencio. Ese es el nivel de ruido de la sala.
5. Reduzca Thresh entre 2 y 3 dB para que la compuerta se cierre firmemente sobre el ruido sin cortar el flanco inicial de su voz. La bola de entrada debe quedar claramente por debajo de la línea de umbral cuando usted está en silencio.
6. Hable a volumen normal. Confirme que la barra de reducción de ganancia baja a cero (sin relleno) de forma inmediata al comenzar a hablar, lo que indica que la compuerta se ha abierto.
7. Vuelva al silencio. Confirme que el relleno ámbar regresa con prontitud. Si la compuerta tarda en cerrarse, reduzca Release. Consulte [Ajustar ataque / liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).

## Función de cada control

| Control | Valor por defecto | Rango válido | Clave persistente | Comportamiento |
|---|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la compuerta comienza a atenuar. Configúrelo justo por encima del nivel de ruido de la sala. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Valores más altos producen un corte más pronunciado; valores más bajos producen una expansión descendente más suave. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Rapidez con la que la compuerta se abre cuando la entrada supera Thresh. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Rapidez con la que la compuerta se cierra después de que la entrada cae por debajo de Thresh. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que puede aplicar la compuerta. Evita el silencio total entre palabras. |

La curva de transferencia (Transfer curve) representa la relación estática entrada/salida y muestra una bola de entrada en vivo con el nivel de señal actual. La barra de reducción de ganancia (Gain-reduction) es una franja horizontal ámbar, rellena desde la derecha, con escala de 0 a 40 dB; una marca señala la posición predeterminada de Floor en −15 dB.

## Consejos

- Ajuste Thresh durante la condición de ruido más desfavorable (ventilador al máximo, mayor actividad de fondo). Un umbral calibrado en una sala silenciosa dejará pasar el ruido cuando las condiciones cambien.
- Si la compuerta corta el inicio de las palabras, reduzca Attack o disminuya Thresh entre 1 y 2 dB para que la compuerta se abra más rápido o se active antes.
- La barra de reducción de ganancia y la bola de entrada se actualizan en vivo a aproximadamente 30 Hz, por lo que ráfagas de ruido breves serán visibles aunque sean cortas.
- Los cambios en cualquier control se guardan de inmediato y se conservan tras un reinicio. No es necesario confirmar ni aplicar por separado.

## Solución de problemas

- **El applet no es visible** — La etapa GATE no está habilitada. Haga clic una vez en la etapa GATE del widget CHAIN para habilitarla, o haga doble clic para abrir el editor flotante y habilitarla desde allí.
- **La barra de reducción de ganancia nunca se llena durante el silencio** — Thresh está configurado por debajo del nivel de ruido. Suba Thresh hasta que aparezca relleno ámbar de forma consistente durante el silencio.
- **La compuerta corta el inicio de las palabras** — Thresh está demasiado cerca del nivel de su voz, o Attack es demasiado lento. Reduzca Thresh ligeramente o disminuya el valor de Attack.
- **La compuerta no se cierra entre palabras** — Thresh es demasiado bajo para el nivel de ruido actual. Suba Thresh hasta que la barra se llene de forma fiable durante las pausas.

## Relacionados

- [Omitir la compuerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Ajustar ataque / liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Configurar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Elegir el comportamiento de compuerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
