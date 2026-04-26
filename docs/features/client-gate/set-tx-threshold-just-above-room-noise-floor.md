# Ajuste el umbral de TX justo por encima del piso de ruido ambiental

Configurar el control Thresh justo por encima del nivel de ruido ambiente indica a la puerta de TX que deje pasar la voz mientras silencia el siseo de fondo, el ruido del ventilador o el zumbido de la red eléctrica que permanece por debajo de ese nivel entre palabras.

## Antes de comenzar

- El Aetherial TX Gate debe estar habilitado mediante el widget CHAIN en el lado TX. El applet permanece oculto hasta que la etapa Gate esté activa.
- Abra el subcontenedor "Aetherial TX Gate" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante "Aetherial Gate — TX".

## Pasos

1. Coloque su estación en sus condiciones normales de operación: ruido de fondo presente, radio encendida, pero sin transmitir.
2. Observe la pelota de entrada en vivo sobre la curva de transferencia. La pelota muestra dónde se encuentra actualmente el ruido ambiental en la escala de entrada.
3. Observe la barra de reducción de ganancia (Gain-reduction). Mientras guarda silencio, la barra debe mostrar relleno ámbar, confirmando que la puerta está atenuando activamente.
4. Gire el control Thresh lentamente en sentido antihorario (hacia abajo) hasta que la barra de reducción de ganancia comience a llenarse de ámbar justo cuando deje de hablar. Este es el punto donde la puerta captura el ruido ambiental.
5. Gire Thresh en sentido horario (hacia arriba) entre 2 y 3 dB más allá de ese punto, de modo que el umbral quede holgadamente por encima del piso de ruido.
6. Hable con normalidad. La barra de reducción de ganancia debe despejarse de inmediato cuando comience a hablar y volver a llenarse dentro del tiempo de Release después de que se detenga. Si la puerta corta el inicio de las palabras, consulte [Ajuste de ataque/release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de persistencia | Comportamiento |
|---|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la puerta comienza a atenuar. Configúrelo justo por encima del piso de ruido. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Agresividad con la que la puerta corta por debajo del umbral. Valores más altos producen cortes más pronunciados. |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Rapidez con la que la puerta se abre cuando la entrada supera el umbral. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Rapidez con la que la puerta se cierra tras caer la entrada por debajo del umbral. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la puerta puede aplicar. Evita el silencio total entre palabras. |

La **curva de transferencia** (Transfer curve) grafica la relación estática entrada/salida y muestra una pelota en vivo en el nivel de entrada actual. La **barra de reducción de ganancia** (Gain-reduction bar) es una franja horizontal ámbar, rellena desde la derecha, con escala de 0 a 40 dB; una marca indica el piso predeterminado de −15 dB.

## Consejos

- Ajuste Thresh de forma auditiva usando la barra de reducción de ganancia como guía: la barra debe estar completamente iluminada durante el silencio y despejarse en el momento en que comience a hablar.
- Deje Floor en −15.0 dB inicialmente. Un piso tan superficial evita que el audio caiga a un silencio muerto antinatural entre palabras. Auméntelo solo si el piso de ruido es lo suficientemente alto como para resultar audible a ese nivel.
- Si la pelota de entrada nunca supera el umbral al hablar, Thresh está configurado demasiado alto. Bájelo hasta que la pelota cruce la línea de umbral en los picos de voz.
- Los cambios en cualquier control surten efecto de inmediato y se guardan automáticamente. No se requiere ningún paso de confirmación adicional.

## Solución de problemas

- **La puerta corta el inicio de las palabras** — Attack es demasiado lento, o Thresh está configurado demasiado cerca del nivel de su voz. Baje Thresh entre 3 y 5 dB o reduzca Attack. Consulte [Ajuste de ataque/release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).
- **La barra de reducción de ganancia permanece vacía incluso durante el silencio** — Thresh está configurado por debajo del piso de ruido. Suba Thresh hasta que la barra muestre relleno ámbar cuando la sala esté en silencio.
- **La puerta oscila rápidamente (chattering)** — Thresh está configurado justo en el límite del piso de ruido. Suba Thresh entre 2 y 3 dB para crear separación entre el nivel de ruido y el umbral.
- **El applet no es visible** — La etapa Gate no está habilitada en la cadena TX. Habilítela mediante el widget CHAIN. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Observar la reducción de ganancia en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Ajuste de ataque/release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Configurar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir el comportamiento de puerta vs. expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
