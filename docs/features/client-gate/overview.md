# Visión general de Aetherial TX Gate / Aetherial AGC-T (RX)

AetherSDR incluye un expansor descendente y una puerta de ruido del lado del cliente que funcionan de forma independiente tanto en la ruta de audio de transmisión como en la de recepción. Se utiliza para suprimir el ruido de fondo entre palabras en TX o para reducir el ruido de banda por debajo de un umbral seleccionado en RX.

## Antes de empezar

- La etapa Gate debe habilitarse a través del widget CHAIN o del editor flotante en el lado correspondiente antes de que el applet se vuelva visible.
- AetherSDR no necesita estar conectado a una radio para que los controles de la puerta se puedan ajustar, pero el audio debe estar en ejecución para que los indicadores en vivo sean significativos.

## Cómo funciona

AetherSDR crea dos copias totalmente independientes del applet de puerta:

- **Aetherial TX Gate** — actúa sobre el audio de transmisión saliente. Se encuentra en el contenedor principal Aetherial Audio (TXDSP).
- **Aetherial AGC-T** — actúa sobre el audio de recepción entrante. Se encuentra en el mismo contenedor principal como un subcontenedor separado.

Ambas copias comparten controles e indicadores idénticos. La configuración de cada lado se almacena de forma independiente. Los cambios realizados en el mosaico del applet acoplado y los cambios realizados en el editor flotante se mantienen sincronizados; el applet consulta el motor aproximadamente cada 33 ms y actualiza las posiciones de los mandos y la barra de reducción de ganancia para reflejar el lado que está activo.

### Flujo de señal

La puerta es un **expansor descendente**. Cuando el nivel de entrada cae por debajo del punto Thresh, la puerta atenúa la señal. La cantidad de atenuación depende de Ratio, y el corte más profundo permitido lo establece Floor. Return establece una banda muerta de histéresis: la puerta se abre cuando la señal supera Thresh y no se cierra de nuevo hasta que la señal cae por debajo de Thresh − Return. Release controla la rapidez con la que se cierra la puerta una vez que la señal cae por debajo de ese límite inferior.

Establecer Ratio en un valor bajo (cerca de 1.0:1) produce un efecto suave de expansor suave que reduce gradualmente el nivel. Establecer Ratio en un valor alto (cerca de 10.0:1) produce una puerta dura que corta agresivamente.

### Atenuación por bypass

Cuando la etapa de puerta está en bypass, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa no está procesando audio. El mosaico vuelve a la opacidad total tan pronto como se vuelve a habilitar la etapa.

### Abrir el applet

Haga doble clic en la etapa GATE en el widget CHAIN en el lado TX o RX para abrir el editor sin marco correspondiente, titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**. Se puede hacer clic derecho en las barras de título del subcontenedor acoplado para **Aetherial TX Gate** y **Aetherial AGC-T** para flotar, sacar u ocultar el mosaico.

## Qué hace cada control

Los controles que se enumeran a continuación aparecen de forma idéntica tanto en los applets de TX como de RX. Las claves de configuración que se muestran se aplican al lado TX; el lado RX utiliza las claves equivalentes `ClientGateRx*`.

| Control                | Tipo                                                                                                                                                                                                                                                                 | Valor predeterminado                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Curva de transferencia | Indicador                                                                                                                                                                                                                                                            | —                                                                                                                                                                                                                                                                   |
| Barra de reducción de ganancia | Medidor                                                                                                                                                                                                                                                          | —                                                                                                                                                                                                                                                                   |
| Thresh                 | Mando                                                                                                                                                                                                                                                                | −40,0 dB                                                                                                                                                                                                                                                            |
| Ratio                  | Mando                                                                                                                                                                                                                                                                | 2,0:1                                                                                                                                                                                                                                                               |
| Return                 | Mando                                                                                                                                                                                                                                                                | 2,0 dB                                                                                                                                                                                                                                                              |
| Release                | Mando                                                                                                                                                                                                                                                                | 100 ms                                                                                                                                                                                                                                                              |
| Floor                  | Mando                                                                                                                                                                                                                                                                | −15,0 dB                                                                                                                                                                                                                                                            |
| Flip (Expander / Gate) | Sin marcar = expansor descendente (suave, basado en ratio). Marcado = Gate (corte duro). Ajusta ratio y floor a pares predefinidos al alternar; los otros mandos permanecen en su lugar. La etiqueta se actualiza en vivo entre 'Expander' y 'Gate'. | Control solo de editor (ClientGateEditor flotante). Color: sin marcar = verde (Expander), marcado = ámbar (Gate). Información sobre herramientas: 'Cambie entre los modos Expander descendente (suave) y Gate (duro). Ajusta ratio + floor a pares predefinidos; los otros mandos permanecen donde los dejó.' |
| Peek (lookahead)       | Establece un retardo de prelectura para que la puerta pueda abrirse fraccionalmente antes de que llegue un transitorio, evitando bordes de ataque recortados. 'Off' desactiva la línea de retardo por completo.                                                  | Control solo de editor. Los valores más altos aumentan la latencia en la ruta TX. 1 y 1,5 ms coinciden con las opciones predefinidas de Ableton; se agregaron 3 y 5 ms para transitorios muy rápidos.                                                                 |
| Attack                 | Mapeo exponencial (0,1 * 1000^n). Establece la rapidez con la que se abre la puerta después de que la entrada supere Thresh.                                                                                                         | Control solo de editor. Etiqueta 'X.XX ms' por debajo de 10 ms, 'X.X ms' por encima.                                                                                                                                                                                   |
| Hold                   | Mapeo lineal (n * 500). Después de que la entrada caiga por debajo de Thresh − Return, la puerta permanece abierta durante este tiempo antes de comenzar a cerrarse, evitando el aleteo en material rítmico.                                  | Control solo de editor. Etiqueta 'X.X ms'.                                                                                                                                                                                                                                |

El estado de habilitación/bypass de cada lado se conserva bajo `ClientGateTxEnabled` (TX) y `ClientGateRxEnabled` (RX).

## Edición de valor en línea

Los mandos en el mosaico del applet admiten la entrada numérica directa. Haga clic en el texto del valor debajo de un mando para activar un editor en línea que se ve idéntico a la etiqueta de valor pintada. Escriba un número y presione Enter o haga clic en otro lugar para confirmar el valor. El valor se ajusta al rango válido del mando. Presione Escape para cancelar la edición y volver al valor anterior.

El editor en línea está disponible en todos los controles de mando tanto en los mosaicos del applet TX como RX.

## Indicadores visuales

| Indicador | Estados | Significado |
|---|---|---|
| Bola de entrada | Por debajo del umbral / por encima del umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | Ausente (Return = 0) / banda vertical cian suave | Visualiza la banda muerta de Return en el eje de entrada de la curva de transferencia: la zona de adherencia de la puerta entre (Thresh − Return) y Thresh. |
| Barra de reducción de ganancia | Vacía / relleno ámbar / marca de −15 dB | Profundidad de atenuación mientras la puerta está cerrada. La escala máxima es de 40 dB; una marca en −15 dB señala el valor predeterminado de floor del expansor suave. |
| Opacidad del mosaico del applet | Opacidad completa (habilitado) / aproximadamente 55 % de opacidad (en bypass) | Indica de un vistazo si la etapa de puerta está procesando audio actualmente. |

## Consejos

- Observe la barra de reducción de ganancia mientras no habla (TX) o durante un momento de solo ruido de banda (RX). Si la barra no se llena, Thresh está configurado por debajo del piso de ruido y la puerta no se está disparando. Consulte [Ver GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md).
- La marca de −15 dB en la barra de reducción de ganancia señala el valor predeterminado de Floor. Si la barra se llena completamente más allá de esa marca, Floor está configurado más profundo que −15 dB o Ratio es lo suficientemente alto como para llevar la reducción más allá de ese punto.
- Use la banda de histéresis cian en la curva de transferencia para juzgar si el valor de Return es lo suficientemente amplio para evitar el castañeteo sin hacer que la puerta sea lenta para cerrarse.
- Cuando el mosaico aparece atenuado, la etapa de puerta está en bypass. Vuelva a habilitarla a través del widget CHAIN o del editor flotante antes de esperar cualquier atenuación.
- Los cambios en cualquier mando surten efecto de inmediato y se guardan automáticamente. No se necesita ningún botón Apply.
- Para ingresar un valor numérico preciso, haga clic en el texto del valor debajo de cualquier mando y escriba el número directamente.

## Solución de problemas

- **El applet no es visible** — La etapa Gate no se ha habilitado en ese lado. Habilítela a través del widget CHAIN o del editor flotante para el lado TX o RX.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está en bypass. El mosaico se renderiza con opacidad reducida cuando el bypass está activo. Habilite la etapa a través del widget CHAIN o del editor flotante para restaurar el procesamiento completo y el brillo completo del mosaico.
- **La puerta no atenúa el ruido entre palabras** — Thresh puede estar configurado demasiado bajo, por debajo del piso de ruido ambiente. Aumente Thresh hasta que la barra de reducción de ganancia muestre movimiento durante el silencio. Consulte [Establecer el umbral de TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md).
- **La puerta castañea rápidamente cerca del umbral** — Return está configurado demasiado bajo. Aumente Return para que la puerta no se vuelva a abrir hasta que la señal esté claramente por encima de Thresh, ensanchando la banda muerta que muestra la banda cian en la curva de transferencia.
- **Silencio antinatural entre palabras** — Floor está configurado demasiado profundo. Aumente Floor hacia 0 dB para que pase algo de audio residual durante los períodos de cierre. Consulte [Establecer Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **Las posiciones de los mandos en el mosaico no coinciden con el editor flotante** — El mosaico se sincroniza cada ~33 ms. Si parecen no coincidir inmediatamente después de abrir el editor, espere un ciclo de actualización o mueva un mando para forzar una sincronización.
- **Recorte o vibración de la etiqueta del eje en la curva de transferencia** — Este problema se ha resuelto en v26.5.1. La curva ahora utiliza texto estático en caché para las etiquetas de los ejes, lo que mejora el rendimiento de renderizado y evita el movimiento de las etiquetas durante las transiciones de modo compacto.

## Relacionados

- [Establecer el umbral de TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Usar AGC-T en RX para suprimir el ruido de banda por debajo de un umbral seleccionado](use-agc-t-on-rx-to-suppress-band-noise-below-a-chosen-floor.md)
- [Elegir el comportamiento de puerta vs. expansor suave mediante ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Establecer Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ver GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
- [Poner en bypass la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
