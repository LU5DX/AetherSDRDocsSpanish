# Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le ofrece un solo clic para sacar al transmisor del estado TX. Esto resulta útil cuando MOX está atascado en activo, una portadora de sintonía sigue en marcha, o cualquier otra condición ha dejado la radio en transmisión y el applet de Control TX no está a la mano.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La insignia TX solo aparece en la barra de estado cuando hay una conexión de radio activa.
- La radio debe estar actualmente en estado de transmisión (MOX activado o portadora de sintonía activa) para que la insignia sea accionable.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR, en la parte inferior de la ventana principal. La insignia es visible y está iluminada cuando la radio está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que la radio ha vuelto a recepción: el indicador de RF Pwr en el applet de Control TX baja a cero, el botón MOX vuelve a su estado sin iluminar (azul), y la etiqueta del botón TUNE vuelve a "TUNE" si una portadora de sintonía estaba activa.

## Consejos

- Si el applet de Control TX está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activo). La insignia TX de la barra de estado es la vía más rápida cuando el applet está colapsado o fuera de vista.
- Si MOX fue activado por un comando CAT o TCI externo, hacer clic en la insignia TX envía el mismo comando de desactivación. La fuente del PTT original no importa.

## Solución de problemas

- **Hacer clic en la insignia TX no detiene la transmisión** — La radio puede estar activada por PTT de hardware (pedal o línea PTT del micrófono). Libere primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware mantenida activa.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en Modo Mínimo (`View > Minimal Mode`). Desactivar el Modo Mínimo restaura la barra de estado.

## Relacionados

- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Descripción general de Control TX](overview.md)

***

# Descripción general de Control TX

El applet de Control TX proporciona la interfaz principal para las operaciones de transmisión: medidores de potencia directa y ROE, deslizadores para potencia de RF y potencia de sintonía (mostrados como porcentaje), un selector de perfil TX, y botones para TUNE, MOX, ATU, MEM y APD (predistorsión adaptativa).

## Antes de comenzar

- AetherSDR debe estar conectado a un FlexRadio FLEX-8600 con firmware 4.2 o posterior.
- La radio debe estar en un estado operativo (no en espera ni sin conexión).

## Controles

### RF Pwr (Medidor de potencia directa)

- Muestra la potencia directa en la salida del excitador en vatios.
- La escala cambia según el modelo de radio: 0–120 W (sin amplificador) o 0–600 W (con amplificador Aurora 500W).
- La zona roja indica >100 W (sin amplificador) o >500 W (con amplificador).
- El medidor incluye una **barra de retención de pico** que captura el valor máximo de PEP durante la transmisión. El pico se mantiene durante 2 segundos y luego decae hacia el nivel de potencia actual en aproximadamente 2,5 segundos desde el pico hasta el fondo.
- Cuando no se transmite, el medidor permanece en cero. Cuando el transmisor se desactiva, tanto la lectura en vivo como la barra de retención de pico caen a cero inmediatamente, de modo que no queda ninguna muestra de potencia obsoleta en la pantalla.
- Pase el cursor del mouse sobre el medidor para ver una lectura numérica exacta en el formato "X W" (p. ej., "75 W").

### ROE (Medidor de relación de onda estacionaria)

- Muestra la ROE en la salida del excitador.
- Rango 1,0–3,0, con zona roja que indica >2,5.
- Cuando no se transmite, el medidor permanece en 1,0 (mínimo). Cuando el transmisor se desactiva, el medidor vuelve a 1,0 inmediatamente.
- Si no hay lectura de ROE disponible durante la transmisión, el medidor también permanece en 1,0 en lugar de mostrar un cero crudo o una relación obsoleta.
- Pase el cursor del mouse sobre el medidor para ver una lectura numérica exacta en el formato "N,N:1" (p. ej., "1,32:1").

### Deslizador de potencia de RF

- Establece el nivel de potencia de RF de transmisión como porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setRfPower` al ajustarse.
- Al arrastrar el deslizador, una información sobre herramientas muestra el valor actual en el formato "X%" (p. ej., "75%").
- Al terminar de arrastrar (soltar el botón del mouse), el valor se sincroniza desde el modelo de radio para garantizar una visualización precisa.

### Deslizador de potencia de sintonía

- Establece el nivel de potencia de la portadora de sintonía como porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setTunePower` al ajustarse.
- Al arrastrar el deslizador, una información sobre herramientas muestra el valor actual en el formato "X%" (p. ej., "10%").
- Al terminar de arrastrar (soltar el botón del mouse), el valor se sincroniza desde el modelo de radio para garantizar una visualización precisa.

### Cuadro combinado de perfil TX

- Selecciona un perfil de transmisión de la lista proporcionada por la radio (`profileList()`).
- Cambiar el perfil llama a `TransmitModel::loadProfile`.

### Indicadores ATU

Tres LED de estado indican el estado del ATU:

- **Success** — Se ilumina en verde cuando el estado del ATU es `Successful` o `OK`.
- **Byp** — Se ilumina en naranja cuando el ATU está en `Bypass` o `ManualBypass`.
- **Mem** — Se ilumina en verde cuando el ATU está usando una memoria.

### Botón TUNE

- Inicia o detiene una portadora de sintonía. La etiqueta del botón cambia a "TUNING..." con fondo rojo mientras está activo.
- **Clic derecho** para abrir un menú contextual y seleccionar la forma de portadora para el siguiente ciclo de sintonía:
  - **Mono Tone** — Portadora tradicional de tono único.
  - **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación.
  
  La selección es transitoria de un solo uso: se aplica solo a la siguiente pulsación de TUNE y no se guarda en AppSettings. El `tune_mode` de la radio vuelve a `single_tone` tras los ciclos de alimentación.
- El botón está marcado como control de activación TX en la interfaz (emite una portadora de sintonía).

### Botón MOX

- Alterna la transmisión manual activada/desactivada. El botón se pone rojo mientras TX está activado.
- Cuando los tonos Quindar están habilitados en la tira de canal de audio, los tonos K y BK suenan al activar y desactivar en modos de telefonía.
- El botón está marcado como control de activación TX en la interfaz (PTT manual).
- **Apariencia en reposo:** Cuando no se transmite, el botón MOX muestra un borde ámbar y un acento de texto ámbar, distinguiéndolo de los botones neutros TUNE, ATU y MEM. Este acento es personalizable en el Editor de Temas usando los colores tokenizados `color.tx.mox.border`, `color.tx.mox.text`, `color.tx.mox.border.hover` y `color.tx.mox.text.hover`.

### Botón ATU

- Inicia el ciclo de sintonía del ATU interno.
- Si el estado del ATU es `Successful` o `OK` en la frecuencia actual, un segundo clic envía una derivación (bypass).
- **Deshabilitado** cuando la radio no tiene acoplador de antena (p. ej., un Hermes-Lite 2) o cuando TGXL está en modo OPERATE. Pase el cursor sobre el botón deshabilitado para ver el motivo:
  - **"This radio has no antenna tuner"** — La radio no tiene ATU instalado. El motivo de falta de acoplador se informa primero porque es la condición más fundamental, incluso si TGXL también está en modo OPERATE.
  - **"Disabled — TGXL is in OPERATE mode"** — La radio tiene acoplador, pero TGXL está en modo OPERATE.
- El botón está marcado como control de activación TX en la interfaz (inicia la sintonía del ATU).
- **Clic derecho** para abrir un menú contextual con dos opciones:
  - **Pre-tune bands…** — Abre un diálogo para ejecutar el barrido de pre-sintonía del ATU en las bandas seleccionadas por el usuario. Esta acción requiere que MEM esté habilitado primero; si MEM está desactivado, el elemento del menú aparece atenuado con una información sobre herramientas.
  - **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias del ATU de la radio.

### Botón MEM

- Alterna el recuerdo de memoria del ATU activado/desactivado.
- **Deshabilitado** cuando la radio no tiene acoplador de antena o cuando TGXL está en modo OPERATE. La información sobre herramientas explica el motivo, usando la misma lógica que el botón ATU.

### Botón APD y grupo de estado

- **APD** — Botón de alternancia que habilita o deshabilita la predistorsión adaptativa en la radio.
- Tres indicadores de estado muestran el estado del APD:
  - **Active** — Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente.
  - **Cal** — Se ilumina en verde cuando APD está activado y aún está calibrando.
  - **Avail** — Se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.
  
  La progresión típica es: Cal (calibrando) → Avail (listo) → Active (aplicado).
- El botón APD y el grupo de estado están ocultos en radios que no admiten APD. En un inicio en frío, el grupo no aparece hasta que la radio confirma que admite APD — nunca muestra un botón con apariencia funcional sin funcionalidad de respaldo.

## Comportamiento de retención de pico

El medidor de potencia directa incluye una función de retención de pico que captura el PEP máximo (potencia de envolvente de pico) durante una transmisión. La barra de retención de pico:

- Se actualiza instantáneamente cuando se detecta un nuevo pico.
- Mantiene el valor de pico durante 2 segundos.
- Después del período de retención, decae hacia el nivel de potencia suavizado actual. La tasa de decaimiento está escalada al rango de escala completa del medidor (120 W o 600 W), de modo que la sensación visual (~2,5 segundos desde el pico hasta el fondo) es consistente en ambas escalas.
- Se restablece a cero inmediatamente cuando el transmisor se desactiva (MOX liberado o TUNE detenido). Esto evita que una lectura de PEP retenida permanezca entre transmisiones.

Cuando el transmisor se desactiva, la lectura de potencia en vivo también cae a cero inmediatamente — la última muestra no queda pintada en el medidor.

## Marcadores de control de activación TX

Los botones TUNE, MOX y ATU están marcados internamente como controles de activación TX (`markTxKeying`). Este marcador es usado por la utilidad `TxKeyingMarker` para identificar controles que pueden activar el transmisor. El marcador no cambia la apariencia visible de los botones, pero se usa internamente para un comportamiento consistente en toda la aplicación.

## Relacionados

- [Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado](cancel-an-active-or-stuck-transmission-with-the-status-bar-tx-badge.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
