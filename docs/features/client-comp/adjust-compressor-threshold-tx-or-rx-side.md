# Ajustar el Umbral del Compresor (Lado TX o RX)

Esta página explica cómo establecer el nivel de umbral en el cual el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) comienza a actuar. Bajar el umbral hace que el compresor actúe antes y afecte una mayor parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero atenuado a aproximadamente un 55% de opacidad. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico parece atenuado o si necesita volver a habilitar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe ser visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Busque el mando **Thresh** en la fila de cinco mandos en la parte inferior del mosaico.
3. Haga clic y arrastre el mando **Thresh** hacia arriba para subir el umbral o hacia abajo para bajarlo. La etiqueta debajo del mando se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Para ingresar un valor directamente, haga clic en la etiqueta de valor debajo de cualquier mando. Aparece una superposición QLineEdit con un sutil fondo oscuro y un borde cian. Escriba el valor deseado y presione Enter. El editor también confirma el valor cuando pierde el foco (por ejemplo, al hacer clic en otro lugar del applet). El valor se limita automáticamente al rango válido.
5. Observe la curva de transferencia y la bola de envolvente sobre la fila de mandos. Al ajustar el umbral, el punto de inflexión en la curva se desplaza y la posición de la bola en relación con la curva cambia para reflejar dónde cae el nivel de señal actual.
6. Observe la barra de reducción de ganancia. Un relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en −6 dB indica una cantidad de trabajo típica de reducción de ganancia.
7. Suelte el mando cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Qué hace cada control

| Control            | Valor predeterminado | Rango válido      | Clave de ajuste           | Notas                                                        |
|--------------------|----------------------|-------------------|---------------------------|--------------------------------------------------------------|
| Thresh             | −18.0 dB             | −60.0 a 0.0 dB    | `ClientCompTxThresholdDb` | Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. |
| Ratio              | 3.0                  | 1.0 a 20.0        | `ClientCompTxRatio`       | Mapeo logarítmico. Etiqueta formateada como `X.XX:1`.       |
| Attack             | 20.0 ms              | 0.1 a 300.0 ms    | `ClientCompTxAttackMs`    | Mapeo exponencial. Etiqueta `X.X ms` debajo de 10, `X ms` arriba. |
| Release            | 200 ms               | 5 a 2000 ms       | `ClientCompTxReleaseMs`   | Mapeo exponencial. Etiqueta formateada como `X ms`.         |
| Makeup             | 0.0 dB               | −12.0 a 24.0 dB   | `ClientCompTxMakeupDb`    | Mapeo lineal. La etiqueta muestra el signo `+` para valores positivos. |
| Curva de transferencia | —                 | —                 | —                         | ClientCompCurveWidget en modo compacto. Solo vista en el applet. |
| Barra de reducción de ganancia | —          | 0 a 20 dB GR      | —                         | Franja horizontal ámbar, relleno desde la derecha. Marca en −6 dB. |
| Drive              | 0.0 dB               | 0.0 a 18.0 dB     | `ClientCompTxDriveDb`     | Aumento de ganancia previo a la compresión con auto-makeup vinculado. Solo en StripCompPanel flotante. Etiqueta `+X.X dB`. |
| Phase              | 0 etapas             | 0 a 6 etapas      | `ClientCompTxPhaseRotatorStages` | Cascada de paso total para reducción de PAPR. Etiqueta `Off` cuando es 0, `N stg` cuando está activa. Solo en StripCompPanel flotante. |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y baje el umbral gradualmente mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de rodilla y limitador, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de rodilla y techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia proporciona retroalimentación visual inmediata: si la bola nunca sale del segmento recto inferior izquierdo, el umbral está configurado por encima de su nivel de señal típico y el compresor no está actuando.
- Para ingresar valores precisos, haga clic en la etiqueta de valor debajo de cualquier mando para abrir el editor en línea. Escriba el número (se admite la configuración regional; la coma como separador decimal es compatible) y presione Enter.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad del brillo. Esto es solo un indicador visual y no afecta ningún valor guardado de los mandos.
- La curva de transferencia y la bola de envolvente ahora respetan los colores del tema actual. El fondo, las líneas de cuadrícula, la curva y el resplandor de la bola reflejan la paleta del tema activo para una apariencia visual consistente en toda la aplicación.

## Solución de problemas

- **El mando Thresh está presente pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — La etapa del compresor puede estar aún en bypass, o el motor de audio no está funcionando. Confirme que la etapa esté habilitada a través del widget CHAIN y que el audio esté fluyendo.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Habilítela desde el widget CHAIN para restaurar el brillo completo y la activación del procesamiento. El mosaico permanece visible mientras está en bypass, a diferencia de versiones anteriores donde estaba oculto.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
