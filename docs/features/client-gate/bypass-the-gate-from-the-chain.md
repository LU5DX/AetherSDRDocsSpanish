# Puerta Aetherial TX / AGC-G Aetherial (RX)

El cliente AetherSDR implementa un expansor descendente / puerta de ruido que se ejecuta completamente del lado del cliente, sin ida y vuelta a la radio. El AppletPanel crea dos copias independientes:

- **Puerta Aetherial TX** — procesa la cadena de audio de transmisión.
- **AGC-G Aetherial (RX)** — procesa la cadena de audio de recepción (AGC significa Control Automático de Ganancia – variante Puerta).

La puerta silencia el ruido de fondo entre palabras (TX) o por debajo de un piso de audio RX deseado, atenuando el audio por debajo de un umbral. La interfaz de usuario muestra la curva de transferencia estática con una bola de entrada en vivo, una superposición de banda de histéresis en cian entre (Umbral − Retorno) y Umbral, un medidor de reducción de ganancia de 40 dB y cinco perillas de ajuste: Umbral, Relación, Retorno, Liberación, Piso.

Los colores de las perillas (anillo de fondo, arco frontal, puntero, etiqueta y valor numérico) siguen el tema definido en el espacio de nombres `color.knob.*`. El contenedor del applet se registra como `applet/gate` para la búsqueda de tema, lo que permite anulaciones de color por applet, como el color frontal ámbar específico del applet de puerta/expansor.

## Controles

| Etiqueta | Tipo | Predeterminado | Rango Válido | Clave de Configuración | Comportamiento | Notas |
|---|---|---|---|---|---|---|
| Curva de transferencia | indicador | — | — | — | ClientGateCurveWidget en modo compacto. Grafica la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. | |
| Barra de reducción de ganancia | medidor | — | 0 a 40 dB GR | — | Franja horizontal ámbar, rellena desde la derecha. Escala máxima en 40 dB (las puertas pueden cortar muy profundo); una marca en -15 dB señala el piso predeterminado del expansor suave. | |
| Umbral | perilla | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` (lado TX)<br>`ClientGateRxThresholdDb` (lado RX) | Mapeo lineal. Nivel por debajo del cual la puerta comienza a atenuar. | Edición en línea: haga clic en el valor, escriba un número nuevo, presione Enter o haga clic en otro lugar para confirmar. |
| Relación | perilla | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` (lado TX)<br>`ClientGateRxRatio` (lado RX) | Mapeo lineal. Relaciones más altas dan un corte más duro, similar a una puerta; relaciones más bajas actúan como un expansor descendente suave. | Etiqueta 'X.X:1'. Edición en línea: haga clic en el valor, escriba un número nuevo, presione Enter o haga clic en otro lugar para confirmar. |
| Retorno | perilla | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` (lado TX)<br>`ClientGateRxReturnDb` (lado RX) | Mapeo lineal (n * 20). Establece la banda muerta de histéresis: la puerta se abre por encima del Umbral y no se cierra hasta que la entrada cae por debajo de Umbral − Retorno, evitando el parloteo rápido cerca del umbral. | Etiqueta 'X.XX dB'. El widget de curva dibuja una banda vertical cian suave entre (Umbral − Retorno) y Umbral para hacer visible la zona pegajosa. Edición en línea: haga clic en el valor, escriba un número nuevo, presione Enter o haga clic en otro lugar para confirmar. |
| Liberación | perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` (lado TX)<br>`ClientGateRxReleaseMs` (lado RX) | Mapeo exponencial (5 * 400^n). Establece la velocidad a la que la puerta se cierra después de que la entrada cae por debajo de Umbral − Retorno. | Etiqueta 'X.X ms' por debajo de 100, 'X ms' por encima. Edición en línea: haga clic en el valor, escriba un número nuevo, presione Enter o haga clic en otro lugar para confirmar. |
| Piso | perilla | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` (lado TX)<br>`ClientGateRxFloorDb` (lado RX) | Mapeo lineal. Atenuación máxima que la puerta puede aplicar. | Edición en línea: haga clic en el valor, escriba un número nuevo, presione Enter o haga clic en otro lugar para confirmar. |

## Indicadores

| Etiqueta | Estados | Significado |
|---|---|---|
| Bola de entrada | por debajo del umbral, por encima del umbral | Muestra si la puerta está actualmente abierta o cerrada. |
| Banda de histéresis | ausente (Retorno = 0), banda vertical cian suave | Visualiza la banda muerta de Retorno en el eje de entrada de la curva de transferencia — la zona pegajosa de la puerta entre (Umbral − Retorno) y Umbral. |
| Franja de reducción de ganancia | vacía, relleno ámbar, marca de -15 dB | Profundidad de atenuación mientras la puerta está cerrada. |

## Widget de Curva de Transferencia

El ClientGateCurveWidget muestra la curva de transferencia estática. En modo compacto (usado dentro del Panel de Applets) utiliza una fuente más pequeña de 7 píxeles para las etiquetas de los ejes. En modo de tamaño completo (editor flotante) utiliza una fuente de 9 píxeles y dibuja etiquetas de cuadrícula en -dB en las posiciones de las marcas principales. Las etiquetas se pre-renderizan como objetos `QStaticText` para mejorar el rendimiento del dibujo.

El widget de curva lee los colores del tema activo. La curva usa la entrada de paleta `color.accent.warning` (ámbar), y todos los colores de fondo, cuadrícula y etiquetas de ejes provienen de los espacios de nombres de tema `color.background.*` y `color.text.*`.

El widget de curva de transferencia se redibuja en cada tick de su temporizador de suavizado para garantizar que la bola en vivo y el medidor de reducción de ganancia se actualicen suavemente sin parpadeo.

## Edición de Valor en Línea

Cada perilla admite la entrada numérica directa. Haga clic en el valor mostrado para abrir un editor en línea. El editor aparece como un pequeño campo de texto con un fondo oscuro sutil y un borde cian cuando está enfocado. Escriba el valor deseado (por ejemplo, "12.5 ms" o "-40.0 dB") y presione Enter para confirmar, o haga clic en otro lugar de la pantalla. El valor se ajusta automáticamente al rango válido de la perilla. Presione Escape para cancelar la edición y revertir al valor anterior.

Cuando una perilla está en modo de edición, los eventos de la rueda del ratón se reenvían a la perilla para que pueda ajustarla desplazándose si lo prefiere.

# Bypass de la Puerta desde la Cadena

El widget CHAIN controla si la etapa de Puerta está activa en la cadena de procesamiento de audio. Al hacer bypass, puede desactivar la puerta TX o RX por completo sin cambiar ninguna de sus perillas de ajuste, permitiendo comparar audio con y sin puerta o silenciar temporalmente la etapa.

## Antes de comenzar

- Abra el contenedor principal Audio Aetherial (TXDSP) en el Panel de Applets. Los subcontenedores "Puerta Aetherial TX" (TX) y "AGC-G Aetherial (RX)" (RX) están ocultos hasta que la etapa de Puerta se habilite a través del widget CHAIN.
- Sepa qué lado desea pasar por bypass — TX (afecta su audio transmitido) o RX (afecta el audio recibido).

## Pasos

1. Localice el widget CHAIN para el lado que desea cambiar — TX o RX — dentro del contenedor principal Audio Aetherial (TXDSP) en el Panel de Applets.
2. Haga un solo clic en la etapa GATE en el widget CHAIN para alternar el bypass de la puerta en ese lado.
   - Cuando la etapa está habilitada, el subcontenedor "Puerta Aetherial TX" o "AGC-G Aetherial (RX)" se vuelve visible con opacidad completa y la puerta está activa en la cadena.
   - Cuando la etapa está en bypass, el subcontenedor se atenúa a una opacidad reducida (aproximadamente el 55 % del brillo total) y no se aplica ninguna reducción de ganancia.
3. Para volver a habilitar la etapa, haga un solo clic en la etapa GATE en el widget CHAIN nuevamente. El subcontenedor vuelve a la opacidad completa.

El estado de bypass se persiste como `ClientGateTxEnabled` (lado TX) o `ClientGateRxEnabled` (lado RX) y se restaura en el próximo inicio de la aplicación.

## Consejos

- El efecto de atenuación cuando está en bypass coincide con el tratamiento visual aplicado a la curva EQ cuando su etapa está en bypass, proporcionando una señal visual consistente en todas las etapas DSP.
- Hacer bypass desde el widget CHAIN no restablece ninguna de las cinco perillas de ajuste — los valores de Umbral, Relación, Retorno, Liberación y Piso se conservan.
- Para abrir el editor de puerta flotante para un ajuste detallado sin hacer bypass, haga doble clic en la etapa GATE en el widget CHAIN en lugar de un solo clic.

## Relacionados

- [Descripción general de Audio Aetherial (TXDSP)](overview.md)
- [Establecer umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Observar GR en vivo mientras no habla](watch-live-gr-while-not-speaking.md)
