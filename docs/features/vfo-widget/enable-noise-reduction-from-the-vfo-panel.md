# Panel VFO

El Panel VFO es un panel de control flotante por segmento anclado al marcador VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes por segmento más utilizados — modo, preajustes de filtro, selección de antena, ganancia AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación DAX — sin salir de la vista del espectro. Puede colapsarse a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. Haga clic en la bandera del marcador VFO en la pantalla del espectro para el segmento que desea ajustar. El panel VFO se abre anclado al marcador.
2. El panel se abre en su estado expandido. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Controles

El Panel VFO está organizado en pestañas. Cada pestaña contiene controles relacionados.

### Controles generales

Estos controles aparecen en el área principal del Panel VFO, sobre las pestañas.

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| **Botón de antena RX** | N/A | Abre el menú de selección de antena para la antena receptora de este segmento. |
| **Botón de antena TX** | N/A | Abre el menú de selección de antena para la antena transmisora de este segmento. |
| **Visualización de frecuencia** | N/A | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | N/A | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Modo. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0,1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Botón de grosor del marcador** | 1 px | Cambia la línea del marcador VFO entre Apagado, 1 px y 3 px. Se conserva por segmento (`Slice{N}_MarkerWidth`). |
| **Botón de bordes del filtro** | mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por segmento (`Slice{N}_FilterEdgesHidden`). |
| **Alternancia de colapso** | expandido | Colapsa el panel VFO a una tira compacta de solo frecuencia. Se conserva por segmento (`SliceFlagCollapsed_{N}`). |

### Barra de pestañas

Las etiquetas de la barra de pestañas ahora están implementadas como widgets `QPushButton` seleccionables en lugar de elementos `QLabel`. Cada botón de pestaña admite el foco del teclado y eventos de accesibilidad.

Cuando se hace clic derecho en la pestaña de audio/altavoz, el silencio de audio del segmento se activa directamente.

### Pestaña de Audio

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| **Deslizador de ganancia AF** | 100 | 0–100 | Establece el nivel de salida de audio para este segmento. No se conserva — refleja el estado en vivo de la radio. |
| **Deslizador de paneo** | 50 | 0–100 | Establece el paneo estéreo izquierdo/derecho para este segmento. 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura para indicar la posición neutra. |
| **Botón de silencio** | apagado | — | Silencia la salida de audio para este segmento sin cambiar la configuración de ganancia AF. |
| **Botón + deslizador de silenciador** | apagado | 0–100 | Activa el silenciador para este segmento. El deslizador adyacente establece el umbral. |
| **Combo AGC** | RÁPIDO | RÁPIDO / MED / LENTO / APAGADO | Establece la velocidad de ataque/liberación del AGC para este segmento. |

### Pestaña DSP

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | apagado | Activa el algoritmo de reducción de ruido correspondiente para este segmento. La disponibilidad del botón depende de la serie de radio y la compilación. |
| **Botón ADSP** | N/A | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). El mismo punto de entrada que el menú de Configuración (v0.9.8). Con estilo como un botón de activación DSP del lado de la radio, pero no seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de Configuración de AetherDSP. |
| **Botón AetherVoice** | N/A | Activa la tira de Canal de Audio Aetherial — el conjunto unificado de DSP TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

**Deslizador de nivel DSP:** Cuando uno o más algoritmos DSP con nivel están activos, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta del deslizador muestra qué algoritmo está apuntando actualmente — se reorienta automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador. El deslizador siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN o APF están encendidos), la fila del deslizador se atenúa y no responde a la entrada.

Algoritmos que exponen el deslizador de nivel: NR, NRL, NRS, NRF.

### Pestaña Modo

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| **Combo Modo** | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY | Establece el modo de demodulación para este segmento. |
| **Botones de preajuste de filtro** | N/A | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Valor predeterminado | Comportamiento |
|---------|----------------------|----------------|
| **Botones RIT / XIT + etiquetas** | apagado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|----------------------|--------------|----------------|
| **Combo de canal DAX** | Apagado | Apagado / 1–8 | Asigna un canal de audio DAX a este segmento. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| **Insignia TX** | TX (rojo) / oculto | Se muestra cuando este segmento es el segmento de transmisión activo. |
| **Insignia SPLIT** | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignado a un segmento diferente al segmento receptor activo. |

## Entrada de frecuencia

La visualización de frecuencia admite varios formatos de entrada:

- Formato MHz: `14.225`, `14.225.000`, `14225`, `14225.0`
- Formato kHz (solo HF): `14225` (interpreta números enteros simples como kHz si están por debajo de 54000)
- Formato Hz (solo HF): `14225000` (interpreta como Hz si está por encima de 54000)
- Entrada explícita en MHz: cualquier entrada con un punto se trata como MHz. Si el valor supera los 54 MHz, se acepta como frecuencia VHF/UHF incluso sin una antena XVTR.

En bandas XVTR, los números enteros simples como `145` se tratan como MHz (conveniencia de banda de 3 dígitos).

## Edición de frecuencia

El campo de edición de frecuencia ahora utiliza una subclase `FreqLineEdit` con un texto de sugerencia de marcador de posición ("MHz (ej. 14.225)") en lugar del texto de marcador de posición estándar de `QLineEdit`. Esto proporciona una experiencia de usuario consistente en todas las plataformas.

## Accesibilidad

El Panel VFO incluye soporte de accesibilidad a través de eventos `QAccessible`. Cuando el valor de la frecuencia cambia, se emite un evento de cambio de valor accesible para notificar a las tecnologías de asistencia. Un temporizador dedicado asegura que las actualizaciones duplicadas o rápidas se fusionen, evitando ruido de eventos innecesario.

## Comportamiento de la rueda de desplazamiento

El Panel VFO respeta la configuración **Invertir rueda del ratón** de `InteractionSettings`. Cuando está habilitada, al desplazar la rueda del ratón en la dirección opuesta se cambia la frecuencia en consecuencia (ver #3302).

## Notas sobre el silenciador

El silenciador está deshabilitado (el botón y el deslizador no funcionan) cuando el segmento está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

Si el silenciador estaba activo al cambiar a uno de estos modos, se desactiva automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Notas sobre el bloqueo VFO

Cuando un segmento está bloqueado:
- El botón de bloqueo muestra un icono de candado. Al hacer clic nuevamente se desbloquea el segmento.
- Al desplazarse sobre el panel VFO colapsado o la visualización de frecuencia, se muestra una superposición BLOQUEADO y se bloquean los cambios de frecuencia. El evento de desplazamiento se consume pero la frecuencia no cambia.
- La entrada directa de frecuencia se cancela si se inicia mientras el segmento está bloqueado.
- Desbloquear el segmento elimina la superposición BLOQUEADO.

## Soporte de temas (v26.6.1)

El Panel VFO ahora utiliza el sistema de temas para su estilo visual:

- **Ámbito del contenedor:** El panel reside bajo el ámbito del contenedor de tema `spectrum/vfo`, por lo que sus tokens de color heredan de las anulaciones de la pantalla del espectro, pero pueden personalizarse de forma independiente.
- **Cobertura del inspector:** Los siguientes tokens están declarados para inspección — al hacer clic en la bandera VFO, la insignia de indicativo o la tira del medidor de señal en modo Inspeccionar, estos tokens aparecerán en la lista de aciertos:
  - `color.background.0`
  - `color.background.1`
  - `color.background.2`
  - `color.text.primary`
  - `color.text.label`
  - `color.accent`
  - `color.accent.bright`
- **Deslizador de paneo:** El deslizador de paneo utiliza un relleno anclado al centro que se pinta desde el centro hacia afuera en el color de acento. El relleno de la ranura en el lado opuesto del controlador utiliza el color de fondo. Esto coincide con el comportamiento visual de los controles de balance L/R. Un punto de marca central en la posición neutra ayuda al operador a ver el punto medio.
- **Estilo de botón mini:** Los botones mini (antena) utilizan colores temáticos mediante los tokens `{{color.background.1}}` y `{{color.accent}}` en lugar de valores hexadecimales fijos.
- **Contraste de la insignia SPLIT:** El color del texto de la insignia SPLIT se ha ajustado para mejorar la legibilidad — el estado normal es `rgba(255,255,255,120)`, el estado al pasar el ratón es `rgba(255,255,255,180)`.

## Sombra de elevación (v26.7.4)

Una sombra de elevación ligera acelerada por hardware se renderiza ahora detrás de la bandera VFO. La sombra es dibujada por un widget `FlagShadow` dedicado que reside debajo del `VfoWidget` en el orden de apilamiento. Este diseño aísla la sombra de las repintadas en vivo del medidor — el medidor puede actualizarse a la velocidad de animación sin forzar que toda la bandera se vuelva a desenfocar.

La sombra utiliza un enfoque de altura-por-ancho de `SmartMtrWidget`: la altura de la tira VFO puede ser impulsada por una página que mantiene una relación de aspecto (por ejemplo, el medidor S). Las páginas sin altura-por-ancho (el espaciador del medidor S predeterminado) no se ven afectadas.

## Controles de filtro adaptativo (v26.7.4)

Cuando un filtro adaptativo (por ejemplo, APF) o un filtro similarmente dinámico está activo, aparece un widget `AdaptiveFilterControls` en el Panel VFO. Este widget proporciona deslizadores de parámetros e indicadores en tiempo real para el algoritmo de filtro adaptativo (por ejemplo, frecuencia central, ancho de banda, profundidad). Los controles aparecen solo cuando un algoritmo de filtro compatible está habilitado para el segmento.

## Integración SmartMtr (v26.7.4)

El Panel VFO ahora se integra con `SmartMtrWidget` para mostrar datos del medidor de señal en tiempo real dentro de la propia bandera VFO. Cuando el panel está en su estado expandido, una tira compacta de medidor S aparece debajo de la visualización de frecuencia y sobre las pestañas, mostrando la intensidad de la señal, la actividad del AGC y otras indicaciones del medidor. La tira del medidor utiliza el mismo comportamiento de altura-por-ancho que el widget de sombra para mantener un tamaño consistente.

## Consejos

- Se pueden activar varios botones de reducción de ruido al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar algoritmos de reducción de ruido del lado del cliente.
- Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.
- Haga clic derecho en la etiqueta de la pestaña Audio para activar el silencio del segmento directamente.

## Relacionado

- [VFO Panel overview](overview.md)
- [Enable squelch from the VFO panel](enable-squelch-from-the-vfo-panel.md)
