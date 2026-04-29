# Abrir el editor completo del compresor para los controles de rodilla y limitador

El mosaico del applet expone cinco perillas — Thresh, Ratio, Attack, Release y Makeup —, pero los controles de anchura de rodilla y limitador solo están disponibles en el editor flotante. Esta página explica cómo abrir ese editor para el compresor TX o RX.

## Antes de comenzar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa COMP debe existir en el widget CHAIN para el lado que desea editar (TX o RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea editar — TX o RX.
2. Haga doble clic en la etapa COMP dentro del widget CHAIN.
   - Para el lado TX, esto abre el editor flotante titulado **Aetherial Compressor — TX**.
   - Para el lado RX, esto abre el editor flotante titulado **Aetherial Compressor — RX**.
3. Use los controles del editor flotante para ajustar los parámetros de rodilla y limitador. El editor contiene todos los controles del mosaico del applet más las secciones de rodilla y limitador que no están disponibles en el mosaico.

## Qué hace cada control

El editor flotante incluye las cinco perillas compartidas con el mosaico del applet más dos secciones adicionales: rodilla y limitador. Todos los valores se guardan por separado para cada lado.

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

Los valores predeterminados y los rangos válidos para Knee y Limiter ceiling no están especificados en la documentación disponible; consulte el editor flotante para ver los valores actuales.

## Consejos

- Los cambios realizados en el editor flotante se reflejan inmediatamente en la curva de transferencia y la barra de reducción de ganancia del mosaico del applet.
- Los editores TX y RX son completamente independientes. Abrir uno no afecta al otro.
- El editor flotante no tiene marco. Arrastre su barra de título para reposicionarlo.

## Solución de problemas

- **Hacer doble clic en COMP en el widget CHAIN no produce ningún efecto** — Es posible que la etapa COMP esté desactivada o que el motor de audio no esté conectado. Verifique que la etapa esté activa y que AetherSDR tenga un motor de audio en ejecución.
- **Los controles de rodilla y limitador no son visibles** — Es posible que esté mirando el mosaico del applet en lugar del editor flotante. El mosaico no expone los controles de rodilla ni de limitador. Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Ver la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
