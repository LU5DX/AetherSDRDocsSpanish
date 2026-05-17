# Ajustar la ganancia de AF y la posición del paneo desde el panel del VFO

Use la pestaña Audio en el panel del VFO para establecer el nivel de salida de audio y la posición estéreo de paneo para cualquier slice de recepción de forma independiente de otros slices.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel del VFO requiere una conexión activa con el radio.
- El panel del VFO para el slice objetivo debe estar abierto. Si está colapsado en una tira solo de frecuencia, haga clic en cualquier parte de la tira colapsada para expandirlo.

## Pasos

1. Haga clic en la bandera del marcador del VFO en la visualización del espectro para el slice que desea ajustar. El panel del VFO se abre anclado al marcador.
2. Haga clic en la pestaña **Audio** dentro del panel del VFO.
3. Para establecer el nivel de salida de audio, arrastre el **deslizador de ganancia de AF** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el **deslizador de paneo** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 mueve el audio hacia el canal izquierdo; superior a 50 hacia el derecho.

## Función de cada control

| Control | Valor predeterminado | Rango |
|---|---|---|
| Deslizador de ganancia de AF (pestaña Audio) | 100 | 0–100 |
| Deslizador de paneo (pestaña Audio) | 50 | 0–100 |
| Botón de silencio (pestaña Audio) | desactivado | — |
| Botón y deslizador de squelch (pestaña Audio) | desactivado | 0–100 |
| Combo AGC (pestaña Audio) | FAST | FAST \| MED \| SLOW \| OFF |
| Botón ADSP (pestaña DSP) | Abre el cuadro de diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú de configuración (v0.9.8). | Diseñado como un conmutador de DSP del lado del radio, pero no es seleccionable. Al hacer clic, abre y enfoca el cuadro de diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Activa o desactiva la tira de canal de audio Aetherial: el conjunto unificado de DSP de TX/RX (v0.9.8). | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |
| Botón de antena RX | — | Abre el menú de selección de antena para la antena de recepción de este slice. |
| Botón de antena TX | — | Abre el menú de selección de antena para la antena de transmisión de este slice. |
| Visualización de frecuencia | — | Muestra la frecuencia actual del slice. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Entrar o Tabulador. |
| Etiqueta de ancho de filtro | — | Muestra el ancho de banda del filtro actual. Haga clic para recorrer cíclicamente los botones de ajuste preestablecido del filtro en la pestaña Modo. |
| Combo de modo (pestaña Modo) | USB | USB \| LSB \| CW \| CWL \| AM \| SAM \| DIGU \| DIGL \| FM \| NFM \| DFM \| RTTY |
| Botones de ajuste preestablecido de filtro (pestaña Modo) | — | Aplica un ajuste preestablecido de ancho de filtro guardado. Haga clic derecho para guardar el ancho de filtro actual en esa ranura. |
| Botones y etiquetas RIT / XIT (pestaña X/RIT) | desactivado | Habilita la sintonización incremental del receptor (RIT) o del transmisor (XIT). |
| Combo de canal DAX (pestaña DAX) | Desactivado | Desactivado \| 1–8 |
| Botón de grosor del marcador | 1 píxel | Desactivado \| 1 píxel \| 3 píxeles |
| Botón de bordes del filtro | mostrado | Activa o desactiva las líneas de borde del filtro en la banda pasante del espectro. |
| Conmutador de colapso | expandido | Colapsa el panel del VFO a una tira compacta solo de frecuencia. |
| Insignia del slice | — | Muestra la letra del slice. Muestra la insignia de TX (roja) cuando este slice es el slice de transmisión activo. Muestra la insignia SPLIT (ámbar) cuando la TX está asignada a un slice diferente al slice de recepción activo. |

## Consejos

- Al hacer doble clic en cualquiera de los deslizadores, se restablece a su valor predeterminado: 100 para ganancia de AF, 50 para paneo.
- La ganancia de AF es por slice. Ajustar un slice no afecta a ningún otro slice.
- Para silenciar un slice sin mover el deslizador de ganancia de AF, use el **botón de silencio** en la pestaña Audio en su lugar. Silenciar no cambia el valor de ganancia almacenado.

## Cambios en la etiqueta de ancho de filtro en v0.9.8

La etiqueta de ancho de filtro ahora usa `RxApplet::formatFilterWidth` como su única fuente de verdad. Esto corrige un desplazamiento de 0.1 kHz que afectaba anteriormente las lecturas de modo SSB y digital (#2197, v0.9.8). La etiqueta ahora se mantiene sincronizada con la lectura del filtro en el applet RX.

## Comportamiento del squelch para modo RTTY (v26.5.1)

El botón y el deslizador de squelch ahora están deshabilitados en modo RTTY, además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles cuando el audio alimenta decodificadores externos a través de DAX (#2504).

## Cambios en la pestaña DSP en v0.9.7

La pestaña DSP en el panel del VFO ahora muestra solo los algoritmos de reducción de ruido proporcionados por el radio. Los algoritmos del lado del cliente que antes eran accesibles como botones en esta pestaña (NR2, RN2, NR4, MNR, BNR y DFNR) se han movido fuera del panel del VFO. Para habilitar esos algoritmos, use el menú de superposición del espectro o el applet AetherDSP.

Los botones que permanecen en la pestaña DSP son:

| Botón | Algoritmo |
|---|---|
| NR | Reducción de ruido |
| NB | Supresor de ruido |
| ANF | Filtro de muesca automático |
| APF | Filtro de énfasis de audio (solo modo CW) |
| NRL | Nivel de reducción de ruido |
| NRS | Sustracción espectral |
| RNN | Reducción de ruido RNN |
| NRF | Filtro de ruido espectral |
| ANFL | Filtro de muesca LMS |
| ANFT | Filtro de muesca FFT |

### Botón ADSP (v0.9.8)

La pestaña DSP ahora incluye un **botón ADSP** que abre el cuadro de diálogo de configuración de AetherDSP. Este botón proporciona el mismo punto de entrada que el menú de configuración. Está diseñado como un conmutador de DSP del lado del radio, pero no es seleccionable. Haga clic en él para abrir y enfocar el cuadro de diálogo no modal de configuración de AetherDSP.

### Botón AetherVoice (v0.9.8)

La pestaña DSP también incluye un **botón AetherVoice** que activa o desactiva la tira de canal de audio Aetherial: el conjunto unificado de DSP de TX/RX. Este botón ocupa 2 columnas en la cuadrícula de DSP de 4 columnas y coincide con los puntos de entrada existentes del menú y la cadena para la tira.

### Deslizador de nivel de DSP

Ahora aparece un deslizador de nivel compartido debajo de la cuadrícula de botones de DSP. El deslizador se reorienta automáticamente al algoritmo de DSP con nivel que se habilitó más recientemente. La etiqueta a la izquierda del deslizador muestra el nombre del algoritmo actualmente orientado, y el valor numérico se muestra a la derecha.

Cambio importante en v0.9.8: El deslizador de nivel de DSP ahora aparece correctamente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado del radio. Anteriormente, el deslizador faltaba hasta que se alternaba manualmente el algoritmo (#startup-slider). Esto afecta a NB, NR, ANF, NRL, NRS, NRF y ANFL.

La fila del deslizador permanece visible en todo momento. Cuando no hay ningún algoritmo con nivel activo, o cuando solo RNN, ANFT o APF está encendido, la fila del deslizador se atenúa y no responde a los clics.

| Control | Rango | Comportamiento |
|---|---|---|
| Deslizador de nivel de DSP | 0–100 | Establece el nivel para el algoritmo de DSP con nivel habilitado más recientemente. Se reorienta automáticamente al cambiar de algoritmo. Se oculta (atenuado) cuando no hay ningún algoritmo con nivel activo. |

## Selección de antena (v26.5.2.1)

Los botones de antena RX y antena TX abren menús contextuales que muestran los puertos de antena disponibles para el slice actual.

- El menú de antena RX muestra las antenas de la lista de antenas RX dedicadas del slice cuando están disponibles, recurriendo a la lista de antenas global.
- El menú de antena TX filtra automáticamente los puertos de antena solo de RX. Los puertos de antena que comienzan con "RX" se excluyen de la selección TX.
- Cada entrada del menú muestra el nombre de la antena. La antena seleccionada actualmente está marcada con una marca de verificación.

## Indicadores del panel del VFO

El panel del VFO incluye dos indicadores que aparecen cuando se cumplen ciertas condiciones:

- **Insignia TX (roja)**: Se muestra cuando este slice es el slice de transmisión activo.
- **Insignia SPLIT (ámbar)**: Se muestra cuando la TX está asignada a un slice diferente al slice de recepción activo.

La insignia del slice muestra la letra del slice y utiliza formato de texto enriquecido para una representación adecuada.

## Entrada de frecuencia para bandas XVTR (v26.5.2.1)

Al ingresar frecuencias en bandas XVTR (frecuencia del slice superior a 54 MHz o antena RX que comienza con "XVT"):

- La frecuencia máxima aceptada es 50000 MHz.
- Para slices en el rango de 100–999 MHz (bandas de 2m/70cm), los números enteros se formatean automáticamente con un decimal después del tercer dígito. Por ejemplo, al ingresar 1446 se convierte en 144.6, 14696 se convierte en 146.96 y 144600 se convierte en 144.600.
- Para bandas de microondas (23cm y superiores, 1000 MHz y más), los números enteros se tratan como el valor exacto en MHz. Por ejemplo, 1296 se convierte en 1296 MHz.

## Relacionado

- [Silenciar el audio de un slice desde el panel del VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Habilitar el squelch desde el panel del VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel del VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel del VFO](overview.md)
