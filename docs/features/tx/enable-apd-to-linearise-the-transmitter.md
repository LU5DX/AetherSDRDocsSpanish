# Controles de TX

El applet Controles de TX proporciona controles de transmisión para la radio, incluyendo medidores de potencia directa y ROE, deslizadores de potencia de RF y de tono de sintonía, un selector de perfil TX y botones TUNE/MOX/ATU/MEM. También incluye el conmutador APD (Adaptive Pre-Distortion, predistorsión adaptativa) con indicadores de estado Active/Cal/Avail.

## Abrir el applet Controles de TX

Si el applet Controles de TX no está visible, haga clic en el botón TX de la barra lateral derecha.

## APD (Adaptive Pre-Distortion)

El APD reduce la no linealidad del transmisor aplicando un ecualizador de corrección a la señal antes de que llegue al PA. Activarlo mejora la pureza espectral, especialmente en SSB y modos digitales.

### Activar APD

1. Localice el botón APD en la parte inferior del applet Controles de TX.
2. Haga clic en APD para activar la predistorsión adaptativa. El fondo del botón cambia a verde cuando está activado.
3. Observe los indicadores de estado a la derecha del botón:
   - **Cal** se enciende en verde mientras la radio recopila datos de calibración.
   - **Avail** se enciende en verde cuando una calibración está completa pero aún no se ha aplicado.
   - **Active** se enciende en verde cuando el ecualizador se aplica a la señal de transmisión.
4. Para desactivar APD, haga clic nuevamente en APD. El botón vuelve a su estado sin iluminar y los tres indicadores se apagan.

La progresión normal después de activar APD es: Cal → Avail → Active.

| Control | Tipo          | Comportamiento                                                                                 |
|---------|---------------|------------------------------------------------------------------------------------------------|
| APD     | Botón de conmutación | Activa o desactiva la predistorsión adaptativa en la radio. Verde cuando está activado, sin iluminar cuando está desactivado. |
| Active  | Indicador     | Se enciende en verde cuando APD está activado y el ecualizador se aplica activamente a la señal. |
| Cal     | Indicador     | Se enciende en verde cuando APD está activado y la radio aún está calibrando.                  |
| Avail   | Indicador     | Se enciende en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada. |

### Consejos

- La calibración de APD se realiza automáticamente después de activarlo. No necesita transmitir manualmente para activarla; espere a que los indicadores avancen por Cal → Avail → Active.
- Si desactiva y reactiva APD, la secuencia de calibración se reinicia desde Cal.

## Medidores RF Pwr y SWR

La potencia directa se muestra como una barra de medición horizontal. La escala cambia según el modelo de radio (sin amplificador 0–120 W, o Aurora 500W 0–600 W). La barra se vuelve roja por encima de 100 W (sin amplificador) o 500 W (Aurora).

Retención de pico PEP: la lectura máxima se mantiene durante 2 segundos y luego decae suavemente hasta el valor actual. El pico se borra inmediatamente cuando el transmisor deja de transmitir para evitar lecturas residuales entre ráfagas.

Pase el cursor sobre la barra RF Pwr para ver la lectura exacta de potencia en vatios (por ejemplo, "45 W").

El SWR se muestra como una barra de medición horizontal. Rango 1.0–3.0. La barra se vuelve roja por encima de 2.5.

Pase el cursor sobre la barra SWR para ver la relación exacta en forma convencional (por ejemplo, "1.52:1").

Cuando el transmisor no está transmitiendo, ambas barras permanecen en cero potencia / 1.0 SWR. Si la radio no reporta una lectura válida de SWR durante la transmisión, la barra SWR permanece en su posición de reposo de 1.0 en lugar de mostrar un valor fuera de escala.

| Control | Tipo   | Comportamiento                                                                                                                                                                                                                                                                      |
|---------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Pwr  | Medidor  | Muestra la potencia directa a la salida del excitador con retención de pico PEP (retención de 2 s y decaimiento al valor suavizado actual en ~2.5 s). El pico se reinicia inmediatamente al dejar de transmitir. La escala cambia según el modelo de radio. Rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W). |
| SWR     | Medidor  | Muestra la relación de onda estacionaria en el excitador. Rango 1.0–3.0, rojo por encima de 2.5. Permanece en 1.0 cuando no hay lectura válida disponible o el transmisor no está transmitiendo.                    |

## Deslizadores RF Power / Tune Power

| Control    | Tipo   | Comportamiento                                                                                                                                                                                                                                                                      |
|------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RF Power   | Deslizador | Establece el nivel de potencia de transmisión RF como porcentaje del máximo (0–100%). Valor predeterminado: 100%. Durante el arrastre, muestra el valor actual como "XX%" sobre el control deslizante. El valor se fija en la última posición establecida al soltar. |
| Tune Pwr   | Deslizador | Establece el nivel de potencia de la portadora de sintonía como porcentaje del máximo (0–100%). Valor predeterminado: 10%. Durante el arrastre, muestra el valor actual como "XX%" sobre el control deslizante. El valor se fija en la última posición establecida al soltar. |

Al soltar cualquiera de los deslizadores, el valor se sincroniza desde el modelo de radio, lo que garantiza que el valor mostrado coincida con el estado real de la radio incluso si la radio rechazó el valor intermedio durante el arrastre.

## Selector de perfil TX

Seleccione un perfil TX en el cuadro combinado para cargarlo en la radio. Los perfiles se completan desde la lista de perfiles de la radio.

## Botón TUNE

Haga clic en TUNE para iniciar o detener una portadora de sintonía. La etiqueta del botón cambia a **TUNING...** con fondo rojo mientras la portadora está activa.

### Menú contextual de TUNE

Haga clic derecho en el botón TUNE para elegir la forma de la portadora para el siguiente ciclo de sintonía:

| Acción      | Comportamiento                                                                                          |
|-------------|----------------------------------------------------------------------------------------------------------|
| Mono Tone   | Establece la portadora de sintonía en un tono único. Marcado si este es el modo actual.                  |
| Two Tone    | Establece la portadora de sintonía en dos tonos. Marcado si este es el modo actual.                      |

La selección es transitoria de un solo uso: el modo de sintonía de la radio vuelve al tono único tras los ciclos de alimentación. AetherSDR no conserva la elección en AppSettings.

| Control | Tipo        | Comportamiento                                                                                        |
|---------|-------------|--------------------------------------------------------------------------------------------------------|
| TUNE    | Botón pulsador | Inicia/detiene la portadora de sintonía; el texto cambia a **TUNING...** con fondo rojo mientras está activa. El clic derecho selecciona la forma de la portadora (Mono Tone / Two Tone) para el siguiente ciclo de sintonía. |

## Botón MOX y tonos Quindar

Al hacer clic en MOX, la acción pasa por el coordinador de tonos Quindar en lugar de conmutar el transmisor directamente. Esto significa:

- **Activar (clic en MOX para activar):** si Quindar está habilitado en la tira de canales de Audio y la slice TX activa está en modo de fonía, el tono K suena antes de que el transmisor se active.
- **Desactivar (clic en MOX para desactivar):** el tono BK suena después de que el transmisor se desactiva.
- Si Quindar está deshabilitado, o la slice TX activa no está en modo de fonía, MOX se comporta como antes y activa el transmisor inmediatamente.

El botón MOX tiene una apariencia distintiva incluso en reposo (borde y texto ámbar) para distinguirlo de los botones TUNE/ATU/MEM. El botón se vuelve rojo mientras el transmisor está activado y vuelve a su acento ámbar cuando el transmisor está apagado. Los colores de acento son editables mediante el tema usando los tokens `color.tx.mox.*`.

Cuando el transmisor está activado, el botón MOX se vuelve rojo. Cuando el transmisor está apagado, el botón vuelve a su acento ámbar.

| Control | Tipo          | Comportamiento                                                                                                                                                      |
|---------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| MOX     | Botón de conmutación | Conmuta la transmisión manual. Pasa por el coordinador de tonos Quindar para que los tonos K/BK suenen al activar/desactivar PTT en modos de fonía cuando Quindar está habilitado. El botón se vuelve rojo mientras TX está activado, acento ámbar en reposo. |

## Botón ATU

El botón ATU inicia el ciclo de sintonización del sintonizador de antena interno. Utiliza una conmutación por frecuencia que refleja el comportamiento de SmartSDR:

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonía ATU.
- **Segundo clic en la misma frecuencia**, cuando el ATU reporta una coincidencia exitosa: cambia el sintonizador a bypass.
- **Clic después de cualquier cambio de frecuencia**: siempre inicia un nuevo ciclo de sintonía, incluso si el estado anterior fue exitoso.

El estado de bypass se borra automáticamente cuando cambia la frecuencia de transmisión, por lo que el siguiente clic iniciará una nueva sintonía en lugar de activar el bypass. No hay cambios en la etiqueta ni en la apariencia del botón ATU; los indicadores **Success**, **Byp** y **Mem** debajo del botón siguen reflejando el estado del ATU como antes.

### Menú contextual de ATU

Haga clic derecho en el botón ATU para abrir un menú contextual con dos acciones:

| Acción                       | Comportamiento                                                                                     |
|------------------------------|-----------------------------------------------------------------------------------------------------|
| Pre-tune bands…              | Abre el diálogo ATU Pre-Tune para barrer y almacenar configuraciones del sintonizador en todas las bandas. Habilitado solo cuando MEM está activado. |
| Clear ATU memories…          | Borra todas las memorias ATU almacenadas en la radio. Aparece un diálogo de confirmación antes de borrar. |

| Indicador | Tipo      | Comportamiento                                                          |
|-----------|-----------|--------------------------------------------------------------------------|
| Success   | Indicador | Se enciende en verde cuando el ATU reporta una coincidencia exitosa u OK. |
| Byp       | Indicador | Se enciende en naranja cuando el ATU está en bypass o bypass manual.      |
| Mem       | Indicador | Se enciende en verde cuando el ATU está usando una memoria almacenada.    |

| Control | Tipo        | Comportamiento                                                                                        |
|---------|-------------|---------------------------------------------------------------------------------------------------------|
| ATU     | Botón pulsador | Inicia el ciclo de sintonización del ATU interno. Si el estado es Successful/OK en la misma frecuencia, un segundo clic envía bypass en su lugar. El clic derecho abre las acciones de barrido de pre-sintonía y Clear ATU Memories. |

### Disponibilidad de ATU y MEM

Los botones ATU y MEM se deshabilitan con información sobre herramientas explicativa en dos situaciones:

- **Sin sintonizador de antena instalado:** la radio no reporta ATU interno. La información sobre herramientas dice "This radio has no antenna tuner".
- **TGXL en modo OPERATE:** el amplificador TGXL está presente y en OPERATE (no en bypass). La información sobre herramientas dice "Disabled — TGXL is in OPERATE mode".

Cuando está deshabilitado por cualquiera de estas razones, el botón TUNE permanece habilitado para que pueda seguir enviando una portadora a través del TGXL para verificaciones de potencia y SWR.

| Control | Tipo          | Comportamiento                                                                        |
|---------|---------------|----------------------------------------------------------------------------------------|
| MEM     | Botón de conmutación | Conmuta la recuperación de memoria ATU activada/desactivada. Deshabilitado cuando la radio no tiene ATU o cuando TGXL está en modo OPERATE. |

## Soporte de temas

A partir de v26.6.1, el applet Controles de TX utiliza colores adaptables al tema para todos los controles e indicadores. El relleno de los deslizadores, los colores de las etiquetas y los estados de los indicadores se adaptan al tema activo. Si usa un tema personalizado, estos controles respetarán el alcance `applet/tx` en la definición del tema.

El botón MOX y las barras RF Pwr/SWR también admiten tokens de tema. El botón MOX usa `color.tx.mox.border`, `color.tx.mox.text`, `color.tx.mox.border.hover` y `color.tx.mox.text.hover` para su color de acento en reposo. Las información sobre herramientas de las barras usan el estilo de información sobre herramientas predeterminado del tema.

## Relacionado

- [Descripción general de Controles de TX](overview.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
- [Establecer potencia de salida RF](set-rf-output-power.md)
