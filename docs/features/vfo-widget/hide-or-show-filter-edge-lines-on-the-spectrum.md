# Ocultar o mostrar las líneas de borde del filtro en el espectro

El panel VFO le proporciona una opción por segmento para ocultar o mostrar las líneas verticales que marcan los bordes de la banda pasante del filtro de recepción en la visualización del espectro. Ocultarlas reduce el desorden visual cuando desea una vista del panadapter más limpia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El segmento que desea ajustar debe tener un marcador VFO visible en la visualización del espectro.

## Pasos

1. Haga clic en la bandera del marcador VFO en la visualización del espectro para el segmento objetivo. El panel VFO se abre anclado al marcador.
2. Localice el **Filter edges button** en el panel VFO.
3. Haga clic en **Filter edges button** para desactivar las líneas de borde del filtro. Vuelva a hacer clic para restaurarlas.

El estado se guarda inmediatamente. Cuando vuelva a abrir AetherSDR, la configuración se restaura al estado en que la dejó para ese segmento.

## Qué hace cada control

| Control                      | Predeterminado                                                                                                                           | Configuración persistida                                                                                               |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **Filter edges button**      | Mostrado (bordes visibles)                                                                                                               | `Slice{N}_FilterEdgesHidden`                                                                                           |
| **RX antenna button**        | Abre el menú de selección de antena para la antena receptora de este segmento. El menú utiliza la lista de antenas RX informada por el radio cuando está disponible. | No persistida                                                                                                          |
| **TX antenna button**        | Abre el menú de selección de antena para la antena transmisora de este segmento. Omite automáticamente los puertos de antena solo RX (los que comienzan con "RX") e incluye antenas cuyo nombre comienza con "ANT", "TX" o "XVTR" como respaldo. | No persistida                                                                                                          |
| **Frequency display**        | Muestra la frecuencia actual del segmento. Haga clic una vez para comenzar la entrada directa de frecuencia; escriba MHz y presione Enter o Tab. En bandas XVTR, los enteros simples de 4 o más dígitos con el segmento en el rango de 100-999 MHz insertan automáticamente un decimal después del tercer dígito (ej., 1446 → 144.6). Por encima de 1000 MHz, los enteros simples se tratan como el valor directo en MHz. Entrada máxima de frecuencia: 50000 MHz. La visualización de frecuencia muestra una superposición "LOCKED" cuando el VFO del segmento está bloqueado. | No persistida                                                                                                          |
| **Filter width label**       | Muestra el ancho de banda actual del filtro. Haga clic para recorrer los botones de preajuste de filtro en la pestaña Mode. Utiliza `RxApplet::formatFilterWidth` como fuente única de verdad, corrigiendo un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. | No persistida                                                                                                          |
| **AF Gain slider**           | 100                                                                                                                                       | No persistida — refleja el estado en vivo del radio.                                                                   |
| **Pan slider**               | 50                                                                                                                                        | No persistida                                                                                                          |
| **Mute button**              | off                                                                                                                                       | No persistida                                                                                                          |
| **Squelch button + slider**  | off                                                                                                                                       | No persistida                                                                                                          |
| **AGC combo**                | FAST                                                                                                                                      | No persistida                                                                                                          |
| **NR / NR2 / RN2 / NR4 / MNR / DFNR / BNR / NRL / NRS / RNN / NRF buttons** | off                                                                                                                     | No persistida                                                                                                          |
| **ADSP button**              | Abre el diálogo de configuración de AetherDSP (NR2 / NR4 / DFNR / RN2 / BNR / MNR del lado del cliente). Mismo punto de entrada que el menú Settings (v0.9.8). | Con estilo de alternancia DSP del lado del radio pero no verificable. Al hacer clic, abre y enfoca el diálogo modal de configuración de AetherDSP. |
| **AetherVoice button**       | Alterna la Aetherial Audio Channel Strip — el conjunto unificado de DSP de TX/RX (v0.9.8).                                                | Ocupa 2 columnas en la cuadrícula DSP de 4 columnas. Coincide con los puntos de entrada existentes del menú/cadena para la tira.              |
| **Mode combo**               | USB                                                                                                                                       | No persistida                                                                                                          |
| **Filter preset buttons**    | Aplica un preajuste guardado de ancho de filtro. Haga clic derecho para guardar el ancho de filtro actual en esa ranura.                   | `FilterPresets`                                                                                                        |
| **RIT / XIT buttons + labels** | off                                                                                                                                     | No persistida                                                                                                          |
| **DAX channel combo**        | Off                                                                                                                                       | No persistida                                                                                                          |
| **Marker thickness button**  | 1 px                                                                                                                                      | `Slice{N}_MarkerWidth`                                                                                                 |
| **Collapse toggle**          | expandido                                                                                                                                 | `SliceFlagCollapsed_{N}`                                                                                               |

`{N}` es el número del segmento. Cada segmento almacena su propio valor de forma independiente.

## Consejos

- La configuración es por segmento. Ocultar los bordes del filtro en el segmento 0 no afecta al segmento 1 ni a ningún otro segmento.
- Si ha colapsado el panel VFO a la vista solo de frecuencia, expándalo primero haciendo clic en la tira colapsada para acceder al **Filter edges button**.
- En v0.9.8, varios botones de reducción de ruido que estaban anteriormente en la pestaña DSP (NR2, RN2, BNR, NR4, MNR y DFNR) se han movido fuera del panel VFO. Esos algoritmos ahora se activan desde el menú de superposición del espectro y el applet AetherDSP. Si no ve un botón que usaba anteriormente, búsquelo allí.
- En v0.9.8, el **Filter width label** ahora utiliza `RxApplet::formatFilterWidth` como fuente única de verdad para formatear el ancho de banda del filtro. Esto corrige un desplazamiento de 0.1 kHz que afectaba las lecturas en modo SSB/digital. El ancho de filtro mostrado ahora coincide exactamente con la lectura del filtro del applet RX.
- En v0.9.8, los botones de alternancia DSP (NB, NR, ANF, NRL, NRS, NRF, ANFL) ahora colocan y retiran automáticamente la pila compartida de deslizadores de nivel DSP cuando llegan cambios de estado desde el radio. Esto asegura que el deslizador esté presente al inicio para cualquier DSP que estuviera habilitado en el perfil guardado del radio.
- En v26.5.1, el squelch está deshabilitado para los modos RTTY además de los modos digital y CW. Esto evita que el squelch bloquee señales FSK débiles enviadas a decodificadores externos a través de DAX.
- En v26.5.2.1, los menús de antena RX y TX ahora utilizan la lista de antenas por segmento informada por el radio cuando está disponible. El menú de antena TX filtra automáticamente los puertos de antena solo RX. El máximo de entrada de frecuencia para bandas XVTR se ha incrementado a 50000 MHz. La insignia del segmento ahora admite renderizado HTML (#2606).
- En v26.5.3, el panel VFO utiliza un widget `TabStack` personalizado que informa solo la sugerencia de tamaño de la pestaña actual, evitando un espacio visual al cambiar entre pestañas de diferentes alturas. La visualización de frecuencia muestra una superposición "LOCKED" cuando el VFO del segmento está bloqueado. La entrada directa de frecuencia se cancela cuando el segmento se bloquea. El sintonizador de rueda de desplazamiento en un VFO bloqueado ahora notifica al usuario que la sintonización está bloqueada.
- En v26.6.1, los controles deslizantes del panel VFO (AF Gain, Pan, Squelch threshold) ahora utilizan tokens de color conscientes del tema para el estilo de su ranura y mango, asegurando una apariencia coherente con el espectro y otros elementos temáticos. El **Pan slider** utiliza un relleno anclado al centro que se extiende hacia afuera desde el punto medio, con un pequeño punto de marca central para indicar la posición neutral.
- En v26.6.1, al panel VFO se le ha asignado su propio ámbito de contenedor de tematización (`spectrum/vfo`) que hereda las anulaciones del espectro. Esto mejora la cobertura del inspector de temas: al hacer clic en el fondo del panel VFO, la insignia del segmento o el medidor de señal, ahora se muestran los tokens de tema relevantes en el inspector.
- En v26.6.3, las etiquetas de las pestañas en el panel VFO ahora se implementan como `QPushButton` en lugar de `QLabel`, lo que las hace navegables por teclado con Tab. Use Tab para mover el foco entre las pestañas, luego presione Enter o Espacio para activar la pestaña seleccionada. Haga clic derecho en la pestaña del altavoz (primera pestaña) para alternar la muted de audio directamente.
- En v26.6.3, el sintonizador de rueda de desplazamiento respeta la configuración de rueda de ratón inversa de InteractionSettings. Habilite la configuración de rueda de ratón inversa en Preferences para invertir la dirección de desplazamiento para la sintonización de frecuencia VFO.
- En v26.6.3, la visualización de frecuencia utiliza `FreqLineEdit` para la entrada directa de frecuencia, con una sugerencia que muestra "MHz (e.g. 14.225)" en lugar de un texto de marcador de posición. El texto de la insignia dividida tiene un contraste mejorado con valores de color actualizados.
- En v26.6.3, se ha mejorado el soporte de accesibilidad. La etiqueta de frecuencia anuncia cambios a través de `QAccessibleValueChangeEvent`, asegurando que los lectores de pantalla reciban actualizaciones cuando cambie la frecuencia del segmento.

## Relacionado

- [Change the VFO marker line thickness](change-the-vfo-marker-line-thickness.md)
- [Collapse the VFO panel to frequency-only view](collapse-the-vfo-panel-to-frequency-only-view.md)
- [VFO Panel overview](overview.md)
