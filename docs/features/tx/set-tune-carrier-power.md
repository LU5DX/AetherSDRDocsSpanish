# Controles de TX

El applet Controles de TX proporciona todos los controles manuales de transmisión en AetherSDR, incluyendo la medición de potencia directa y ROE (con retención de pico PEP), deslizadores de potencia RF/Sintonía, selección de perfil TX, botones TUNE/MOX/ATU/MEM e indicadores de estado APD (Predistorsión Adaptativa). En v0.9.7+, el botón MOX pasa a través del coordinador de tonos Quindar para que los tonos K/BK se reproduzcan al activar/desactivar PTT cuando Quindar está habilitado (solo modos de teléfono).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TX no está disponible sin una conexión activa a la radio.
- Abra el applet Controles de TX: haga clic en el botón de la bandeja TX en la barra lateral derecha si el applet aún no está visible.

## Ajuste de la potencia de salida RF

El deslizador "RF Power" establece la potencia directa máxima que el transmisor producirá durante la operación normal.

### Pasos

1. Localice el deslizador "RF Power:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia. La lectura numérica a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía a la radio.

### Escala del medidor

El medidor de potencia RF y el medidor de ROE muestran lecturas en tiempo real. Una barra de retención de pico PEP marca la potencia de envolvente de pico y disminuye después de una ventana de retención de 2 segundos. El pico se reinicia a cero cuando el transmisor desactiva la transmisión.

| Medidor | Escala | Umbral rojo |
|---|---|---|
| Potencia RF | 0–120 W (sin amplificador), 0–600 W (Aurora 500W) | > 100 W / > 500 W |
| ROE | 1.0–3.0 | > 2.5 |

### Lectura al pasar el cursor

Pase el mouse sobre el medidor de potencia RF o ROE para ver el valor exacto. La lectura de potencia RF muestra la potencia exacta en vatios (p. ej., "45 W") y la lectura de ROE muestra la relación en forma convencional (p. ej., "1.32:1"). Esto le ayuda a evitar estimar entre marcas durante la transmisión.

## Ajuste de la potencia de portadora de sintonía

El deslizador "Tune Pwr" establece el nivel de potencia de la portadora continua que se transmite al presionar TUNE. Mantener este valor bajo protege sus etapas finales y el sistema de antena durante la sintonización del ATU o las comprobaciones de ROE.

### Pasos

1. Localice el deslizador "Tune Pwr:" en el applet Controles de TX.
2. Arrastre el deslizador hacia la izquierda para disminuir o hacia la derecha para aumentar el nivel de potencia de la portadora de sintonía. La lectura numérica a la derecha del deslizador se actualiza inmediatamente.
3. Suelte el deslizador. El nuevo valor se envía a la radio.

### Visualización del valor al arrastrar

Al arrastrar el deslizador de Potencia RF o Potencia de Sintonía, un tooltip muestra el valor actual como porcentaje del máximo (p. ej., "45%") mientras mueve el deslizador. Esto le ayuda a establecer niveles de potencia precisos sin soltar el mouse.

## Selección de perfil TX

1. Localice el cuadro combinado "TX Profile:" en el applet Controles de TX.
2. Haga clic en el cuadro combinado para revelar la lista de perfiles TX disponibles en la radio.
3. Seleccione un perfil. La radio lo carga inmediatamente.

## Botón TUNE

1. Haga clic en TUNE para iniciar una portadora de sintonía continua al nivel establecido por "Tune Pwr".
   - El texto del botón cambia a "TUNING..." y el fondo se vuelve rojo.
2. Haga clic en TUNE nuevamente o haga clic en el botón TUNE para detener la portadora.

**Menú contextual con clic derecho**:
- Haga clic derecho en el botón TUNE para abrir un menú contextual para seleccionar la forma de la portadora del próximo ciclo de sintonía.
- Elija **Tono único** o **Dos tonos**. La selección es de un solo uso: el modo de sintonía de la radio vuelve a tono único al reiniciar, y AetherSDR no guarda la elección.

## Botón MOX

1. Haga clic en MOX para activar manualmente el transmisor.
   - El botón se vuelve rojo mientras el transmisor está activado.
2. Haga clic en MOX nuevamente para desactivar.
   - El botón vuelve a su estado inactivo con un borde y texto de acento ámbar, distinguiéndolo de los botones TUNE, ATU y MEM.

**Comportamiento del tono Quindar**:
- Al **activar**: si Quindar está habilitado en la tira de canal de audio y la franja TX activa está en un modo de teléfono, el tono K se reproduce antes de activar el transmisor.
- Al **desactivar**: el tono BK se reproduce después de que el transmisor se desactiva.
- Si Quindar está deshabilitado, o la franja TX activa no está en un modo de teléfono, el comportamiento es inmediato: el transmisor se activa y desactiva sin tonos.

## Botón ATU

El botón ATU inicia un ciclo de sintonización del ATU interno. El botón ATU alterna entre iniciar un ciclo de sintonía y omitir el sintonizador, reflejando el comportamiento por frecuencia en SmartSDR.

### Menú contextual con clic derecho

Haga clic derecho en el botón ATU para acceder a acciones adicionales del sintonizador:

| Elemento del menú | Acción |
|---|---|
| **Sintonización previa de bandas…** | Abre el diálogo de sintonización previa de bandas para barrer las memorias del sintonizador en todas las bandas. Solo habilitado cuando MEM está activado. |
| **Borrar memorias del ATU…** | Confirma y borra todas las memorias almacenadas del ATU. |

### Comportamiento del ciclo de sintonía

La acción exacta al hacer clic en ATU depende del estado actual del sintonizador y su frecuencia de transmisión:

| Situación | Lo que hace el clic en ATU |
|---|---|
| No existe una sintonización exitosa para la frecuencia actual | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU reporta una coincidencia exitosa y la frecuencia de transmisión no ha cambiado desde esa sintonización | Cambia el ATU a bypass. |
| El ATU reporta una coincidencia exitosa pero la frecuencia de transmisión ha cambiado desde esa sintonización | Inicia un nuevo ciclo de sintonía del ATU. |
| El ATU ya está en bypass | Inicia un nuevo ciclo de sintonía del ATU. |

En la práctica, esto significa:

1. Haga clic en ATU en una nueva frecuencia. La radio ejecuta un ciclo de sintonía. El indicador de éxito se enciende en verde cuando se encuentra una coincidencia.
2. Haga clic en ATU nuevamente sin cambiar la frecuencia. El sintonizador entra en bypass. El indicador Byp se enciende en naranja y el indicador de éxito se atenúa.
3. Cambie la frecuencia y haga clic en ATU. La radio ejecuta un nuevo ciclo de sintonía independientemente del resultado anterior.

El botón ATU y el botón MEM están deshabilitados cuando TGXL está en modo OPERATE.

## Botón MEM

1. Haga clic en MEM para activar o desactivar el uso de la memoria del ATU.
   - Cuando está activado, el indicador Mem se enciende en verde.
2. Haga clic en MEM nuevamente para desactivar el uso de la memoria.

El botón MEM está deshabilitado cuando TGXL está en modo OPERATE.

## Indicadores de estado del ATU

Tres indicadores muestran el estado actual del ATU:

| Indicador | Color | Significado |
|---|---|---|
| **Success** | Verde | El estado del ATU es Exitoso u OK |
| **Byp** | Naranja | El ATU está en Bypass o ManualBypass |
| **Mem** | Verde | El ATU está usando una memoria |

## APD (Predistorsión Adaptativa)

1. Haga clic en **APD** para activar/desactivar la predistorsión adaptativa en la radio.
2. Observe los tres indicadores de estado:

| Indicador | Color | Significado |
|---|---|---|
| **Active** | Verde | APD está activado y el ecualizador se aplica activamente |
| **Cal** | Verde | APD está activado y aún está calibrando |
| **Avail** | Verde | APD está activado y hay una calibración disponible pero aún no se ha aplicado |

La progresión típica es: **Cal** (calibrando) → **Avail** (listo) → **Active** (aplicado).

## Función de cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| RF Power | Establece el nivel máximo de potencia RF de transmisión (porcentaje del máximo). | 100 |
| Tune Pwr | Establece el nivel de potencia de la portadora de sintonía (porcentaje del máximo). | 10 |
| TX Profile | Selecciona un perfil TX de la radio. | — |
| TUNE | Inicia/detiene una portadora de sintonía. Haga clic derecho para la forma de portadora de tono único / dos tonos. | — |
| MOX | Activa/desactiva la transmisión manual. El estado inactivo muestra un borde de acento ámbar. | — |
| ATU | Inicia un ciclo de sintonización del ATU o alterna el bypass. Haga clic derecho para sintonización previa de bandas / borrar memorias del ATU. | — |
| MEM | Activa/desactiva el uso de la memoria del ATU. | — |
| APD | Activa/desactiva la predistorsión adaptativa. | — |

## Consejos

- Ajuste "Tune Pwr" al nivel mínimo que permita a su ATU encontrar una coincidencia. Muchos operadores usan 10-20% del máximo para la sintonización del ATU.
- El ajuste "Tune Pwr" es independiente de "RF Power", que controla la potencia de transmisión normal. Ajustar uno no afecta al otro.
- Puede establecer valores predeterminados de potencia de sintonía por banda en `Settings > TX Band Settings...`.
- La barra de retención de pico de potencia RF se reinicia a cero cuando el transmisor desactiva la transmisión, evitando que una lectura PEP retenida persista entre sobretiros.
- Los deslizadores de potencia ahora muestran valores como porcentajes de la potencia máxima de la radio. La potencia real en vatios depende del modelo de su radio y de cualquier amplificador externo.
- Pase el cursor sobre los medidores de potencia RF o ROE para ver lecturas precisas (vatios exactos o relación de ROE) en lugar de estimar entre marcas.

## Relacionado

- [Iniciar una portadora de sintonía para comprobar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)
