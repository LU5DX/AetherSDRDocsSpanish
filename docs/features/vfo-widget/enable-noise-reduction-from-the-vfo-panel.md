# Panel de VFO

El Panel de VFO es un panel de control flotante por slice, anclado al marcador de VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes más usados por slice — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Puede colapsarse a una tira compacta que solo muestra la frecuencia.

## Cómo abrir el Panel de VFO

1. Haga clic en la bandera del marcador de VFO en la pantalla del espectro del slice que desea ajustar. El panel de VFO se abre anclado al marcador.
2. El panel se abre en su estado expandido. Si está colapsado como una tira de solo frecuencia, haga clic en cualquier parte para expandirlo.

## Controles

El Panel de VFO está organizado en pestañas. Cada pestaña contiene controles relacionados.

### Controles generales

Estos controles aparecen en el área principal del Panel de VFO, encima de las pestañas.

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botón de antena RX** | N/A | Abre el menú de selección de antena para la antena receptora de este slice. |
| **Botón de antena TX** | N/A | Abre el menú de selección de antena para la antena transmisora de este slice. |
| **Indicador de frecuencia** | N/A | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | N/A | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Botón de grosor del marcador** | 1 px | Cambia la línea del marcador de VFO entre Apagado, 1 px y 3 px. Se conserva por slice (`Slice{N}_MarkerWidth`). |
| **Botón de bordes de filtro** | mostrado | Alterna la visualización de las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice (`Slice{N}_FilterEdgesHidden`). |
| **Alternar colapso** | expandido | Colapsa el panel de VFO a una tira compacta de solo frecuencia. Se conserva por slice (`SliceFlagCollapsed_{N}`). |

### Barra de pestañas

Las etiquetas de la barra de pestañas ahora se implementan como widgets `QPushButton` seleccionables en lugar de elementos `QLabel`. Cada botón de pestaña admite foco de teclado y eventos de accesibilidad.

Al hacer clic derecho en la pestaña de audio, se alterna la salida de audio del slice directamente.

### Pestaña de Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Deslizador de ganancia AF** | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se conserva — refleja el estado en vivo de la radio. |
| **Deslizador de paneo** | 50 | 0–100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura para indicar la posición neutra. |
| **Botón de silencio** | apagado | — | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. |
| **Botón + deslizador de Squelch** | apagado | 0–100 | Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| **Combo AGC** | RÁPIDO | RÁPIDO / MED / LENTO / APAGADO | Establece la velocidad de ataque/liberación del AGC para este slice. |

### Pestaña DSP

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | apagado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de radio y la compilación. |
| **Botón ADSP** | N/A | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Estilizado como un conmutador DSP del lado de la radio pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| **Botón AetherVoice** | N/A | Alterna la Tira de Canales de Audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada del menú / cadena existentes para la tira. |

**Deslizador de nivel DSP:** Cuando uno o más algoritmos DSP con nivel están activos, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta del deslizador muestra qué algoritmo está apuntando actualmente — se reasigna automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador. El deslizador siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN, o APF está encendido), la fila del deslizador se atenúa y no responde a la entrada.

Algoritmos que exponen el deslizador de nivel: NR, NRL, NRS, NRF.

### Pestaña Mode

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de modo** | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY | Establece el modo de demodulación para este slice. |
| **Botones de preajuste de filtro** | N/A | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botones + etiquetas RIT / XIT** | apagado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del mouse ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de canal DAX** | Apagado | Apagado / 1–8 | Asigna un canal de audio DAX a este slice. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|--------|-------------|
| **Distintivo TX** | TX (rojo) / oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **Distintivo SPLIT** | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. |

## Entrada de frecuencia

La pantalla de frecuencia admite varios formatos de entrada:

- Formato MHz: `14.225`, `14.225.000`, `14225`, `14225.0`
- Formato kHz (solo HF): `14225` (interpreta enteros simples como kHz cuando están por debajo de 54000)
- Formato Hz (solo HF): `14225000` (interpreta como Hz cuando está por encima de 54000)
- Entrada explícita en MHz: cualquier entrada con un punto se trata como MHz. Si el valor supera los 54 MHz, se acepta como frecuencia VHF/UHF incluso sin una antena XVTR.

En bandas XVTR, los enteros simples como `145` se tratan como MHz (conveniencia de banda de 3 dígitos).

## Edición de frecuencia

El campo de edición de frecuencia ahora utiliza una subclase `FreqLineEdit` con un texto de sugerencia ("MHz (ej. 14.225)") en lugar del texto de marcador estándar de `QLineEdit`. Esto proporciona una experiencia de usuario consistente en todas las plataformas.

## Accesibilidad

El Panel de VFO incluye soporte de accesibilidad a través de eventos `QAccessible`. Cuando el valor de la frecuencia cambia, se emite un evento de cambio de valor accesible para notificar a las tecnologías de asistencia. Un temporizador dedicado asegura que las actualizaciones duplicadas o rápidas se fusionen, evitando ruido innecesario de eventos.

## Comportamiento de la rueda del mouse

El Panel de VFO respeta la configuración **Reverse mouse wheel** de `InteractionSettings`. Cuando está habilitada, desplazar la rueda del mouse en la dirección opuesta cambia la frecuencia en consecuencia (ver #3302).

## Notas sobre el squelch

El squelch está deshabilitado (el botón y el deslizador no funcionan) cuando el slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

Si el squelch estaba activo al cambiar a uno de estos modos, se desactiva automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Notas sobre el bloqueo de VFO

Cuando un slice está bloqueado:
- El botón de bloqueo muestra un icono de candado. Al hacer clic nuevamente se desbloquea el slice.
- Desplazarse sobre el panel de VFO colapsado o la pantalla de frecuencia muestra una superposición de BLOQUEADO y bloquea los cambios de frecuencia. El evento de desplazamiento se consume pero la frecuencia no cambia.
- La entrada directa de frecuencia se cancela si se inicia mientras el slice está bloqueado.
- Desbloquear el slice elimina la superposición de BLOQUEADO.

## Soporte de temas (v26.6.1)

El Panel de VFO ahora utiliza el sistema de temas para su estilo visual:

- **Ámbito del contenedor:** El panel reside bajo el ámbito del contenedor de tema `spectrum/vfo`, por lo que sus fichas de color heredan de las anulaciones de la pantalla del espectro pero se pueden personalizar de forma independiente.
- **Cobertura del inspector:** Las siguientes fichas se declaran para inspección: al hacer clic en la bandera de VFO, el distintivo de llamada o la tira del medidor de señal en el modo Inspeccionar, estas fichas aparecerán en la lista de resultados:
  - `color.background.0`
  - `color.background.1`
  - `color.background.2`
  - `color.text.primary`
  - `color.text.label`
  - `color.accent`
  - `color.accent.bright`
- **Deslizador de paneo:** El deslizador de paneo utiliza un relleno anclado al centro que se pinta desde el centro hacia afuera en el color de acento. El relleno de la ranura en el lado opuesto del control utiliza el color de fondo. Esto coincide con el comportamiento visual de los controles de balance L/R. Un punto de marca central en la posición neutra ayuda al operador a ver el punto medio.
- **Estilo de botones mini:** Los botones mini (antena) utilizan colores del tema a través de las fichas `{{color.background.1}}` y `{{color.accent}}` en lugar de valores hexadecimales codificados.
- **Contraste del distintivo SPLIT:** El color del texto del distintivo SPLIT se ha ajustado para mejorar la legibilidad: el estado normal es `rgba(255,255,255,120)`, el estado al pasar el mouse es `rgba(255,255,255,180)`.

## Consejos

- Varios botones de reducción de ruido pueden estar activos al mismo tiempo.
- Puede abrir el applet de AetherDSP desde `Settings > AetherDSP Settings...` para configurar algoritmos de reducción de ruido del lado del cliente.
- Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.
- Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio del slice directamente.

## Relacionados

- [Descripción general del Panel de VFO](overview.md)
- [Activar squelch desde el panel de VFO](enable-squelch-from-the-vfo-panel.md)
