# Ajustar el umbral del compresor (lado TX o RX)

Esta página explica cómo establecer el nivel de umbral en el que el Aetherial Compressor (TX) o el Aetherial AGC-C (RX) comienza a actuar. Reducir el umbral hace que el compresor se active antes y afecte a una mayor parte de su señal.

## Antes de comenzar

- El compresor debe estar habilitado (bypass desactivado) en el lado que desea ajustar. Cuando la etapa está en bypass, el mosaico del applet permanece visible pero atenuado aproximadamente al 55 % de opacidad. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico aparece atenuado o si necesita volver a habilitar la etapa.
- El contenedor principal Aetherial Audio (TXDSP) debe estar visible en el panel de applets. Si el panel de applets está oculto, haga clic en `View > Applet Panel` para mostrarlo.

## Pasos

1. Localice el subcontenedor **Aetherial Compressor** (lado TX) o **Aetherial AGC-C** (lado RX) en el panel de applets.
2. Encuentre el control **Thresh** en la fila de cinco controles en la parte inferior del mosaico.
3. Haga clic y arrastre el control **Thresh** hacia arriba para aumentar el umbral o hacia abajo para reducirlo. La etiqueta debajo del control se actualiza en tiempo real y muestra el valor actual en dB (por ejemplo, `-18.0 dB`).
4. Para ingresar un valor directamente, haga clic en la etiqueta de valor debajo de cualquier control. Aparece una superposición QLineEdit con un sutil fondo oscuro y borde cian. Escriba el valor deseado y presione Enter. El editor también confirma el valor cuando se pierde el foco (por ejemplo, al hacer clic en otro lugar del applet). El valor se limita automáticamente al rango válido.
5. Observe la curva de transferencia y la bola de envolvente sobre la fila de controles. Al ajustar el umbral, el punto de inflexión en la curva se desplaza y la posición de la bola con respecto a la curva cambia para reflejar dónde cae el nivel de señal actual.
6. Observe la barra de reducción de ganancia. El relleno ámbar que aparece desde la derecha indica compresión activa. Una marca en −6 dB indica una cantidad de trabajo típica de reducción de ganancia.
7. Suelte el control cuando el valor mostrado sea el deseado. El nuevo umbral se guarda automáticamente en `ClientCompTxThresholdDb` (TX) o `ClientCompRxThresholdDb` (RX).

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` / `ClientCompRxThresholdDb` | Establece el nivel de entrada por encima del cual comienza la compresión. Los valores más bajos activan el compresor antes. La asignación es lineal. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` / `ClientCompRxRatio` | Determina cuánto se contienen los picos una vez que se supera el umbral. La asignación es logarítmica (1 × 20^n). |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` | Establece la rapidez con la que el compresor se activa después de superar el umbral. La asignación es exponencial (0.1 × 3000^n). |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` | Establece la rapidez con la que la ganancia regresa después de que la entrada vuelve a estar por debajo del umbral. La asignación es exponencial (5 × 400^n). |
| Makeup | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` / `ClientCompRxMakeupDb` | Agrega ganancia perdida por la compresión. Asignación lineal. Los valores positivos muestran un signo '+' explícito. |
| Curva de transferencia | — | — | — | Visualización solo de la relación de ganancia entrada/salida. La bola de envolvente en vivo muestra dónde se encuentra la señal actual en la curva. Las etiquetas de los ejes se dibujan con QStaticText para un almacenamiento en caché de texto eficiente; las etiquetas se reconstruyen automáticamente cuando el applet cambia entre el modo compacto y el modo completo. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. Muestra cuánta atenuación está aplicando el compresor en este momento. La marca en −6 dB. |

## Consejos

- Comience con el valor predeterminado de −18.0 dB y reduzca gradualmente el umbral mientras habla (TX) o escucha una señal típica (RX) hasta que la barra de reducción de ganancia muestre unos pocos dB de relleno ámbar.
- Si desea que los cambios de umbral surtan efecto junto con los ajustes de knee y limitador, abra el editor completo haciendo doble clic en la etapa COMP en el widget CHAIN. Los controles de knee y techo del limitador solo están disponibles allí.
- La bola de envolvente en la curva de transferencia proporciona información visual inmediata: si la bola nunca sale del segmento recto inferior izquierdo, el umbral está establecido por encima de su nivel de señal típico y el compresor no está actuando.
- Para ingresar valores precisos, haga clic en la etiqueta de valor debajo de cualquier control para abrir el editor en línea. Escriba el número (con reconocimiento de configuración regional; se admite la coma como separador decimal) y presione Enter.
- Cuando la etapa está en bypass, todo el mosaico del applet se atenúa aproximadamente a la mitad del brillo. Esto es solo un indicador visual y no afecta ningún valor de control guardado.

## Solución de problemas

- **El control Thresh está presente, pero la barra de reducción de ganancia permanece vacía independientemente de la posición del umbral** — La etapa del compresor aún puede estar en bypass o el motor de audio no está funcionando. Confirme que la etapa esté habilitada a través del widget CHAIN y que fluya audio.
- **El mosaico del applet aparece atenuado** — La etapa del compresor está en bypass. Habilítela desde el widget CHAIN para restaurar el brillo completo y el procesamiento activo. El mosaico permanece visible mientras está en bypass, a diferencia de versiones anteriores donde estaba oculto.
- **El mosaico del applet no es visible en absoluto** — El contenedor principal Aetherial Audio (TXDSP) está colapsado. Expándalo en el panel de applets para revelar el mosaico.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Tune attack / release for a natural-sounding squeeze](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md)
