# Cambiar el grosor de la línea del marcador de VFO

Use el botón de grosor del marcador para controlar qué tan prominente aparece la línea del marcador de VFO en la pantalla del espectro, o para ocultarla por completo. La configuración se guarda por segmento (slice).

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel de VFO debe estar abierto para el segmento que desea ajustar. Si no está visible, haga clic en la bandera del marcador de VFO de ese segmento en la pantalla del espectro.

## Pasos

1. Abra el panel de VFO para el segmento objetivo haciendo clic en su bandera de marcador de VFO en la pantalla del espectro.
2. Localice el **botón de grosor del marcador (Marker thickness button)** en el panel de VFO.
3. Haga clic en el botón para recorrer los valores disponibles: **Off**, **1 px** y **3 px**.
4. Deje de hacer clic cuando se muestre el grosor deseado. El marcador en la pantalla del espectro se actualiza de inmediato.

## Qué hace cada control

| Control                      | Valor predeterminado                                                                                                                 | Valores válidos                                                                                                           |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Botón de grosor del marcador | 1 px                                                                                                                                 | Off, 1 px, 3 px                                                                                                           |
| Botón ADSP (pestaña DSP)     | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Tiene el estilo de un conmutador de DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP. |
| Botón AetherVoice (pestaña DSP) | Activa/desactiva la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8).                     | Ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira. |

Cada clic avanza al siguiente valor en el ciclo: **Off** → **1 px** → **3 px** → **Off**. La configuración se conserva por segmento, por lo que el segmento 1 y el segmento 2 pueden tener grosores diferentes.

## Consejos

- Configurar el marcador en **Off** oculta la línea vertical por completo. El panel de VFO y la bandera permanecen visibles y funcionales.
- Si ejecuta varios segmentos en el mismo panadapter, aumentar un marcador a **3 px** puede ayudar a distinguirlo de los segmentos adyacentes.

## Cambios en la pestaña DSP en v0.9.8

La pestaña DSP en el panel de VFO ahora muestra solo los botones de reducción de ruido proporcionados por la radio. Los siguientes botones se han eliminado de la pestaña DSP del panel de VFO:

| Botón eliminado | Dónde encontrarlo ahora |
|---|---|
| NR2 | Menú superpuesto del espectro o applet AetherDSP |
| RN2 | Menú superpuesto del espectro o applet AetherDSP |
| BNR | Menú superpuesto del espectro o applet AetherDSP |
| NR4 | Menú superpuesto del espectro o applet AetherDSP |
| MNR | Menú superpuesto del espectro o applet AetherDSP |
| DFNR | Menú superpuesto del espectro o applet AetherDSP |

Los botones restantes de la pestaña DSP están dispuestos en una cuadrícula de cuatro columnas:

| Fila | Col 0 | Col 1 | Col 2 | Col 3 |
|---|---|---|---|---|
| 0 | NR | NB | ANF | APF |
| 1 | NRL | NRS | RNN | NRF |
| 2 | ANFL | ANFT | ADSP | AetherVoice (2 cols) |

El botón APF permanece oculto a menos que el segmento esté en modo CW.

Dos nuevos botones de lanzamiento del lado del cliente aparecen en la fila 2 de la cuadrícula:
- **ADSP** — Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Este botón tiene el estilo de un conmutador de DSP del lado de la radio pero no es seleccionable. Al hacer clic, abre y enfoca el diálogo no modal de configuración de AetherDSP.
- **AetherVoice** — Activa/desactiva la tira de canales de audio Aetherial — el conjunto unificado de DSP de TX/RX (v0.9.8). Este botón ocupa 2 columnas en la cuadrícula de DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.

### Control deslizante de nivel de DSP

Una fila de control deslizante de nivel compartido aparece debajo de la cuadrícula de botones de DSP. El control deslizante se redirige automáticamente al botón de DSP con nivel que se haya activado más recientemente. La etiqueta de la fila se actualiza para mostrar el objetivo activo (por ejemplo, **NR** o **NB**). El valor numérico se muestra a la derecha del control deslizante.

La fila siempre está presente en el diseño. Cuando no hay ningún DSP con nivel activo — o cuando solo RNN, ANFT o APF están encendidos — la fila se desvanece a transparente. Se vuelve completamente visible tan pronto como se enciende un DSP con nivel.

El control deslizante controla el nivel para estos objetivos:

| Etiqueta del objetivo | DSP controlado |
|---|---|
| NR | Nivel de reducción de ruido |
| NB | Nivel de anulador de ruido |
| ANF | Nivel de filtro de muesca automático |
| NRL | Nivel de reducción de ruido (NRL) |
| NRS | Nivel de sustracción espectral |
| NRF | Nivel de filtro de ruido espectral |
| ANFL | Nivel de filtro de muesca LMS |

## Comportamiento de DSP al inicio (v0.9.8)

Cuando AetherSDR se conecta a la radio, cualquier DSP que estuviera habilitado en el perfil guardado de la radio ahora envía inmediatamente su nivel al control deslizante de nivel de DSP compartido. Anteriormente, el control deslizante faltaba al inicio para estos DSP hasta que el usuario los activaba manualmente. Esta corrección asegura que el control deslizante esté siempre presente y activo cuando un DSP con nivel ya está habilitado en la radio.

## Corrección de la etiqueta de ancho de filtro (v0.9.8)

La etiqueta de ancho de filtro en el panel de VFO ahora usa una única fuente de verdad (`RxApplet::formatFilterWidth`) para generar su lectura. Esto corrige un desfase de 0.1 kHz que afectaba las lecturas en modo SSB y digital, y asegura que el panel de VFO y el applet de RX muestren valores de ancho de filtro idénticos.

## Relacionados

- [Ocultar o mostrar las líneas de borde del filtro en el espectro](hide-or-show-filter-edge-lines-on-the-spectrum.md)
- [Contraer el panel de VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Resumen del panel de VFO](overview.md)
