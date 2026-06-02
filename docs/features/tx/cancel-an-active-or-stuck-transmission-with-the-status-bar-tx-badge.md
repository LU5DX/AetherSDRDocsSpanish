# Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le permite detener la transmisión con un solo clic, útil cuando MOX está atascado, una portadora de sintonía sigue activa, o cualquier otra condición ha dejado la radio en transmisión y la ventana de controles TX no está disponible de inmediato.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La insignia TX solo aparece en la barra de estado cuando hay una conexión de radio activa.
- La radio debe estar actualmente en estado de transmisión (MOX activado o portadora de sintonía activa) para que la insignia sea funcional.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR en la parte inferior de la ventana principal. La insignia es visible y está iluminada cuando la radio está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que la radio ha vuelto a recepción: el indicador RF Pwr en la ventana TX Controls baja a cero, el botón MOX vuelve a su estado apagado (azul), y la etiqueta del botón TUNE vuelve a "TUNE" si había una portadora de sintonía activa.

## Consejos

- Si la ventana TX Controls está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activo). La insignia TX de la barra de estado es la ruta más rápida cuando la ventana está colapsada o fuera de vista.
- Si MOX fue activado por un comando externo CAT o TCI, hacer clic en la insignia TX envía el mismo comando de desactivación. La fuente original del PTT no importa.

## Solución de problemas

- **Hacer clic en la insignia TX no detiene la transmisión** — La radio puede estar activada por PTT de hardware (pedal o línea PTT del micrófono). Libere primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware mantenida activa.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en modo mínimo (`View > Minimal Mode`). Desactivar el modo mínimo restaura la barra de estado.

## Relacionado

- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [TX Controls overview](overview.md)

***

# TX Controls overview

La ventana TX Controls proporciona la interfaz principal para las operaciones de transmisión: medidores de potencia directa y ROE, deslizadores de potencia de RF y potencia de sintonía (mostrados como porcentaje), un selector de perfil TX, y botones para TUNE, MOX, ATU, MEM y APD (Adaptive Pre-Distortion, predistorsión adaptativa).

## Antes de comenzar

- AetherSDR debe estar conectado a un FlexRadio FLEX-8600 con firmware 4.2 o posterior.
- La radio debe estar en un estado operativo (no en espera ni desconectada).

## Controles

### RF Pwr (Medidor de potencia directa)

- Muestra la potencia directa en la salida del excitador en vatios.
- La escala cambia según el modelo de radio: 0–120 W (sin amplificador) o 0–600 W (con amplificador Aurora 500W).
- La zona roja indica >100 W (sin amplificador) o >500 W (con amplificador).
- El medidor incluye una **barra de retención de pico** que captura el valor PEP máximo durante la transmisión. El pico se mantiene durante 2 segundos, luego disminuye hacia el nivel de potencia actual en aproximadamente 2.5 segundos desde el pico hasta el mínimo. El pico se reinicia a cero inmediatamente cuando se desactiva el transmisor.

### SWR (Medidor de ROE)

- Muestra la ROE en la salida del excitador.
- Rango 1.0–3.0, con zona roja que indica >2.5.

### Deslizador de potencia de RF

- Establece el nivel de potencia de transmisión de RF como porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setRfPower` cuando se ajusta.
- Al arrastrar el deslizador, un cuadro informativo muestra el valor actual en el formato "X%" (ej., "75%").

### Deslizador de potencia de sintonía

- Establece el nivel de potencia de la portadora de sintonía como porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setTunePower` cuando se ajusta.
- Al arrastrar el deslizador, un cuadro informativo muestra el valor actual en el formato "X%" (ej., "10%").

### Cuadro combinado de perfil TX

- Selecciona un perfil de transmisión de la lista proporcionada por la radio (`profileList()`).
- Cambiar el perfil llama a `TransmitModel::loadProfile`.

### Indicadores ATU

Tres LED de estado indican el estado de la ATU:

- **Success** — Se ilumina en verde cuando el estado de la ATU es `Successful` o `OK`.
- **Byp** — Se ilumina en naranja cuando la ATU está en `Bypass` o `ManualBypass`.
- **Mem** — Se ilumina en verde cuando la ATU está usando una memoria.

### Botón TUNE

- Inicia o detiene una portadora de sintonía. La etiqueta del botón cambia a "TUNING..." con fondo rojo mientras está activo.
- **Clic derecho** para abrir un menú contextual para seleccionar la forma de la portadora para el siguiente ciclo de sintonía:
  - **Mono Tone** — Portadora tradicional de un solo tono.
  - **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación.
  
  La selección es transitoria de un solo uso: se aplica solo a la siguiente pulsación de TUNE y no se conserva en AppSettings. El `tune_mode` de la radio vuelve a `single_tone` tras los ciclos de alimentación.

### Botón MOX

- Activa/desactiva manualmente la transmisión. El botón se vuelve rojo mientras TX está activado.
- Cuando los tonos Quindar están habilitados en la tira de canal de audio, los tonos K y BK suenan al activar y desactivar en modos de fonía.

### Botón ATU

- Inicia el ciclo de sintonía de la ATU interna.
- **Deshabilitado** cuando TGXL está en modo OPERATE.
- **Clic derecho** para abrir un menú contextual con dos opciones:
  - **Pre-tune bands…** — Abre un diálogo para ejecutar el barrido de pre-sintonía de la ATU en las bandas seleccionadas por el usuario. Esta acción requiere que MEM esté habilitado primero; si MEM está desactivado, el elemento del menú aparece atenuado con un cuadro informativo.
  - **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias de la ATU de la radio.

### Botón MEM

- Activa/desactiva el recuerdo de memoria de la ATU.
- **Deshabilitado** cuando TGXL está en modo OPERATE.

### Botón APD y grupo de estado

- **APD** — Botón de alternancia que habilita o deshabilita la predistorsión adaptativa en la radio.
- Tres indicadores de estado muestran el estado de APD:
  - **Active** — Se ilumina en verde cuando APD está activado y el ecualizador se aplica activamente.
  - **Cal** — Se ilumina en verde cuando APD está activado y aún está calibrando.
  - **Avail** — Se ilumina en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.
  
  La progresión típica es: Cal (calibrando) → Avail (listo) → Active (aplicado).

## Comportamiento de retención de pico

El medidor de potencia directa incluye una función de retención de pico que captura el PEP máximo (potencia de envolvente de pico) durante una transmisión. La barra de retención de pico:

- Se actualiza instantáneamente cuando se detecta un nuevo pico.
- Mantiene el valor pico durante 2 segundos.
- Después del período de retención, disminuye hacia el nivel de potencia suavizado actual. La tasa de disminución se escala al rango completo del medidor (120 W o 600 W), por lo que la sensación visual (~2.5 segundos desde el pico hasta el mínimo) es consistente en ambas escalas.
- Se reinicia a cero inmediatamente cuando se desactiva el transmisor (MOX liberado o TUNE detenido). Esto evita que una lectura PEP retenida persista entre sobretiros.

## Relacionado

- [Cancel an active or stuck transmission with the status bar TX badge](cancel-an-active-or-stuck-transmission-with-the-status-bar-tx-badge.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
