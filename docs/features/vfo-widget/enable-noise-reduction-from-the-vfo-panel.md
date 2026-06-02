# Panel de VFO

El Panel de VFO es un panel de control flotante por slice anclado al marcador de VFO en la pantalla del espectro. Proporciona acceso rápido a los ajustes más utilizados por slice — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, squelch, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX — sin salir de la vista del espectro. Puede colapsarse a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel de VFO

1. Haga clic en la bandera del marcador de VFO en la pantalla del espectro del slice que desea ajustar. El panel de VFO se abre anclado al marcador.
2. El panel se abre en su estado expandido. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte para expandirlo.

## Controles

El Panel de VFO está organizado en pestañas. Cada pestaña contiene controles relacionados.

### Controles generales

Estos controles aparecen en el área principal del Panel de VFO, sobre las pestañas.

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botón de antena RX** | N/A | Abre el menú de selección de antena para la antena de recepción de este slice. |
| **Botón de antena TX** | N/A | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| **Visualización de frecuencia** | N/A | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | N/A | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como única fuente de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital (#2197, v0.9.8). |
| **Botón de grosor del marcador** | 1 px | Cambia la línea del marcador de VFO entre Off, 1 px y 3 px. Se conserva por slice (`Slice{N}_MarkerWidth`). |
| **Botón de bordes de filtro** | mostrado | Alterna las líneas de borde del filtro en la banda pasante del espectro. Se conserva por slice (`Slice{N}_FilterEdgesHidden`). |
| **Alternar colapso** | expandido | Colapsa el panel de VFO a una tira compacta de solo frecuencia. Se conserva por slice (`SliceFlagCollapsed_{N}`). |

### Pestaña Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Deslizador de ganancia AF** | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se conserva — refleja el estado en vivo de la radio. |
| **Deslizador de paneo** | 50 | 0–100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. El relleno del deslizador se ancla desde el centro hacia afuera, con un punto de marca central pintado en la ranura para indicar la posición neutra. |
| **Botón de silencio** | apagado | — | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. |
| **Botón + deslizador de Squelch** | apagado | 0–100 | Activa el squelch para este slice. El deslizador adyacente establece el umbral. |
| **Combo de AGC** | FAST | FAST / MED / SLOW / OFF | Establece la velocidad de ataque/liberación del AGC para este slice. |

### Pestaña DSP

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | apagado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad de los botones depende de la serie de radio y la compilación. |
| **Botón ADSP** | N/A | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Estilizado como un interruptor DSP del lado de la radio pero no marcable. Al hacer clic, abre y enfoca el diálogo modal de Configuración de AetherDSP. |
| **Botón AetherVoice** | N/A | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8). Abarca 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

**Deslizador de nivel DSP:** Cuando uno o más algoritmos DSP con nivel están activos, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta del deslizador muestra a qué algoritmo apunta actualmente — se reasigna automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador. El deslizador siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN o APF están encendidos), la fila del deslizador se atenúa y no responde a la entrada.

Algoritmos que exponen el deslizador de nivel: NR, NRL, NRS, NRF.

### Pestaña Mode

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de modo** | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY | Establece el modo de demodulación para este slice. |
| **Botones de preajuste de filtro** | N/A | N/A | Aplica un preajuste guardado de ancho de filtro. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se conserva en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botones + etiquetas RIT / XIT** | apagado | Activa la sintonización incremental del receptor (RIT) o del transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda de desplazamiento ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de canal DAX** | Off | Off / 1–8 | Asigna un canal de audio DAX a este slice. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|--------|---------|
| **Distintivo TX** | TX (rojo) / oculto | Se muestra cuando este slice es el slice de transmisión activo. |
| **Distintivo SPLIT** | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignado a un slice diferente al slice de recepción activo. |

## Ingreso de frecuencia

La pantalla de frecuencia admite varios formatos de ingreso:

- Formato MHz: `14.225`, `14.225.000`, `14225`, `14225.0`
- Formato kHz (solo HF): `14225` (interpreta enteros simples como kHz cuando están por debajo de 54000)
- Formato Hz (solo HF): `14225000` (interpreta como Hz cuando está por encima de 54000)
- Ingreso explícito de MHz: cualquier ingreso con un punto se trata como MHz. Si el valor supera los 54 MHz, se acepta como frecuencia VHF/UHF incluso sin una antena XVTR.

En bandas XVTR, los enteros simples como `145` se tratan como MHz (conveniencia para bandas de 3 dígitos).

## Notas sobre squelch

El squelch está deshabilitado (el botón y el deslizador se vuelven no funcionales) cuando el slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

Si el squelch estaba activo al cambiar a uno de estos modos, se desactiva automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Notas sobre el bloqueo de VFO

Cuando un slice está bloqueado:
- El botón de bloqueo muestra un icono de candado. Al hacer clic nuevamente, se desbloquea el slice.
- Al desplazarse sobre el panel de VFO colapsado o la pantalla de frecuencia, se muestra una superposición LOCKED y se bloquean los cambios de frecuencia. El evento de desplazamiento se consume pero la frecuencia no cambia.
- El ingreso directo de frecuencia se cancela si se inicia mientras el slice está bloqueado.
- Desbloquear el slice elimina la superposición LOCKED.

### Soporte de temas (v26.6.1)

El Panel de VFO ahora utiliza el sistema de temas para su estilo visual:

- **Ámbito del contenedor:** El panel reside bajo el ámbito del contenedor de tema `spectrum/vfo`, por lo que sus tokens de color heredan de las anulaciones de la pantalla del espectro pero pueden personalizarse de forma independiente.
- **Cobertura del inspector:** Los siguientes tokens se declaran para inspección: al hacer clic en la bandera de VFO, el distintivo de llamada o la tira del medidor de señal en el modo Inspect, estos tokens aparecerán en la lista de resultados:
  - `color.background.0`
  - `color.background.1`
  - `color.background.2`
  - `color.text.primary`
  - `color.text.label`
  - `color.accent`
  - `color.accent.bright`
- **Deslizador de paneo:** El deslizador de paneo utiliza un relleno anclado al centro que se pinta desde el centro hacia afuera en el color de acento. El relleno de la ranura en el lado opuesto del control usa el color de fondo. Esto coincide con el comportamiento visual de los controles de balance L/R. Un punto de marca central en la posición neutra ayuda al operador a ver el punto medio.
- **Estilo de botones mini:** Los botones mini (de antena) usan colores temáticos mediante los tokens `{{color.background.1}}` y `{{color.accent}}` en lugar de valores hexadecimales codificados.

## Consejos

- Múltiples botones de reducción de ruido pueden estar activos al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar algoritmos de reducción de ruido del lado del cliente.
- Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

## Relacionados

- [Descripción general del Panel de VFO](overview.md)
- [Activar squelch desde el panel de VFO](enable-squelch-from-the-vfo-panel.md)
