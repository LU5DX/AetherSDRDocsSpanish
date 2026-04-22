# Ajustar Floor para evitar silencios antinaturales entre palabras

El control **Floor** limita la profundidad máxima de atenuación que puede aplicar la puerta de ruido. Sin un límite de Floor, la puerta puede cortar la señal hasta casi el silencio entre palabras, lo que suena antinatural. Ajustar Floor a un valor moderado — como el predeterminado de −15.0 dB — deja un nivel residual pequeño durante las pausas silenciosas para que el corte sea menos brusco.

## Antes de comenzar

- El applet GATE debe estar visible en el panel de applets. Permanece oculto hasta que la etapa Gate se habilite mediante el widget CHAIN o el editor flotante Gate. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md) para saber cómo habilitarla.
- No se requiere una conexión de radio para ajustar Floor; los cambios surten efecto de inmediato y se conservan entre reinicios.

## Pasos

1. Localice el subcontenedor GATE en el panel de applets.
2. Encuentre el control más a la derecha en la fila de cinco controles, etiquetado como **Floor**.
3. Gire el control **Floor** en sentido horario para subir el piso (menos atenuación máxima) o en sentido antihorario para bajarlo (más atenuación máxima).
4. Hable con normalidad y observe la barra de reducción de ganancia. El relleno ámbar no debe superar la marca de −15 dB durante las pausas normales entre palabras. Si lo supera, suba Floor hacia 0.0 dB hasta que el relleno se mantenga dentro de un rango cómodo.
5. Transmita una grabación de prueba corta y escúchela. Si las pausas entre palabras suenan abruptamente silenciosas, suba Floor. Si el ruido de fondo se cuela de forma notoria durante las pausas, baje Floor.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — |

**Floor** establece la atenuación máxima que la puerta tiene permitido aplicar. Un valor de −15.0 dB significa que la puerta puede reducir la señal como máximo 15 dB, dejando el audio a −15 dB respecto a su nivel abierto en lugar de cortarlo al silencio total. Un valor de −80.0 dB otorga a la puerta una profundidad de corte prácticamente ilimitada.

La **barra de reducción de ganancia** es una franja ámbar horizontal, rellena desde la derecha, que va de 0 a 40 dB. La marca en −15 dB corresponde al valor predeterminado de Floor y sirve como referencia visual de la profundidad de corte de la puerta.

## Consejos

- La marca de −15 dB en la barra de reducción de ganancia es una referencia integrada para el Floor predeterminado. Si el relleno ámbar supera sistemáticamente esa marca durante las pausas normales del habla, su Floor está configurado por debajo del valor predeterminado y puede producir un corte notablemente abrupto.
- Floor interactúa con Ratio. Un Ratio alto (puerta dura) combinado con un Floor muy bajo (por ejemplo, −80.0 dB) produce un efecto encendido/apagado agresivo. Si desea un sonido más suave, suba Floor hacia −10.0 dB o reduzca Ratio en lugar de ajustar ambos de forma independiente.
- El control Floor en el tile del applet GATE y el mismo control en el editor flotante Gate están sincronizados en tiempo real. Ajustar uno actualiza el otro de inmediato.

## Temas relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Elegir entre comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ver la reducción de ganancia en vivo sin estar hablando](watch-live-gr-while-not-speaking.md)
- [Ajustar ataque y release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
