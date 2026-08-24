# Controles de TX

El applet Controles de TX proporciona todos los controles manuales de transmisión en AetherSDR, incluida la medición de potencia directa y ROE (con retención de pico PEP), controles deslizantes de potencia RF/Sintonía, selección de perfil TX, botones TUNE/MOX/ATU/MEM e indicadores de estado APD (predistorsión adaptativa). En la versión 0.9.7+, el botón MOX se enruta a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar PTT cuando Quindar está habilitado (solo modos de teléfono).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX no está disponible sin una conexión activa a la radio.
- Abra el applet Controles de TX: haga clic en el botón TX en la barra lateral derecha si el applet no está ya visible.

## Configurar la potencia de salida RF

El control deslizante "RF Power" establece la potencia directa máxima que el transmisor producirá durante la operación normal.

### Pasos

1. Ubique el control deslizante "RF Power:" en el applet Controles de TX.
2. Arrastre el control deslizante hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia. La lectura numérica a la derecha del control se actualiza inmediatamente.
3. Suelte el control deslizante. El nuevo valor se envía a la radio.

### Escala del medidor

El medidor RF Pwr y el medidor ROE muestran lecturas en tiempo real. Una barra de retención de pico PEP marca la potencia de envolvente máxima y decae después de una ventana de retención de 2 segundos. El pico se restablece a cero cuando el transmisor desactiva la transmisión.

| Medidor | Escala | Umbral rojo |
|---|---|---|
| RF Pwr | 0–120 W (sin amplificador), 0–600 W (Aurora 500W) | > 100 W / > 500 W |
| ROE | 1.0–3.0 | > 2.5 |

### Lectura al pasar el cursor

Pase el cursor del ratón sobre el medidor RF Pwr o ROE para ver el valor exacto. La lectura RF Pwr muestra la potencia precisa en vatios (p. ej., "45 W") y la lectura ROE muestra la relación en forma convencional (p. ej., "1.32:1"). Esto le ayuda a evitar estimar entre las marcas de escala durante la transmisión.

## Configurar la potencia de la portadora de sintonía

El control deslizante "Tune Pwr" establece el nivel de potencia de la portadora continua transmitida al pulsar TUNE. Mantener este valor bajo protege sus etapas finales y el sistema de antena durante la sintonización ATU o las comprobaciones de ROE.

### Pasos

1. Ubique el control deslizante "Tune Pwr:" en el applet Controles de TX.
2. Arrastre el control deslizante hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonía. La lectura numérica a la derecha del control se actualiza inmediatamente.
3. Suelte el control deslizante. El nuevo valor se envía a la radio.

### Visualización del valor al arrastrar

Al arrastrar el control deslizante RF Power o Tune Pwr, una información sobre herramientas muestra el valor actual como porcentaje del máximo (p. ej., "45%") mientras mueve el control. Esto le ayuda a establecer niveles de potencia precisos sin soltar el ratón.

## Selección de perfil TX

1. Ubique el cuadro combinado "TX Profile:" en el applet Controles de TX.
2. Haga clic en el cuadro combinado para mostrar la lista de perfiles TX disponibles de la radio.
3. Seleccione un perfil. La radio lo carga inmediatamente.

## Botón TUNE

1. Haga clic en TUNE para iniciar una portadora de sintonía continua al nivel establecido por "Tune Pwr".
   - El texto del botón cambia a "TUNING..." y el fondo se vuelve rojo.
2. Haga clic en TUNE nuevamente para detener la portadora.

**Menú contextual con clic derecho**:
- Haga clic derecho en el botón TUNE para abrir un menú contextual y seleccionar la forma de la portadora del próximo ciclo de sintonía.
- Elija **Mono Tone** o **Two Tone**. La selección es de un solo uso: el modo de sintonía de la radio vuelve a single_tone al reiniciar, y AetherSDR no conserva la elección.

## Botón MOX

1. Haga clic en MOX para activar manualmente el transmisor.
   - El botón se vuelve rojo mientras el transmisor está activado.
2. Haga clic en MOX nuevamente para desactivar.
   - El botón vuelve a su estado de reposo con un borde y texto de acento ámbar, distinguiéndolo de los botones TUNE, ATU y MEM.

**Comportamiento del tono Quindar**:
- Al **activar**: si Quindar está habilitado en la tira de canal de audio y la rebanada TX activa está en un modo de teléfono, el tono K se reproduce antes de activar el transmisor.
- Al **desactivar**: el tono BK se reproduce después de que el transmisor desactiva la transmisión.
- Si Quindar está deshabilitado, o la rebanada TX activa no está en un modo de teléfono, el comportamiento es inmediato: el transmisor activa y desactiva la transmisión sin tonos.

## Botón ATU

El botón ATU inicia un ciclo de sintonización ATU interno. El botón ATU alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR. El botón ATU y el botón MEM están deshabilitados cuando la radio no tiene sintonizador de antena instalado (por ejemplo, una Hermes-Lite 2), o cuando un TGXL está en modo OPERATE.

### Menú contextual con clic derecho

Haga clic derecho en el botón ATU para acceder a acciones adicionales del sintonizador:

| Elemento del menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo Pre-Tune Bands para barrer las memorias del sintonizador a través de las bandas. Solo habilitado cuando MEM está activado. |
| **Clear ATU memories…** | Confirma y borra todas las memorias ATU almacenadas. |

### Comportamiento del ciclo de sintonía

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y de su frecuencia de transmisión:

| Situación | Qué hace el clic en ATU |
|---|---|
| No existe una sintonía exitosa para la frecuencia actual | Inicia un ciclo de sintonía ATU nuevo. |
| ATU informa una coincidencia exitosa y la frecuencia de transmisión no ha cambiado desde esa sintonía | Cambia el ATU a bypass. |
| ATU informa una coincidencia exitosa pero la frecuencia de transmisión ha cambiado desde esa sintonía | Inicia un ciclo de sintonía ATU nuevo. |
| ATU ya está en bypass | Inicia un ciclo de sintonía ATU nuevo. |

En la práctica esto significa:

1. Haga clic en ATU en una frecuencia nueva. La radio ejecuta un ciclo de sintonía. El indicador Success se enciende en verde cuando se encuentra una coincidencia.
2. Haga clic en ATU nuevamente sin cambiar de frecuencia. El sintonizador entra en bypass. El indicador Byp se enciende en naranja y el indicador Success se atenúa.
3. Cambie de frecuencia y haga clic en ATU. La radio ejecuta un ciclo de sintonía nuevo independientemente del resultado anterior.

El botón ATU y el botón MEM están ambos deshabilitados cuando la radio no tiene sintonizador, o cuando TGXL está en modo OPERATE. Pase el cursor sobre un botón deshabilitado para ver el motivo aplicable: "This radio has no antenna tuner" tiene prioridad sobre "Disabled — TGXL is in OPERATE mode".

## Botón MEM

1. Haga clic en MEM para activar o desactivar la recuperación de memoria ATU.
   - Cuando está activado, el indicador Mem se enciende en verde.
2. Haga clic en MEM nuevamente para deshabilitar la recuperación de memoria.

El botón MEM está deshabilitado cuando la radio no tiene sintonizador, o cuando TGXL está en modo OPERATE.

## Indicadores de estado ATU

Tres indicadores muestran el estado actual del ATU:

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado ATU es Successful u OK |
| **Byp** | Naranja | ATU está en Bypass o ManualBypass |
| **Mem** | Verde | ATU está usando una memoria |

## APD (Predistorsión adaptativa)

1. Haga clic en **APD** para alternar la predistorsión adaptativa en la radio.
2. Observe los tres indicadores de estado:

| Indicador | Color | Significado |
|---|---|---|
| **Active** | Verde | APD está activado y el ecualizador se aplica activamente |
| **Cal** | Verde | APD está activado y aún está calibrando |
| **Avail** | Verde | APD está activado y hay una calibración disponible pero aún no aplicada |

La progresión típica es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| RF Power | Establece el nivel máximo de potencia RF de transmisión (porcentaje del máximo). | 100 |
| Tune Pwr | Establece el nivel de potencia de la portadora de sintonía (porcentaje del máximo). | 10 |
| TX Profile | Selecciona un perfil TX de la radio. | — |
| TUNE | Inicia/detiene una portadora de sintonía. Clic derecho para forma de portadora Mono Tone / Two Tone. | — |
| MOX | Alterna la transmisión manual. El estado de reposo muestra un borde de acento ámbar. | — |
| ATU | Inicia un ciclo de sintonía ATU o alterna bypass. Clic derecho para Pre-tune bands / Clear ATU memories. | — |
| MEM | Alterna la recuperación de memoria ATU. | — |
| APD | Alterna la predistorsión adaptativa. | — |

## Comportamiento de medición

Los medidores RF Pwr y ROE muestran lecturas en vivo solo mientras el transmisor está activado. Al desactivar la transmisión, ambos medidores vuelven inmediatamente a sus posiciones de reposo (0 W y 1.0 ROE), y la barra de retención de pico PEP cae a cero instantáneamente. Esto evita que lecturas obsoletas persistan entre transmisiones y descarta cualquier respuesta del medidor que ya estuviera en tránsito cuando se produjo el flanco.

Cuando faltan datos de ROE durante una transmisión (por ejemplo, antes de que la radio informe una relación), el medidor ROE se mantiene en 1.0 en lugar de mostrar una lectura de 0.0 fuera de escala.

## Consejos

- Establezca "Tune Pwr" al nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores usan 10–20% del máximo para la sintonización ATU.
- El ajuste "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Ajustar uno no afecta al otro.
- Puede establecer valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.
- La barra de retención de pico RF Pwr se restablece a cero cuando el transmisor desactiva la transmisión, evitando que una lectura PEP retenida persista entre transmisiones.
- Los controles deslizantes de potencia ahora muestran valores como porcentajes de la potencia máxima de la radio. La potencia real en vatios depende del modelo de su radio y de cualquier amplificador externo.
- Pase el cursor sobre los medidores RF Pwr o ROE para ver lecturas precisas — vataje exacto o relación ROE — en lugar de estimar entre las marcas de escala.

## Relacionados

- [Iniciar una portadora de sintonía para comprobar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Configurar la potencia de salida RF](set-rf-output-power.md)
