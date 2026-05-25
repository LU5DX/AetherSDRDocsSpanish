# Controles de TX

El applet Controles de TX proporciona todos los controles manuales de transmisión en AetherSDR, incluyendo la medición de potencia directa y ROE (con retención de pico PEP), deslizadores de potencia RF/Tune, selección de perfil TX, botones TUNE/MOX/ATU/MEM e indicadores de estado APD (Predistorsión Adaptativa). En la versión v0.9.7+, el botón MOX se enruta a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar el PTT cuando Quindar está habilitado (solo modos de fonía).

## Antes de empezar

- AetherSDR debe estar conectado al equipo. El applet TX no está disponible sin una conexión activa al equipo.
- Abra el applet Controles de TX: haga clic en el botón TX de la bandeja en la barra lateral derecha si el applet no está visible.

## Ajustar la potencia de salida RF

El deslizador "RF Power" establece la potencia directa máxima que el transmisor producirá durante la operación normal.

### Pasos

1. Localice el deslizador "RF Power:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia. La lectura numérica a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía al equipo.

### Escala del medidor

El medidor RF Pwr y el medidor SWR muestran lecturas en tiempo real. Una barra de retención de pico PEP marca la potencia de pico de envolvente y decrece tras una ventana de retención de 2 segundos. El pico se reinicia a cero cuando el transmisor desactiva la transmisión.

| Medidor | Escala                          | Umbral rojo |
|---------|--------------------------------|--------------|
| RF Pwr  | 0–120 W (sin amplificador), 0–600 W (Aurora 500W) | > 100 W / > 500 W |
| SWR     | 1.0–3.0                        | > 2.5        |

## Ajustar la potencia de la portadora de sintonía

El deslizador "Tune Pwr" establece el nivel de potencia de la portadora continua transmitida al presionar TUNE. Mantenerlo bajo protege sus etapas finales y el sistema de antena durante la sintonización del ATU o las comprobaciones de ROE.

### Pasos

1. Localice el deslizador "Tune Pwr:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonía. La lectura numérica a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía al equipo.

### Visualización del valor al arrastrar

Al arrastrar cualquiera de los deslizadores RF Power o Tune Pwr, una información sobre herramientas muestra el valor actual en vatios (por ejemplo, "45 W") mientras mueve el deslizador. Esto ayuda a establecer niveles de potencia precisos sin soltar el ratón.

## Selección de perfil TX

1. Localice el cuadro combinado "TX Profile:" en el applet Controles de TX.
2. Haga clic en el cuadro combinado para ver la lista de perfiles TX disponibles en el equipo.
3. Seleccione un perfil. El equipo lo carga inmediatamente.

## Botón TUNE

1. Haga clic en TUNE para iniciar una portadora de sintonía continua al nivel establecido por "Tune Pwr".
   - El texto del botón cambia a "TUNING..." y el fondo se vuelve rojo.
2. Haga clic en TUNE nuevamente o haga clic en el botón TUNE para detener la portadora.

**Menú contextual con clic derecho (v26.5.2.1)**:
- Haga clic derecho en el botón TUNE para abrir un menú contextual y seleccionar la forma de la portadora del siguiente ciclo de sintonía.
- Elija **Mono Tone** o **Two Tone**. La selección es de un solo uso: el modo de sintonía del equipo vuelve a single_tone tras los ciclos de alimentación, y AetherSDR no guarda la elección en AppSettings.

## Botón MOX

1. Haga clic en MOX para activar manualmente el transmisor.
   - El botón se vuelve rojo mientras el transmisor está activado.
2. Haga clic en MOX nuevamente para desactivar.
   - El botón vuelve a azul.

**Comportamiento del tono Quindar (v0.9.7+)**:
- Al **activar**: si Quindar está habilitado en la tira del canal de audio y la losa TX activa está en un modo de fonía, el tono K se reproduce antes de que el transmisor se active.
- Al **desactivar**: el tono BK se reproduce después de que el transmisor se desactive.
- Si Quindar está deshabilitado, o la losa TX activa no está en un modo de fonía, el comportamiento es inmediato: el transmisor se activa y desactiva sin tonos.

## Botón ATU

El botón ATU inicia un ciclo de sintonía del ATU interno. A partir de la versión v0.9.5.1, el botón ATU alterna entre iniciar un ciclo de sintonía y puentear el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

### Menú contextual con clic derecho (v26.5.2.1)

Haga clic derecho en el botón ATU para acceder a acciones adicionales del sintonizador:

| Elemento del menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo Pre-Tune Bands para barrer las memorias del sintonizador a través de las bandas. Solo habilitado cuando MEM está activado. |
| **Clear ATU memories…** | Confirma y borra todas las memorias del ATU almacenadas. |

### Comportamiento del ciclo de sintonía

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y de su frecuencia de transmisión:

| Situación | Lo que hace al hacer clic en ATU |
|---|---|
| No existe una sintonía exitosa para la frecuencia actual | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU reporta una coincidencia exitosa y la frecuencia de transmisión no ha cambiado desde esa sintonía | Cambia el ATU a modo de puenteo. |
| El ATU reporta una coincidencia exitosa pero la frecuencia de transmisión ha cambiado desde esa sintonía | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU ya está en modo de puenteo | Inicia un nuevo ciclo de sintonía del ATU. |

En la práctica, esto significa:

1. Haga clic en ATU en una nueva frecuencia. El equipo ejecuta un ciclo de sintonía. El indicador Success se enciende en verde cuando se encuentra una coincidencia.
2. Haga clic en ATU nuevamente sin cambiar la frecuencia. El sintonizador entra en modo de puenteo. El indicador Byp se enciende en naranja y el indicador Success se apaga.
3. Cambie de frecuencia y haga clic en ATU. El equipo ejecuta un nuevo ciclo de sintonía independientemente del resultado anterior.

El botón ATU y el botón MEM están deshabilitados cuando TGXL está en modo OPERATE.

## Botón MEM

1. Haga clic en MEM para activar o desactivar la recuperación de memoria del ATU.
   - Cuando está activado, el indicador Mem se enciende en verde.
2. Haga clic en MEM nuevamente para deshabilitar la recuperación de memoria.

El botón MEM está deshabilitado cuando TGXL está en modo OPERATE.

## Indicadores de estado del ATU

Tres indicadores muestran el estado actual del ATU:

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado del ATU es Successful o OK |
| **Byp** | Naranja | El ATU está en Bypass o ManualBypass |
| **Mem** | Verde | El ATU está usando una memoria |

## APD (Predistorsión Adaptativa)

1. Haga clic en **APD** para activar o desactivar la predistorsión adaptativa en el equipo.
2. Observe los tres indicadores de estado:

| Indicador | Color | Significado |
|---|---|---|
| **Active** | Verde | APD está activado y el ecualizador se aplica activamente |
| **Cal** | Verde | APD está activado y aún está calibrando |
| **Avail** | Verde | APD está activado y hay una calibración disponible pero aún no aplicada |

La progresión típica es: **Cal** (calibrando) → **Avail** (lista) → **Active** (aplicada).

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| RF Power | Establece el nivel máximo de potencia de transmisión RF (W). | 100 |
| Tune Pwr | Establece el nivel de potencia de la portadora de sintonía (W). | 10 |
| TX Profile | Selecciona un perfil TX del equipo. | — |
| TUNE | Inicia/detiene una portadora de sintonía. Clic derecho para forma de portadora Mono Tone / Two Tone. | — |
| MOX | Activa/desactiva la transmisión manual. | — |
| ATU | Inicia un ciclo de sintonía del ATU o alterna el puenteo. Clic derecho para Pre-tune bands / Clear ATU memories. | — |
| MEM | Activa/desactiva la recuperación de memoria del ATU. | — |
| APD | Activa/desactiva la predistorsión adaptativa. | — |

## Consejos

- Establezca "Tune Pwr" al nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores usan 10–20 W para la sintonización del ATU.
- La configuración de "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Ajustar uno no afecta al otro.
- Puede establecer valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.
- La barra de retención de pico RF Pwr se reinicia a cero cuando el transmisor desactiva la transmisión, evitando que una lectura PEP retenida persista entre sobretransmisiones.

## Relacionados

- [Iniciar una portadora de sintonía para comprobar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
