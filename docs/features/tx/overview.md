# Descripción general de TX Controls

El applet TX Controls es la interfaz principal para gestionar la potencia de transmisión, el ajuste de frecuencia y la adaptación de antena en el FLEX-8600. Proporciona medidores, controles deslizantes, selección de perfiles y controles de manipulación en un único panel.

## Cómo funciona

El applet TX Controls siempre está visible en el Panel de Applets (barra lateral derecha). Haga clic en el botón de bandeja TX para mostrarlo u ocultarlo. El applet requiere una conexión de radio activa para funcionar.

El applet está organizado en cinco áreas funcionales:

**Medidores de potencia** — Dos barras indicadoras horizontales en la parte superior del applet muestran lecturas de transmisión en tiempo real:

- **RF Pwr** — Potencia directa a la salida del excitador. La escala es de 0–120 W para configuraciones estándar, o de 0–600 W para los modelos Aurora 500W. La barra se vuelve roja por encima de 100 W (o por encima de 500 W en los modelos Aurora).
- **SWR** — Relación de onda estacionaria en el excitador, mostrada en una escala de 1.0–3.0. La barra se vuelve roja por encima de 2.5.

**Controles deslizantes de potencia** — Dos controles deslizantes establecen los niveles de potencia enviados al radio:

- **RF Power** — Establece el nivel de potencia de RF de transmisión. Rango: 0–100. Valor predeterminado: 100.
- **Tune Pwr** — Establece el nivel de potencia de la portadora de ajuste. Rango: 0–100. Valor predeterminado: 10.

Ambos controles deslizantes muestran su valor actual como número a la derecha del control.

**Perfil TX y estado del ATU** — Un menú desplegable y tres indicadores comparten una única fila:

- **TX Profile** — Selecciona el perfil de transmisión activo. La lista se obtiene de los perfiles almacenados en el radio. Al seleccionar un perfil, este se carga de inmediato.
- **Success** — Se ilumina en verde cuando el ATU informa una adaptación exitosa.
- **Byp** — Se ilumina en naranja cuando el ATU está en modo de derivación (bypass) o derivación manual.
- **Mem** — Se ilumina en verde cuando el ATU utiliza una memoria almacenada.

**Botones de acción** — Cuatro botones controlan la transmisión y el ajuste de antena:

- **TUNE** — Inicia una portadora de ajuste. La etiqueta del botón cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic de nuevo para detenerlo.
- **MOX** — Activa o desactiva la transmisión manual. El botón se vuelve rojo mientras el transmisor está manipulado.
- **ATU** — Inicia el ciclo de ajuste del ATU interno. Está deshabilitado cuando el transverter TGXL se encuentra en modo OPERATE.
- **MEM** — Activa o desactiva la recuperación de memoria del ATU. Está deshabilitado cuando el transverter TGXL se encuentra en modo OPERATE.

**Indicadores de APD y estado** — La fila inferior controla la Predistorsión Adaptativa (APD):

- **APD** — Activa o desactiva la predistorsión adaptativa en el radio.
- **Active** — Se ilumina en verde cuando el APD está activado y el ecualizador está aplicado de forma activa.
- **Cal** — Se ilumina en verde cuando el APD está activado y aún se está calibrando.
- **Avail** — Se ilumina en verde cuando el APD está activado y hay una calibración disponible pero aún no aplicada.

El estado del APD avanza por los indicadores en secuencia: Cal (calibrando) → Avail (calibración lista) → Active (ecualizador aplicado).

## Consejos

- Mantenga **Tune Pwr** bajo (el valor predeterminado de 10 es un punto de partida razonable) para evitar someter el amplificador o la antena a esfuerzo innecesario durante los ciclos del ATU.
- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de radio que detecte AetherSDR; no se requiere ajuste manual.
- **ATU** y **MEM** aparecen deshabilitados cuando el TGXL está en modo OPERATE. Saque el TGXL del modo OPERATE antes de intentar operaciones con el ATU.

## Relacionados

- [Establecer la potencia de salida de RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de ajuste](set-tune-carrier-power.md)
- [Cambiar perfiles TX (por ejemplo, SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de ajuste para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para manipular el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Activar el APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
