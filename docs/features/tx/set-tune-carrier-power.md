# Controles de TX

El applet de Controles de TX proporciona todos los controles manuales de transmisión en AetherSDR, incluyendo la medición de potencia directa y ROE (con retención de pico PEP), deslizadores de potencia RF/Sintonía, selección de perfil TX, botones TUNE/MOX/ATU/MEM e indicadores de estado APD (Pre-Distorsión Adaptativa). En v0.9.7+, el botón MOX pasa a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar PTT cuando Quindar está habilitado (solo modos de telefonía).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX no está disponible sin una conexión activa a la radio.
- Abra el applet Controles de TX: haga clic en el botón de la bandeja TX en la barra lateral derecha si el applet aún no está visible.

## Ajustar la potencia de salida RF

El deslizador "RF Power" establece la potencia directa máxima que el transmisor producirá durante la operación normal.

### Pasos

1. Localice el deslizador "RF Power:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia. El valor numérico a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía a la radio.

### Escala del medidor

Los medidores de potencia RF y ROE muestran lecturas en tiempo real. Una barra de retención de pico PEP marca la potencia máxima de la envolvente y decae después de una ventana de retención de 2 segundos. El pico se reinicia a cero cuando el transmisor desactiva la transmisión.

| Medidor | Escala                          | Umbral rojo |
|---------|---------------------------------|-------------|
| Potencia RF | 0–120 W (sin amplificador), 0–600 W (Aurora 500W) | > 100 W / > 500 W |
| ROE     | 1.0–3.0                         | > 2.5       |

## Ajustar la potencia de la portadora de sintonía

El deslizador "Tune Pwr" establece el nivel de potencia de la portadora continua transmitida cuando presiona TUNE. Mantener este valor bajo protege sus etapas finales y el sistema de antena durante la sintonización del ATU o las comprobaciones de ROE.

### Pasos

1. Localice el deslizador "Tune Pwr:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonía. El valor numérico a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía a la radio.

### Visualización del valor al arrastrar

Al arrastrar cualquiera de los deslizadores de Potencia RF o Potencia de Sintonía, una información sobre herramientas muestra el valor actual en porcentaje del máximo (por ejemplo, "45%") mientras mueve el deslizador. Esto le ayuda a establecer niveles de potencia precisos sin soltar el ratón.

## Selección de perfil TX

1. Localice el cuadro combinado "TX Profile:" en el applet Controles de TX.
2. Haga clic en el cuadro combinado para revelar la lista de perfiles TX disponibles de la radio.
3. Seleccione un perfil. La radio lo carga inmediatamente.

## Botón TUNE

1. Haga clic en TUNE para iniciar una portadora de sintonía continua al nivel establecido por "Tune Pwr".
   - El texto del botón cambia a "TUNING..." y el fondo se vuelve rojo.
2. Haga clic en TUNE nuevamente o haga clic en el botón TUNE para detener la portadora.

**Menú contextual con clic derecho (v26.5.2.1)**:
- Haga clic derecho en el botón TUNE para abrir un menú contextual para seleccionar la forma de la portadora del próximo ciclo de sintonía.
- Elija **Mono Tone** o **Two Tone**. La selección es de un solo uso: el modo de sintonía de la radio vuelve a single_tone al reiniciar, y AetherSDR no conserva la elección en AppSettings.

## Botón MOX

1. Haga clic en MOX para activar manualmente el transmisor.
   - El botón se vuelve rojo mientras el transmisor está activado.
2. Haga clic en MOX nuevamente para desactivar la transmisión.
   - El botón vuelve a azul.

**Comportamiento del tono Quindar (v0.9.7+)**:
- Al **activar**: si Quindar está habilitado en la tira del canal de audio y el slice TX activo está en un modo de telefonía, el tono K se reproduce antes de activar el transmisor.
- Al **desactivar**: el tono BK se reproduce después de que el transmisor desactive la transmisión.
- Si Quindar está deshabilitado, o el slice TX activo no está en un modo de telefonía, el comportamiento es inmediato: el transmisor se activa y desactiva sin tonos.

## Botón ATU

El botón ATU inicia un ciclo de sintonización del ATU interno. A partir de v0.9.5.1, el botón ATU alterna entre iniciar un ciclo de sintonía y puentear el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

### Menú contextual con clic derecho (v26.5.2.1)

Haga clic derecho en el botón ATU para exponer acciones adicionales del sintonizador:

| Elemento del menú | Acción |
|---|---|
| **Pre-tune bands…** | Abre el diálogo de Pre-sintonización de bandas para barrer las memorias del sintonizador en todas las bandas. Habilitado solo cuando MEM está activado. |
| **Clear ATU memories…** | Confirma y borra todas las memorias almacenadas del ATU. |

### Comportamiento del ciclo de sintonía

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y de su frecuencia de transmisión:

| Situación | Qué hace al hacer clic en ATU |
|---|---|
| No existe una sintonización exitosa para la frecuencia actual | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU reporta una coincidencia exitosa y la frecuencia de transmisión no ha cambiado desde esa sintonización | Cambia el ATU a modo bypass. |
| El ATU reporta una coincidencia exitosa pero la frecuencia de transmisión ha cambiado desde esa sintonización | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU ya está en modo bypass | Inicia un nuevo ciclo de sintonía del ATU. |

En la práctica, esto significa:

1. Haga clic en ATU en una nueva frecuencia. La radio ejecuta un ciclo de sintonía. El indicador Success se enciende en verde cuando se encuentra una coincidencia.
2. Haga clic en ATU nuevamente sin cambiar la frecuencia. El sintonizador entra en modo bypass. El indicador Byp se enciende en naranja y el indicador Success se atenúa.
3. Cambie la frecuencia y haga clic en ATU. La radio ejecuta un nuevo ciclo de sintonía independientemente del resultado anterior.

Los botones ATU y MEM están deshabilitados cuando TGXL está en modo OPERATE.

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

## APD (Pre-Distorsión Adaptativa)

1. Haga clic en **APD** para activar o desactivar la pre-distorsión adaptativa en la radio.
2. Observe los tres indicadores de estado:

| Indicador | Color | Significado |
|---|---|---|
| **Active** | Verde | APD está activado y el ecualizador se aplica activamente |
| **Cal** | Verde | APD está activado y aún está calibrando |
| **Avail** | Verde | APD está activado y hay una calibración disponible pero aún no aplicada |

La progresión típica es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

## Descripción de cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| RF Power | Establece el nivel máximo de potencia RF de transmisión (porcentaje del máximo). | 100 |
| Tune Pwr | Establece el nivel de potencia de la portadora de sintonía (porcentaje del máximo). | 10 |
| TX Profile | Selecciona un perfil TX de la radio. | — |
| TUNE | Inicia/detiene una portadora de sintonía. Haga clic derecho para seleccionar la forma de portadora Mono Tone / Two Tone. | — |
| MOX | Activa/desactiva la transmisión manual. | — |
| ATU | Inicia un ciclo de sintonización del ATU o alterna el modo bypass. Haga clic derecho para Pre-sintonización de bandas / Borrar memorias ATU. | — |
| MEM | Activa/desactiva la recuperación de memoria del ATU. | — |
| APD | Activa/desactiva la pre-distorsión adaptativa. | — |

## Consejos

- Ajuste "Tune Pwr" al nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores usan 10–20% del máximo para la sintonización del ATU.
- El ajuste "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Ajustar uno no afecta al otro.
- Puede establecer valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.
- La barra de retención de pico de potencia RF se reinicia a cero cuando el transmisor desactiva la transmisión, evitando que una lectura PEP retenida persista entre sobretiros.
- Los deslizadores de potencia ahora muestran valores como porcentajes de la potencia máxima de la radio. La potencia real en vatios depende del modelo de su radio y de cualquier amplificador externo.

## Relacionados

- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)
