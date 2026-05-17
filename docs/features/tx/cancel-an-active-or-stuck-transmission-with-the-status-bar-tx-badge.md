# Cancelar una transmisión activa o bloqueada con la insignia TX de la barra de estado

La insignia TX de la barra de estado le proporciona un solo clic para sacar al transmisor del estado TX, útil cuando MOX está bloqueado, una portadora de sintonía sigue activa o cualquier otra condición ha dejado la radio con la transmisión activada y el applet Controles de TX no está a la mano.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La insignia TX solo aparece en la barra de estado cuando hay una conexión activa con la radio.
- La radio debe encontrarse actualmente en estado de transmisión (MOX activado o portadora de sintonía activa) para que la insignia sea funcional.

## Pasos

1. Localice la insignia TX en la barra de estado de AetherSDR, en la parte inferior de la ventana principal. La insignia es visible y está iluminada cuando la radio está transmitiendo.
2. Haga clic una vez en la insignia TX.
3. Confirme que la radio ha vuelto a recepción: el indicador de Potencia RF en el applet Controles de TX baja a cero, el botón MOX vuelve a su estado apagado (azul) y la etiqueta del botón TUNE vuelve a mostrar "TUNE" si había una portadora de sintonía activa.

## Consejos

- Si el applet Controles de TX está visible, también puede hacer clic en MOX para desactivar la transmisión, o hacer clic en TUNE para detener una portadora de sintonía activa (el botón muestra "TUNING..." mientras está activo). La insignia TX de la barra de estado es la ruta más rápida cuando el applet está colapsado o fuera de la vista.
- Si MOX fue activado mediante un comando externo CAT o TCI, al hacer clic en la insignia TX se envía el mismo comando de desactivación. La fuente original de la activación PTT no importa.

## Solución de problemas

- **Hacer clic en la insignia TX no detiene la transmisión** — Es posible que la radio esté activada por PTT de hardware (pedal o línea PTT del micrófono). Suelte primero el PTT de hardware; los comandos de software no pueden anular una línea PTT de hardware sostenida.
- **La insignia TX no es visible durante la transmisión** — La barra de estado puede estar oculta. Verifique que la ventana principal no esté en Modo Mínimo (`View > Minimal Mode`). Desactivar el Modo Mínimo restaura la barra de estado.

## Relacionados

- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Resumen de Controles de TX](overview.md)

***

# Resumen de Controles de TX

El applet Controles de TX proporciona la interfaz principal para las operaciones de transmisión: medidores de potencia directa y ROE, controles deslizantes de potencia RF y potencia de sintonía, un selector de perfil de TX y botones para TUNE, MOX, ATU, MEM y APD (Predistorsión Adaptativa).

## Antes de comenzar

- AetherSDR debe estar conectado a un FlexRadio FLEX-8600 con firmware 4.2 o posterior.
- La radio debe estar en un estado operativo (no en espera ni fuera de línea).

## Controles

### Potencia RF (Medidor de Potencia Directa)

- Muestra la potencia directa a la salida del excitador en vatios.
- La escala cambia según el modelo de radio: 0–120 W (sin amplificador) o 0–600 W (con amplificador Aurora 500W).
- La zona roja indica >100 W (sin amplificador) o >500 W (con amplificador).
- El medidor incluye una **barra de retención de pico** que captura el valor máximo de PEP durante la transmisión. El pico se mantiene durante 2 segundos y luego decae hacia el nivel de potencia actual en aproximadamente 2.5 segundos desde el pico hasta el mínimo. El pico se restablece a cero inmediatamente cuando se desactiva el transmisor.

### ROE (Medidor de Relación de Ondas Estacionarias)

- Muestra la ROE a la salida del excitador.
- Rango 1.0–3.0, con zona roja que indica >2.5.

### Control Deslizante de Potencia RF

- Establece el nivel de potencia de transmisión RF como un porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setRfPower` cuando se ajusta.

### Control Deslizante de Potencia de Sintonía

- Establece el nivel de potencia de la portadora de sintonía como un porcentaje (0–100), que se asigna a vatios según la escala de potencia de la radio.
- Llama a `TransmitModel::setTunePower` cuando se ajusta.

### Cuadro Combinado de Perfil TX

- Selecciona un perfil de transmisión de la lista proporcionada por la radio (`profileList()`).
- Cambiar el perfil llama a `TransmitModel::loadProfile`.

### Indicadores ATU

Tres LED de estado indican el estado del ATU:

- **Success** — Se ilumina en verde cuando el estado del ATU es `Successful` o `OK`.
- **Byp** — Se ilumina en naranja cuando el ATU está en `Bypass` o `ManualBypass`.
- **Mem** — Se ilumina en verde cuando el ATU está usando una memoria.

### Botón TUNE

- Inicia o detiene una portadora de sintonía. La etiqueta del botón cambia a "TUNING..." con fondo rojo mientras está activo.
- **Clic derecho** para abrir un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía:
  - **Mono Tone** — Portadora de tono único tradicional.
  - **Two Tone** — Portadora de dos tonos para pruebas de distorsión por intermodulación.
  
  La selección es transitoria y de un solo uso: se aplica solo a la siguiente pulsación de TUNE y no se conserva en AppSettings. El `tune_mode` de la radio vuelve a `single_tone` tras los ciclos de encendido.

### Botón MOX

- Alterna la transmisión manual encendida/apagada. El botón se vuelve rojo mientras TX está activado.
- Cuando los tonos Quindar están habilitados en la Tira de Canales de Audio, los tonos K y BK se reproducen al activar y desactivar en modos de telefonía.

### Botón ATU

- Inicia el ciclo de sintonía del ATU interno.
- **Deshabilitado** cuando TGXL está en modo OPERATE.
- **Clic derecho** para abrir un menú contextual con dos opciones:
  - **Pre-tune bands…** — Abre un diálogo para ejecutar el barrido de presintonía del ATU en las bandas seleccionadas por el usuario. Esta acción requiere que MEM esté habilitado primero; si MEM está desactivado, el elemento del menú aparece atenuado con una descripción emergente.
  - **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias del ATU de la radio.

### Botón MEM

- Alterna la recuperación de memoria del ATU encendida/apagada.
- **Deshabilitado** cuando TGXL está en modo OPERATE.

### Botón APD y Grupo de Estado

- **APD** — Botón de alternancia que habilita o deshabilita la Predistorsión Adaptativa en la radio.
- Tres indicadores de estado muestran el estado de APD:
  - **Active** — Iluminado en verde cuando APD está activado y el ecualizador se aplica activamente.
  - **Cal** — Iluminado en verde cuando APD está activado y aún está calibrando.
  - **Avail** — Iluminado en verde cuando APD está activado y hay una calibración disponible pero aún no se ha aplicado.
  
  La progresión típica es: Cal (calibrando) → Avail (listo) → Active (aplicado).

## Comportamiento de Retención de Pico

El medidor de potencia directa incluye una función de retención de pico que captura la potencia PEP máxima durante una transmisión. La barra de retención de pico:

- Se actualiza instantáneamente cuando se detecta un nuevo pico.
- Mantiene el valor pico durante 2 segundos.
- Después del período de retención, decae hacia el nivel de potencia suavizado actual. La tasa de decaimiento se escala al rango completo del indicador (120 W o 600 W), por lo que la sensación visual (~2.5 segundos desde el pico hasta el mínimo) es consistente en ambas escalas.
- Se restablece a cero inmediatamente cuando se desactiva el transmisor (MOX liberado o TUNE detenido). Esto evita que un valor PEP retenido persista entre transmisiones.

## Relacionados

- [Cancelar una transmisión activa o bloqueada con la insignia TX de la barra de estado](cancel-an-active-or-stuck-transmission-with-the-status-bar-tx-badge.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
