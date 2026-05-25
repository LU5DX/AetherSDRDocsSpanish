# Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le permite, con un solo clic, desactivar el transmisor y salir del modo TX, útil cuando MOX está atascado en encendido, una portadora de sintonía sigue activa o cualquier otra condición ha dejado el equipo en transmisión y el applet de Controles TX no está disponible de inmediato.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. La insignia TX solo aparece en la barra de estado cuando hay una conexión activa con el equipo.
- El equipo debe estar actualmente en estado de transmisión (MOX activado o portadora de sintonía activa) para que la insignia sea operable.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR en la parte inferior de la ventana principal. La insignia es visible y se ilumina cuando el equipo está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que el equipo ha vuelto a recepción: el indicador RF Pwr en el applet de Controles TX baja a cero, el botón MOX vuelve a su estado sin iluminar (azul) y la etiqueta del botón TUNE vuelve a "TUNE" si había una portadora de sintonía activa.

## Consejos

- Si el applet de Controles TX está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activo). La insignia TX de la barra de estado es la ruta más rápida cuando el applet está colapsado o fuera de vista.
- Si MOX fue activado por un comando externo CAT o TCI, al hacer clic en la insignia TX se envía el mismo comando de desactivación. La fuente original del PTT no importa.

## Solución de problemas

- **Al hacer clic en la insignia TX no se detiene la transmisión** — El equipo puede estar activado por PTT de hardware (pedal o línea PTT del micrófono). Suelte primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware sostenida.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en modo Mínimo (`View > Minimal Mode`). Desactivar el modo Mínimo restaura la barra de estado.

## Relacionado

- [Activar MOX para poner manualmente el transmisor en transmisión](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Resumen de Controles TX](overview.md)

***

# Resumen de Controles TX

El applet de Controles TX proporciona la interfaz principal para las operaciones de transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia RF y potencia de sintonía, un selector de perfil TX y botones para TUNE, MOX, ATU, MEM y APD (Predistorsión Adaptativa).

## Antes de comenzar

- AetherSDR debe estar conectado a un FlexRadio FLEX-8600 con firmware 4.2 o posterior.
- El equipo debe estar en un estado operativo (no en espera ni fuera de línea).

## Controles

### RF Pwr (Medidor de potencia directa)

- Muestra la potencia directa en la salida del excitador en vatios.
- La escala cambia según el modelo del equipo: 0–120 W (sin amplificador) o 0–600 W (con amplificador Aurora 500W).
- La zona roja indica >100 W (sin amplificador) o >500 W (con amplificador).
- El medidor incluye una **barra de retención de pico** que captura el valor máximo de PEP durante la transmisión. El pico se mantiene durante 2 segundos y luego disminuye hacia el nivel de potencia actual en aproximadamente 2.5 segundos desde el pico hasta el mínimo. El pico se reinicia a cero inmediatamente cuando se desactiva el transmisor.

### SWR (Medidor de relación de onda estacionaria)

- Muestra la ROE en la salida del excitador.
- Rango 1.0–3.0, con zona roja que indica >2.5.

### Control deslizante de potencia RF

- Establece el nivel de potencia RF de transmisión como un porcentaje (0–100), que se asigna a vatios según la escala de potencia del equipo.
- Llama a `TransmitModel::setRfPower` cuando se ajusta.
- Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en el formato "X W" (por ejemplo, "75 W").

### Control deslizante de potencia de sintonía

- Establece el nivel de potencia de la portadora de sintonía como un porcentaje (0–100), que se asigna a vatios según la escala de potencia del equipo.
- Llama a `TransmitModel::setTunePower` cuando se ajusta.
- Al arrastrar el control deslizante, una información sobre herramientas muestra el valor actual en el formato "X W" (por ejemplo, "10 W").

### Cuadro combinado de perfil TX

- Selecciona un perfil de transmisión de la lista proporcionada por el equipo (`profileList()`).
- Cambiar el perfil llama a `TransmitModel::loadProfile`.

### Indicadores ATU

Tres LED de estado indican el estado del ATU:

- **Success** — Se ilumina en verde cuando el estado del ATU es `Successful` o `OK`.
- **Byp** — Se ilumina en naranja cuando el ATU está en `Bypass` o `ManualBypass`.
- **Mem** — Se ilumina en verde cuando el ATU está usando una memoria.

### Botón TUNE

- Inicia o detiene una portadora de sintonía. La etiqueta del botón cambia a "TUNING..." con fondo rojo mientras está activo.
- **Clic derecho** para abrir un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:
  - **Mono Tone** — Portadora tradicional de un solo tono.
  - **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación.
  
  La selección es transitoria de un solo uso: se aplica solo a la siguiente pulsación de TUNE y no se guarda en AppSettings. El `tune_mode` del equipo vuelve a `single_tone` tras los ciclos de encendido.

### Botón MOX

- Activa/desactiva la transmisión manual. El botón se vuelve rojo mientras TX está activado.
- Cuando los tonos Quindar están habilitados en la tira de canales de audio, los tonos K y BK suenan al activar y desactivar en modos de teléfono.

### Botón ATU

- Inicia el ciclo de sintonía del ATU interno.
- **Deshabilitado** cuando TGXL está en modo OPERATE.
- **Clic derecho** para abrir un menú contextual con dos opciones:
  - **Pre-tune bands…** — Abre un diálogo para ejecutar el barrido de presintonía del ATU en las bandas seleccionadas por el usuario. Esta acción requiere que MEM esté habilitado primero; si MEM está desactivado, el elemento del menú aparece atenuado con una información sobre herramientas.
  - **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias del ATU del equipo.

### Botón MEM

- Activa/desactiva la recuperación de la memoria del ATU.
- **Deshabilitado** cuando TGXL está en modo OPERATE.

### Botón APD y grupo de estado

- **APD** — Botón de alternancia que habilita o deshabilita la Predistorsión Adaptativa en el equipo.
- Tres indicadores de estado muestran el estado del APD:
  - **Active** — Iluminado en verde cuando APD está activado y el ecualizador se aplica activamente.
  - **Cal** — Iluminado en verde cuando APD está activado y aún está calibrando.
  - **Avail** — Iluminado en verde cuando APD está activado y hay una calibración disponible pero aún no aplicada.
  
  La progresión típica es: Cal (calibrando) → Avail (listo) → Active (aplicado).

## Comportamiento de retención de pico

El medidor de potencia directa incluye una función de retención de pico que captura la PEP máxima (Potencia de Envolvente de Pico) durante una transmisión. La barra de retención de pico:

- Se actualiza instantáneamente cuando se detecta un nuevo pico.
- Mantiene el valor pico durante 2 segundos.
- Después del período de retención, disminuye hacia el nivel de potencia suavizado actual. La tasa de disminución se escala al rango completo del indicador (120 W o 600 W), por lo que la sensación visual (~2.5 segundos desde el pico hasta el mínimo) es consistente en ambas escalas.
- Se reinicia a cero inmediatamente cuando se desactiva el transmisor (MOX liberado o TUNE detenido). Esto evita que una lectura de PEP retenida persista entre transmisiones.

## Relacionado

- [Cancelar una transmisión activa o atascada con la insignia TX de la barra de estado](cancel-an-active-or-stuck-transmission-with-the-status-bar-tx-badge.md)
- [Activar MOX para poner manualmente el transmisor en transmisión](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
