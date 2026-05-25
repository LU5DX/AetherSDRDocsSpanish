# Panel VFO

El Panel VFO es un panel de control flotante por slice, anclado al marcador VFO en la visualización del espectro. Proporciona acceso rápido a los ajustes más usados por slice — modo, preajustes de filtro, selección de antena, ganancia de AF, paneo, silenciador, AGC, RIT/XIT, botones de reducción de ruido DSP y asignación de DAX — sin salir de la vista del espectro. Puede colapsarse a una tira compacta que solo muestra la frecuencia.

## Abrir el Panel VFO

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el slice que desea ajustar. El Panel VFO se abre anclado al marcador.
2. El panel se abre en su estado expandido. Si está colapsado a una tira de solo frecuencia, haga clic en cualquier parte del mismo para expandirlo.

## Controles

El Panel VFO está organizado en pestañas. Cada pestaña contiene controles relacionados.

### Controles generales

Estos controles aparecen en el área principal del Panel VFO, sobre las pestañas.

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botón de antena RX** | N/A | Abre el menú de selección de antena para la antena receptora de este slice. |
| **Botón de antena TX** | N/A | Abre el menú de selección de antena para la antena transmisora de este slice. |
| **Visualización de frecuencia** | N/A | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. |
| **Etiqueta de ancho de filtro** | N/A | Muestra el ancho de banda del filtro actual. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Usa `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modos SSB/digitales (#2197, v0.9.8). |
| **Botón de grosor del marcador** | 1 px | Cambia la línea del marcador VFO entre Off, 1 px y 3 px. Se persiste por slice (`Slice{N}_MarkerWidth`). |
| **Botón de bordes de filtro** | mostrado | Alterna la visualización de las líneas de borde del filtro en la banda pasante del espectro. Se persiste por slice (`Slice{N}_FilterEdgesHidden`). |
| **Alternancia de colapso** | expandido | Colapsa el Panel VFO a una tira compacta de solo frecuencia. Se persiste por slice (`SliceFlagCollapsed_{N}`). |

### Pestaña Audio

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Deslizador de ganancia AF** | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se persiste — refleja el estado activo de la radio. |
| **Deslizador de paneo** | 50 | 0–100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. |
| **Botón de silencio** | apagado | — | Silencia la salida de audio para este slice sin cambiar el ajuste de ganancia AF. |
| **Botón + deslizador de silenciador** | apagado | 0–100 | Activa el silenciador para este slice. El deslizador adyacente establece el umbral. |
| **Combo AGC** | FAST | FAST / MED / SLOW / OFF | Establece la velocidad de ataque/liberación del AGC para este slice. |

### Pestaña DSP

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF** | apagado | Activa el algoritmo de reducción de ruido correspondiente para este slice. La disponibilidad del botón depende de la serie de radio y la compilación. |
| **Botón ADSP** | N/A | Abre el diálogo de Configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). Tiene el estilo de una activación DSP del lado de la radio, pero no es marcable. Al hacer clic, eleva y enfoca el diálogo no modal de Configuración de AetherDSP. |
| **Botón AetherVoice** | N/A | Activa la tira de canal de audio Aetherial — el conjunto DSP unificado de TX/RX (v0.9.8). Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada de menú/cadena existentes para la tira. |

**Deslizador de nivel DSP:** Cuando uno o más algoritmos DSP con nivel están activos, aparece un deslizador de nivel compartido debajo de la cuadrícula de botones. La etiqueta del deslizador muestra qué algoritmo está controlando actualmente; se reasigna automáticamente al algoritmo con nivel habilitado más recientemente. El valor numérico se muestra a la derecha del deslizador. El deslizador siempre está presente en el diseño. Cuando ningún algoritmo con nivel está activo (o solo RNN, o APF están encendidos), la fila del deslizador se atenúa y no responde a la entrada.

Algoritmos que exponen el deslizador de nivel: NR, NRL, NRS, NRF.

### Pestaña Mode

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de modo** | USB | USB / LSB / CW / CWL / AM / SAM / DIGU / DIGL / FM / NFM / DFM / RTTY | Establece el modo de demodulación para este slice. |
| **Botones de preajuste de filtro** | N/A | N/A | Aplica un preajuste de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. Se persiste en `FilterPresets`. Se pueden establecer bordes lo/hi personalizados por ranura mediante clic derecho. |

### Pestaña X/RIT

| Control | Predeterminado | Comportamiento |
|---------|---------|----------|
| **Botones + etiquetas RIT / XIT** | apagado | Activa la sintonización incremental del receptor (RIT) o transmisor (XIT). La etiqueta muestra el desplazamiento actual; la rueda del ratón ajusta en pasos de 10 Hz. |

### Pestaña DAX

| Control | Predeterminado | Rango válido | Comportamiento |
|---------|---------|-------------|----------|
| **Combo de canal DAX** | Off | Off / 1–8 | Asigna un canal de audio DAX a este slice. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|--------|---------|
| **Distintivo TX** | TX (rojo) / oculto | Se muestra cuando este slice es el slice transmisor activo. |
| **Distintivo SPLIT** | SPLIT (ámbar) / oculto | Se muestra cuando TX está asignado a un slice diferente al slice receptor activo. |

## Entrada de frecuencia

La visualización de frecuencia admite varios formatos de entrada:

- Formato MHz: `14.225`, `14.225.000`, `14225`, `14225.0`
- Formato kHz (solo HF): `14225` (interpreta números enteros simples como kHz cuando están por debajo de 54000)
- Formato Hz (solo HF): `14225000` (interpreta como Hz cuando está por encima de 54000)
- Entrada explícita en MHz: cualquier entrada con un punto se trata como MHz. Si el valor supera los 54 MHz, se acepta como frecuencia de VHF/UHF incluso sin una antena XVTR.

En bandas XVTR, los números enteros simples como `145` se tratan como MHz (conveniencia para banda de 3 dígitos).

## Notas sobre el silenciador

El silenciador se desactiva (el botón y el deslizador quedan no funcionales) cuando el slice está en los siguientes modos:
- Modos digitales (DIGU, DIGL)
- RTTY
- Modos CW (CW, CWL)

Si el silenciador estaba activo al cambiar a uno de estos modos, se apaga automáticamente. El estado guardado se restaura al volver a un modo compatible.

## Notas sobre el bloqueo de VFO

Cuando un slice está bloqueado:
- El botón de bloqueo muestra un icono de candado. Al hacer clic nuevamente, se desbloquea el slice.
- Desplazarse sobre el Panel VFO colapsado o la visualización de frecuencia muestra una superposición LOCKED y bloquea los cambios de frecuencia. El evento de desplazamiento se consume, pero la frecuencia no cambia.
- La entrada directa de frecuencia se cancela si se inicia mientras el slice está bloqueado.
- Desbloquear el slice elimina la superposición LOCKED.

## Consejos

- Varios botones de reducción de ruido pueden estar activos al mismo tiempo.
- Puede abrir el applet AetherDSP desde `Settings > AetherDSP Settings...` para configurar algoritmos de reducción de ruido del lado del cliente.
- Haga clic derecho en NR2, NR4, MNR o DFNR para abrir el diálogo de Configuración de AetherDSP para ese algoritmo.

## Relacionados

- [Descripción general del Panel VFO](overview.md)
- [Activar el silenciador desde el Panel VFO](enable-squelch-from-the-vfo-panel.md)
