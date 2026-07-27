# Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le ofrece un solo clic para sacar al transmisor del estado TX, útil cuando MOX está atascado, una portadora de sintonía sigue activa o cualquier otra condición ha dejado la radio keyed y el applet de Controles TX no está a mano.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La insignia TX solo aparece en la barra de estado cuando hay una conexión activa con la radio.
- La radio debe estar actualmente en estado de transmisión (MOX keyed o portadora de sintonía activa) para que la insignia sea accionable.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR en la parte inferior de la ventana principal. La insignia es visible y está iluminada cuando la radio está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que la radio ha vuelto a recepción: el indicador RF Pwr en el applet Controles TX baja a cero, el botón MOX vuelve a su estado apagado (azul) y la etiqueta del botón TUNE vuelve a "TUNE" si había una portadora de sintonía activa.

## Consejos

- Si el applet Controles TX está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activo). La insignia TX de la barra de estado es la ruta más rápida cuando el applet está colapsado o fuera de la vista.
- Si MOX fue activado por un comando CAT o TCI externo, hacer clic en la insignia TX envía el mismo comando de desactivación. No importa la fuente del PTT original.

## Solución de problemas

- **Hacer clic en la insignia TX no detiene la transmisión** — La radio puede estar keyed por PTT de hardware (pedal o línea PTT del micrófono). Suelte primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware mantenida.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en Modo Mínimo (`View > Minimal Mode`). Deshabilitar el Modo Mínimo restaura la barra de estado.

## Relacionado

- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [TX Controls overview](overview.md)

***

# Descripción general de Controles TX

El applet Controles TX proporciona la interfaz principal para las operaciones de transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia de RF y potencia de sintonía (mostrados como porcentaje), un selector de perfil TX y botones para TUNE, MOX, ATU, MEM y APD (Predistorsión Adaptativa).

## Antes de empezar

- AetherSDR debe estar conectado a un FlexRadio FLEX-8600 con firmware 4.2 o posterior.
- La radio debe estar en un estado operativo (no en espera o fuera de línea).

## Controles

### RF Pwr (Medidor de Potencia Directa)

- Muestra la potencia directa en la salida del excitador en vatios.
- La escala cambia según el modelo de radio: 0–120 W (sin amplificador) o 0–600 W (con Aurora 500W).
- La zona roja indica >100 W (sin amplificador) o >500 W (con amplificador).
- El medidor incluye una **barra de retención de pico** que captura el valor máximo de PEP durante la transmisión. El pico se mantiene durante 2 segundos, luego decae hacia el nivel de potencia actual en aproximadamente 2.5 segundos desde el pico hasta el mínimo. El pico se restablece a cero inmediatamente cuando se desactiva el transmisor.
- Pase el cursor del mouse sobre el medidor para ver una lectura numérica exacta en el formato "X W" (ej., "75 W").

### SWR (Medidor de Relación de Ondas Estacionarias)

- Muestra la ROE en la salida del excitador.
- Rango 1.0–3.0, con zona roja que indica >2.5.
- Pase el cursor del mouse sobre el medidor para ver una lectura numérica exacta en el formato "N.N:1" (ej., "1.32:1").

### Control Deslizante de Potencia RF

- Establece el nivel de potencia de RF de transmisión como un porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setRfPower` cuando se ajusta.
- Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en el formato "X%" (ej., "75%").
- Cuando termina de arrastrar (suelta el botón del mouse), el valor se sincroniza desde el modelo de radio para garantizar una visualización precisa.

### Control Deslizante de Potencia de Sintonía

- Establece el nivel de potencia de la portadora de sintonía como un porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setTunePower` cuando se ajusta.
- Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en el formato "X%" (ej., "10%").
- Cuando termina de arrastrar (suelta el botón del mouse), el valor se sincroniza desde el modelo de radio para garantizar una visualización precisa.

### Cuadro Combinado de Perfil TX

- Selecciona un perfil de transmisión de la lista proporcionada por la radio (`profileList()`).
- Cambiar el perfil llama a `TransmitModel::loadProfile`.

### Indicadores ATU

Tres LED de estado indican el estado del ATU:

- **Success** — Se enciende en verde cuando el estado del ATU es `Successful` o `OK`.
- **Byp** — Se enciende en naranja cuando el ATU está en `Bypass` o `ManualBypass`.
- **Mem** — Se enciende en verde cuando el ATU está usando una memoria.

### Botón TUNE

- Inicia o detiene una portadora de sintonía. La etiqueta del botón cambia a "TUNING..." con un fondo rojo mientras está activo.
- **Clic derecho** para abrir un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:
  - **Mono Tone** — Portadora de tono único tradicional.
  - **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación.
  
  La selección es transitoria de un solo uso: se aplica solo a la siguiente pulsación de TUNE y no se conserva en AppSettings. El `tune_mode` de la radio vuelve a `single_tone` tras los ciclos de alimentación.
- El botón está marcado como un control de keying TX en la interfaz de usuario (emite una portadora de sintonía).

### Botón MOX

- Activa o desactiva la transmisión manual. El botón se vuelve rojo mientras TX está keyed.
- Cuando los tonos Quindar están habilitados en la tira de canal de audio, los tonos K y BK se reproducen al activar y desactivar en modos de teléfono.
- El botón está marcado como un control de keying TX en la interfaz de usuario (PTT manual).
- **Apariencia en reposo:** Cuando no está transmitiendo, el botón MOX muestra un borde ámbar y un acento de texto ámbar, distinguiéndolo de los botones neutros TUNE, ATU y MEM. Este acento es personalizable en el Editor de Temas usando los colores tokenizados `color.tx.mox.border`, `color.tx.mox.text`, `color.tx.mox.border.hover` y `color.tx.mox.text.hover`.

### Botón ATU

- Inicia el ciclo de sintonía del ATU interno.
- **Deshabilitado** cuando TGXL está en modo OPERATE.
- El botón está marcado como un control de keying TX en la interfaz de usuario (inicia la sintonía del ATU).
- **Clic derecho** para abrir un menú contextual con dos opciones:
  - **Pre-tune bands…** — Abre un diálogo para ejecutar el barrido de presintonía del ATU en las bandas seleccionadas por el usuario. Esta acción requiere que MEM esté habilitado primero; si MEM está desactivado, el elemento del menú aparece atenuado con una información sobre herramientas.
  - **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias del ATU de la radio.

### Botón MEM

- Activa o desactiva la recuperación de memoria del ATU.
- **Deshabilitado** cuando TGXL está en modo OPERATE.

### Botón APD y Grupo de Estado

- **APD** — Botón de alternancia que habilita o deshabilita la Predistorsión Adaptativa en la radio.
- Tres indicadores de estado muestran el estado de APD:
  - **Active** — Se enciende en verde cuando APD está activado y el ecualizador se aplica activamente.
  - **Cal** — Se enciende en verde cuando APD está activado y aún está calibrando.
  - **Avail** — Se enciende en verde cuando APD está activado y hay una calibración disponible pero aún no se ha aplicado.
  
  La progresión típica es: Cal (calibrando) → Avail (listo) → Active (aplicado).

## Comportamiento de Retención de Pico

El medidor de potencia directa incluye una función de retención de pico que captura la potencia PEP máxima durante una transmisión. La barra de retención de pico:

- Se actualiza instantáneamente cuando se detecta un nuevo pico.
- Mantiene el valor pico durante 2 segundos.
- Después del período de retención, decae hacia el nivel de potencia suavizado actual. La tasa de decaimiento se escala al rango de escala completa del medidor (120 W o 600 W), por lo que la sensación visual (~2.5 segundos desde el pico hasta el mínimo) es consistente en ambas escalas.
- Se restablece a cero inmediatamente cuando se desactiva el transmisor (MOX liberado o TUNE detenido). Esto evita que una lectura PEP retenida persista entre sobretiros.

## Marcadores de Control de Keying TX

Los botones TUNE, MOX y ATU están marcados internamente como controles de keying TX (`markTxKeying`). Este marcador es utilizado por la utilidad `TxKeyingMarker` para identificar controles que pueden keyer el transmisor. El marcador no cambia la apariencia visible de los botones, pero se usa internamente para un comportamiento consistente en toda la aplicación.

## Relacionado

- [Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado](cancel-an-active-or-stuck-transmission-with-the-status-bar-tx-badge.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
