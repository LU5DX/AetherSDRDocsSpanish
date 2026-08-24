# Panel VFO

El Panel VFO es un panel de control flotante por slice anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por slice más utilizados (modo, presets de filtro, selección de antena, ganancia de AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX) sin salir de la vista del espectro. Puede contraerse hasta convertirse en una franja compacta de solo frecuencia.

## Apertura del Panel VFO

1. Haga clic en el marcador VFO de la pantalla del espectro correspondiente al slice que desea ajustar. El panel VFO se abre anclado al marcador.
2. El panel se abre en su estado expandido. Si está contraído a una franja de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Controles

El Panel VFO está organizado en pestañas. Cada pestaña contiene controles relacionados.

### Controles generales

Estos controles aparecen en el área principal del Panel VFO, sobre las pestañas.

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botón de antena RX** | N/D | Abre el menú de selección de antena para la antena receptora de este slice. |
| **Botón de antena TX** | N/D | Abre el menú de selección de antena para la antena transmisora de este slice. |
| **Pantalla de frecuencia** | N/D | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba los MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | N/D | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preset de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desfase de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| **Botón de grosor del marcador** | 1 px | Alterna la línea del marcador VFO entre Off, 1 px y 3 px. Se conserva por slice (`Slice{N}_MarkerWidth`). |
| **Botón de bordes del filtro** | visible | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice (`Slice{N}_FilterEdgesHidden`). |
| **Alternancia de contracción** | expandido | Contrae el panel VFO a una franja compacta de solo frecuencia. Se conserva por slice (`SliceFlagCollapsed_{N}`). |

### Barra de pestañas

Las etiquetas de la barra de pestañas ahora se implementan como widgets `QPushButton` marcables en lugar de elementos `QLabel`. Cada botón de pestaña admite el foco del teclado y eventos de accesibilidad.

Al hacer clic derecho en la pestaña de audio/altavoz, se alterna directamente el silencio de audio del slice.

### Pestaña Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Deslizador de ganancia AF** | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se conserva: refleja el estado en vivo de la radio. |
| **Deslizador de paneo** | 50 | 0–100 | Establece el paneo estéreo izquierda/derecha para este slice. 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura para indicar la posición neutra. |
| **Botón de silencio** | off | — | Silencia la salida de audio de este slice sin cambiar el ajuste de ganancia AF. |
| **Botón + deslizador de squelch** | off | 0–100 | Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| **Combo AGC** | FAST | FAST / MED / SLOW / OFF | Establece la velocidad de ataque/liberación del AGC para este slice. |

### Pestaña DSP

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF / MN** | off | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y de la compilación. El botón MN (filtro de muesca manual) se muestra solo en radios que declaran capacidad de filtro de muesca manual. |
| **Botón ADSP** | N/D | Abre el diálogo de Ajustes de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de un interruptor DSP del lado de la radio pero no es marcable. Al hacer clic, eleva y enfoca el diálogo no modal de Ajustes de AetherDSP. |
| **Botón AetherVoice** | N/D | Alterna la Tira de Canal de Audio Aetherial: la suite unificada de DSP TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

**Deslizador de nivel DSP:** Cuando uno o más algoritmos DSP con nivel están activos, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta del deslizador muestra a qué algoritmo apunta actualmente; se reorienta automáticamente al algoritmo con nivel activado más recientemente. El valor numérico se muestra a la derecha del deslizador. El deslizador siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN o APF están activados), la fila del deslizador se atenúa y no responde a la entrada.

Algoritmos que exponen el deslizador de nivel: NR, NRL, NRS, NRF, MN.

### Pestaña Mode

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de modo** | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY | Establece el modo de demodulación para este slice. |
| **Botones de preset de filtro** | N/D | N/D | Aplica un preset guardado de ancho de filtro. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botones + etiquetas RIT / XIT** | off | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desfase actual; la rueda del mouse ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de canal DAX** | Off | Off / 1–8 | Asigna un canal de audio DAX a este slice. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|--------|------------|
| **Insignia TX** | TX (roja) / oculta | Se muestra cuando este slice es el slice transmisor activo. |
| **Insignia SPLIT** | SPLIT (ámbar) / oculta | Se muestra cuando TX está asignado a un slice diferente del slice receptor activo. |

## Entrada de frecuencia

La pantalla de frecuencia admite varios formatos de entrada:

- Formato MHz: `14.225`, `14.225.000`, `14225`, `14225.0`
- Formato kHz (solo HF): `14225` (interpreta enteros simples como kHz cuando están por debajo de 54000)
- Formato Hz (solo HF): `14225000` (interpreta como Hz cuando está por encima de 54000)
- Entrada explícita en MHz: cualquier entrada con punto se trata como MHz. Si el valor supera 54 MHz, se acepta como frecuencia VHF/UHF incluso sin antena XVTR.

En bandas XVTR, los enteros simples como `145` se tratan como MHz (conveniencia de banda de 3 dígitos).

## Edición de frecuencia

El campo de edición de frecuencia ahora utiliza una subclase `FreqLineEdit` con un texto de sugerencia ("MHz (p. ej. 14.225)") en lugar del texto de sugerencia estándar de `QLineEdit`. Esto proporciona una experiencia de usuario coherente en todas las plataformas.

## Accesibilidad

El Panel VFO incluye soporte de accesibilidad mediante eventos `QAccessible`. Cuando cambia el valor de frecuencia, se emite un evento de cambio de valor accesible para notificar a las tecnologías de asistencia. Un temporizador dedicado garantiza que las actualizaciones duplicadas o rápidas se consoliden, evitando ruido innecesario de eventos.

## Comportamiento de la rueda del mouse

El Panel VFO respeta el ajuste **Reverse mouse wheel** de `InteractionSettings`. Cuando está habilitado, desplazar la rueda del mouse en la dirección opuesta cambia la frecuencia en consecuencia (ver #3302).

## Notas sobre squelch

El squelch se desactiva (el botón y el deslizador dejan de funcionar) cuando el slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

Si el squelch estaba activo al cambiar a uno de estos modos, se apaga automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Notas sobre el bloqueo VFO

Cuando un slice está bloqueado:
- El botón de bloqueo muestra un icono de candado. Hacer clic nuevamente desbloquea el slice.
- Desplazarse sobre el panel VFO contraído o la pantalla de frecuencia muestra una superposición LOCKED y bloquea los cambios de frecuencia. El evento de desplazamiento se consume pero la frecuencia no cambia.
- La entrada directa de frecuencia se cancela si se inicia mientras el slice está bloqueado.
- Desbloquear el slice elimina la superposición LOCKED.

## Soporte de temas (v26.6.1)

El Panel VFO ahora utiliza el sistema de temas para su estilo visual:

- **Ámbito del contenedor:** El panel reside bajo el ámbito de contenedor de tema `spectrum/vfo`, por lo que sus tokens de color heredan de las anulaciones de la pantalla del espectro, pero se pueden personalizar de forma independiente.
- **Cobertura del inspector:** Los siguientes tokens se declaran para inspección: al hacer clic en el marcador VFO, la insignia de indicativo o la tira del medidor de señal en modo Inspect, estos tokens aparecerán en la lista de resultados:
  - `color.background.0`
  - `color.background.1`
  - `color.background.2`
  - `color.text.primary`
  - `color.text.label`
  - `color.accent`
  - `color.accent.bright`
- **Deslizador de paneo:** El deslizador de paneo utiliza un relleno anclado al centro que se pinta desde el centro hacia afuera en el color de acento. El relleno de la ranura en el lado opuesto de la manija utiliza el color de fondo. Esto coincide con el comportamiento visual de los controles de balance L/R. Un punto de marca central en la posición neutra ayuda al operador a ver el punto medio.
- **Estilo de botones mini:** Los botones mini (antena) utilizan colores temáticos mediante tokens `{{color.background.1}}` y `{{color.accent}}` en lugar de valores hexadecimales codificados.
- **Contraste de la insignia SPLIT:** El color del texto de la insignia SPLIT se ha ajustado para mejorar la legibilidad: estado normal es `rgba(255,255,255,120)`, estado de desplazamiento es `rgba(255,255,255,180)`.

## Sombra de elevación (v26.7.4)

Una sombra de elevación ligera acelerada por hardware ahora se renderiza detrás del marcador VFO. La sombra la dibuja un widget dedicado `FlagShadow` que reside debajo del `VfoWidget` en el orden de apilamiento. Este diseño aísla la sombra de los repintados del medidor en vivo: el medidor puede actualizarse a la velocidad de animación sin obligar a que todo el marcador se vuelva a desenfocar.

La sombra utiliza un enfoque de altura-por-ancho de `SmartMtrWidget`: la altura de la tira VFO puede ser impulsada por una página que mantiene una relación de aspecto (p. ej. el S-meter). Las páginas sin altura-por-ancho (el espaciador S-meter predeterminado) no se ven afectadas.

## Controles de filtro adaptativo (v26.7.4)

Cuando un filtro adaptativo (p. ej. APF) u otro filtro dinámico similar está activo, aparece un widget `AdaptiveFilterControls` en el Panel VFO. Este widget proporciona deslizadores e indicadores de parámetros en tiempo real para el algoritmo de filtro adaptativo (p. ej. frecuencia central, ancho de banda, profundidad). Los controles aparecen solo cuando un algoritmo de filtro compatible está habilitado para el slice.

## Integración SmartMtr (v26.7.4)

El Panel VFO ahora se integra con `SmartMtrWidget` para mostrar datos del medidor de señal en tiempo real dentro del propio marcador VFO. Cuando el panel está en su estado expandido, una tira compacta de S-meter aparece debajo de la pantalla de frecuencia y sobre las pestañas, mostrando la intensidad de la señal, la actividad del AGC y otras indicaciones del medidor. La tira del medidor utiliza el mismo comportamiento de altura-por-ancho que el widget de sombra para mantener un tamaño coherente.

## Estabilidad de automatización (v26.8.4)

Los botones de alternancia DSP ahora llevan nombres de objeto estables (`dspNR`, `dspNR2`, `dspMN`, etc.) además de sus nombres accesibles. Esto garantiza que los scripts de automatización puedan dirigirse de manera confiable a estos controles incluso si las etiquetas legibles por humanos se reformulan en el futuro.

## Manejo de spots en panel contraído (v26.8.4)

Al hacer clic derecho en la etiqueta de frecuencia del panel VFO contraído, ahora se abre correctamente el menú contextual **Add Spot** para la propia frecuencia del VFO. Anteriormente, los clics se filtraban al widget del espectro subyacente, que informaba la frecuencia ajustada por pasos del cursor en lugar de la del VFO.

## Consejos

- Varios botones de reducción de ruido pueden estar activos al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar los algoritmos de reducción de ruido del lado del cliente.
- Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Ajustes de AetherDSP para ese algoritmo.
- Haga clic derecho en la etiqueta de la pestaña Audio para alternar el silencio del slice directamente.

## Relacionado

- [Descripción general del Panel VFO](overview.md)
- [Activar squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
