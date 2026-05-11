# Puerta Aetherial TX / AGC-G Aetherial (RX)

El cliente de AetherSDR implementa un expansor descendente / puerta de ruido que se ejecuta completamente en el lado del cliente, sin necesidad de un viaje de ida y vuelta al equipo de radio. El AppletPanel crea dos copias independientes:

- **Puerta Aetherial TX** — procesa la cadena de audio de transmisión.
- **AGC-G Aetherial (RX)** — procesa la cadena de audio de recepción (AGC significa Control Automático de Ganancia – variante Puerta).

La puerta silencia el ruido de fondo entre palabras (TX) o por debajo de un piso de audio RX deseado, atenuando el audio por debajo de un umbral. La interfaz de usuario muestra la curva de transferencia estática con una bola de entrada en vivo, una superposición de banda de histéresis en cian entre (Umbral − Retorno) y Umbral, un medidor de reducción de ganancia de 40 dB y cinco perillas de ajuste: Umbral, Relación, Retorno, Liberación, Piso.

## Controles

| Etiqueta | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento | Notas |
|---|---|---|---|---|---|---|
| Curva de transferencia | indicador | — | — | — | ClientGateCurveWidget en modo compacto. Grafica la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. | |
| Barra de reducción de ganancia | medidor | — | 0 a 40 dB GR | — | Franja horizontal ámbar, relleno desde la derecha. La escala máxima es de 40 dB (las puertas pueden cortar muy profundo); una marca en -15 dB señala el piso predeterminado del expansor suave. | |
| Umbral | perilla | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` (lado TX)<br>`ClientGateRxThresholdDb` (lado RX) | Mapeo lineal. Nivel por debajo del cual la puerta comienza a atenuar. | |
| Relación | perilla | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` (lado TX)<br>`ClientGateRxRatio` (lado RX) | Mapeo lineal. Relaciones más altas producen un corte más fuerte, similar a una puerta; relaciones más bajas actúan como un expansor descendente suave. | Etiqueta 'X.X:1'. |
| Retorno | perilla | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` (lado TX)<br>`ClientGateRxReturnDb` (lado RX) | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la puerta se abre por encima del Umbral y no se cierra nuevamente hasta que la entrada cae por debajo de Umbral − Retorno, evitando el rápido chattering cerca del umbral. | Etiqueta 'X.XX dB'. El widget de curva dibuja una banda vertical en cian suave entre (Umbral − Retorno) y Umbral para hacer visible la zona pegajosa. |
| Liberación | perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` (lado TX)<br>`ClientGateRxReleaseMs` (lado RX) | Mapeo exponencial (5 * 400^n). Establece la rapidez con que la puerta se cierra después de que la entrada cae por debajo de Umbral − Retorno. | Etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima. |
| Piso | perilla | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` (lado TX)<br>`ClientGateRxFloorDb` (lado RX) | Mapeo lineal. Atenuación máxima que la puerta puede aplicar. | |

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Bola de entrada | por debajo del umbral, por encima del umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | ausente (Retorno = 0), banda vertical en cian suave | Visualiza la banda muerta de Retorno en el eje de entrada de la curva de transferencia — la zona pegajosa de la puerta entre (Umbral − Retorno) y Umbral. |
| Franja de reducción de ganancia | vacía, relleno ámbar, marca de -15 dB | Profundidad de atenuación mientras la puerta está cerrada. |

## Widget de Curva de Transferencia

El ClientGateCurveWidget muestra la curva de transferencia estática. En el modo compacto (utilizado dentro del Panel de Applets) usa un tamaño de fuente de 7 píxeles para las etiquetas de los ejes. En el modo de tamaño completo (editor flotante) usa una fuente de 9 píxeles y dibuja etiquetas de cuadrícula en -dB en las posiciones de las marcas principales. Las etiquetas se representan previamente como objetos `QStaticText` para mejorar el rendimiento del dibujo.

# Bypass de la Puerta desde la Cadena

El widget CHAIN controla si la etapa de Puerta está activa en la cadena de procesamiento de audio. Al ponerla en bypass, puede deshabilitar la puerta TX o RX por completo sin cambiar ninguna de sus perillas de ajuste, lo que le permite comparar el audio con y sin puerta o silenciar temporalmente la etapa.

## Antes de comenzar

- Abra el contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets. Los subcontenedores "Puerta Aetherial TX" (TX) y "AGC-G Aetherial (RX)" están ocultos hasta que la etapa de Puerta se habilite a través del widget CHAIN.
- Sepa qué lado desea poner en bypass — TX (afecta su audio transmitido) o RX (afecta el audio recibido).

## Pasos

1. Localice el widget CHAIN para el lado que desea cambiar — TX o RX — dentro del contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets.
2. Haga un solo clic en la etapa GATE en el widget CHAIN para alternar el bypass de la puerta en ese lado.
   - Cuando la etapa está habilitada, el subcontenedor "Puerta Aetherial TX" o "AGC-G Aetherial (RX)" se vuelve visible con opacidad completa y la puerta está activa en la cadena.
   - Cuando la etapa está en bypass, el subcontenedor se atenúa a una opacidad reducida (aproximadamente el 55 % del brillo completo) y no se aplica ninguna reducción de ganancia.
3. Para re-habilitar la etapa, haga un solo clic en la etapa GATE en el widget CHAIN nuevamente. El subcontenedor vuelve a la opacidad completa.

El estado de bypass se conserva como `ClientGateTxEnabled` (lado TX) o `ClientGateRxEnabled` (lado RX) y se restaura en el próximo inicio de la aplicación.

## Consejos

- El efecto de atenuación cuando está en bypass coincide con el tratamiento visual aplicado a la curva EQ cuando su etapa está en bypass, proporcionando una señal visual coherente en todas las etapas de DSP.
- Poner en bypass desde el widget CHAIN no restablece ninguna de las cinco perillas de ajuste: los valores de Umbral, Relación, Retorno, Liberación y Piso se conservan.
- Para abrir el editor de puerta flotante para un ajuste detallado sin poner en bypass, haga doble clic en la etapa GATE en el widget CHAIN en lugar de un solo clic.

## Relacionado

- [Visión general de Aetherial Audio (TXDSP)](overview.md)
- [Ajustar el umbral TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Observar la GR en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
