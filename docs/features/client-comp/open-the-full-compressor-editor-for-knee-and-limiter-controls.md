# Abra el Editor Completo del Compresor para los Controles de Knee y Limitador

El mosaico del applet expone cinco perillas — Thresh, Ratio, Attack, Release y Makeup — pero los controles del ancho de rodilla (knee) y del limitador solo están disponibles en el editor flotante. Esta página explica cómo abrir ese editor para el compresor de TX o RX.

## Antes de empezar

- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets.
- La etapa COMP debe existir en el widget CHAIN para el lado que desea editar (TX o RX).

## Pasos

1. Localice el widget CHAIN para el lado que desea editar — TX o RX.
2. Haga doble clic en la etapa COMP en el widget CHAIN.
   - Para el lado TX, esto abre el editor flotante titulado **Aetherial Compressor — TX**.
   - Para el lado RX, esto abre el editor flotante titulado **Aetherial Compressor — RX**.
3. Use los controles en el editor flotante para ajustar los parámetros de knee y limitador. El editor contiene todos los controles del mosaico del applet más las secciones de knee y limitador no disponibles en el mosaico.

## Función de cada control

El editor flotante incluye las cinco perillas compartidas con el mosaico del applet más dos secciones adicionales: knee y limitador. Todos los valores se guardan por lado.

### Lado TX

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |
| Knee | — | — | `ClientCompTxKneeDb` |
| Limitador activado | — | — | `ClientCompTxLimEnabled` |
| Techo del limitador | — | — | `ClientCompTxLimCeilingDb` |

### Lado RX

| Control | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompRxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompRxRatio` |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompRxReleaseMs` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompRxMakeupDb` |
| Knee | — | — | `ClientCompRxKneeDb` |
| Limitador activado | — | — | `ClientCompRxLimEnabled` |
| Techo del limitador | — | — | `ClientCompRxLimCeilingDb` |

Los valores predeterminados y rangos válidos para Knee y el techo del limitador no están especificados en la documentación disponible; consulte el editor flotante para conocer los valores actuales.

## Controles del mosaico del applet

Cuando el compresor se muestra en el panel de applets (modo compacto), los siguientes controles e indicadores están disponibles sin abrir el editor flotante:

| Elemento | Etiqueta | Tipo | Comportamiento |
|---|---|---|---|
| Curva de transferencia | — | indicador | Dibuja la curva de transferencia de entrada/salida más un punto móvil que muestra el nivel actual de la envolvente. Solo visualización en el applet; editable en el editor flotante. |
| Barra de reducción de ganancia | — | medidor | Barra horizontal ámbar, rellena hacia la derecha. La escala máxima es 20 dB de reducción; una marca en -6 dB señala una cantidad de trabajo típica. Se actualiza a ~30 Hz. |
| Perilla | Thresh | perilla | Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. Valor predeterminado -18.0 dB, rango -60.0 a 0.0 dB. Clave de configuración: `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX). |
| Perilla | Ratio | perilla | Mapeo logarítmico (1 * 20^n). Define qué tan fuerte se contienen los picos una vez que se supera el umbral. Valor predeterminado 3.0, rango 1.0 a 20.0. La etiqueta tiene el formato 'X.XX:1'. |
| Perilla | Attack | perilla | Mapeo exponencial (0.1 * 3000^n). Define qué tan rápido el compresor se activa después de superar el umbral. Valor predeterminado 20.0 ms, rango 0.1 a 300.0 ms. La etiqueta tiene el formato 'X.X ms' por debajo de 10, 'X ms' por encima. |
| Perilla | Release | perilla | Mapeo exponencial (5 * 400^n). Define qué tan rápido regresa la ganancia después de que la entrada cae por debajo del umbral. Valor predeterminado 200 ms, rango 5 a 2000 ms. La etiqueta tiene el formato 'X ms'. |
| Perilla | Makeup | perilla | Mapeo lineal. Agrega ganancia para compensar la pérdida por compresión. Valor predeterminado 0.0 dB, rango -12.0 a 24.0 dB. La etiqueta muestra un signo '+' explícito para valores positivos. |

## Consejos

- Los cambios realizados en el editor flotante se reflejan inmediatamente en la curva de transferencia y la barra de reducción de ganancia del mosaico del applet.
- Los editores de TX y RX son completamente independientes. Abrir uno no afecta al otro.
- El editor flotante no tiene marco. Arrastre su barra de título para reposicionarlo.
- Cuando la etapa del compresor está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio.
- Para escribir un valor preciso en cualquier perilla del mosaico del applet, haga clic directamente en la etiqueta del valor. Aparece un pequeño editor de texto en línea. Escriba el nuevo valor y presione Enter o haga clic en cualquier otro lugar para confirmar. Presione Escape para cancelar la edición y restaurar el valor anterior. Esta función está disponible en las cinco perillas (Thresh, Ratio, Attack, Release, Makeup) del mosaico del applet. Los valores se ajustan automáticamente al rango válido.

## Solución de problemas

- **Al hacer doble clic en COMP en el widget CHAIN no sucede nada** — La etapa COMP puede estar en bypass o el motor de audio puede no estar conectado. Verifique que la etapa esté activa y que AetherSDR tenga un motor de audio en ejecución.
- **Los controles de knee y limitador no son visibles** — Es posible que esté mirando el mosaico del applet en lugar del editor flotante. El mosaico no expone los controles de knee ni de limitador. Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está actualmente en bypass. Active la etapa COMP en el widget CHAIN para restaurar la opacidad completa y reanudar el procesamiento.
- **La edición en línea no aparece al hacer clic en el valor de la perilla** — Asegúrese de hacer clic directamente en el texto del valor (la etiqueta numérica debajo de la perilla), no en el gráfico de la perilla. El editor en línea solo se activa al hacer clic en el área de texto.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ponga el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Ajuste el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Observe la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
