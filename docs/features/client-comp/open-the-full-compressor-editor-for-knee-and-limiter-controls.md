# Abrir el Editor Completo del Compresor para los Controles de Curva y Limitador

El mosaico del applet expone cinco perillas — Thresh, Ratio, Attack, Release y Makeup — pero el ancho de la curva y los controles del limitador solo están disponibles en el editor flotante. Esta página explica cómo abrir ese editor para el compresor de TX o RX.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa COMP debe existir en el widget CHAIN para el lado que desea editar (TX o RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea editar — TX o RX.
2. Haga doble clic en la etapa COMP en el widget CHAIN.
   - Para el lado TX, esto abre el editor flotante titulado **Aetherial Compressor — TX**.
   - Para el lado RX, esto abre el editor flotante titulado **Aetherial Compressor — RX**.
3. Use los controles en el editor flotante para ajustar la curva y la configuración del limitador. El editor contiene todos los controles del mosaico del applet más las secciones de curva y limitador que no están disponibles en el mosaico.

## Función de cada control

El editor flotante incluye las cinco perillas compartidas con el mosaico del applet más dos secciones adicionales: curva y limitador. Todos los valores se conservan por lado.

### Lado TX

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |
| Knee | — | — | `ClientCompTxKneeDb` |
| Limiter enabled | — | — | `ClientCompTxLimEnabled` |
| Limiter ceiling | — | — | `ClientCompTxLimCeilingDb` |

### Lado RX

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompRxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompRxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompRxMakeupDb` |
| Knee | — | — | `ClientCompRxKneeDb` |
| Limiter enabled | — | — | `ClientCompRxLimEnabled` |
| Limiter ceiling | — | — | `ClientCompRxLimCeilingDb` |

Los valores predeterminados y rangos válidos para la curva (Knee) y el techo del limitador no están especificados en la documentación disponible; consulte el editor flotante para conocer los valores actuales.

## Consejos

- Los cambios realizados en el editor flotante se reflejan inmediatamente en la curva de transferencia y la barra de reducción de ganancia del mosaico del applet.
- Los editores de TX y RX son completamente independientes. Abrir uno no afecta al otro.
- El editor flotante no tiene marco. Arrastre su barra de título para reposicionarlo.
- Cuando la etapa del compresor está desviada, todo el mosaico del applet se atenúa aproximadamente al 55% de opacidad. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio.

## Solución de problemas

- **Hacer doble clic en COMP en el widget CHAIN no hace nada** — La etapa COMP podría estar desviada o el motor de audio podría no estar conectado. Verifique que la etapa esté activa y que AetherSDR tenga un motor de audio en ejecución.
- **Los controles de curva y limitador no son visibles** — Es posible que esté mirando el mosaico del applet en lugar del editor flotante. El mosaico no expone los controles de curva ni limitador. Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo.
- **El mosaico del applet parece atenuado** — La etapa del compresor está actualmente desviada. Habilite la etapa COMP en el widget CHAIN para restaurar la opacidad completa y reanudar el procesamiento.

## Relacionado

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Desviar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Ver la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
