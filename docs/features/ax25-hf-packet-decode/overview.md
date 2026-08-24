# Resumen de decodificación de paquetes HF

La función de decodificación de paquetes HF decodifica datos de paquetes de radioaficionados AX.25 transmitidos en HF y VHF. Proporciona una vista en tiempo real de las tramas decodificadas, la actividad de la señal y el estado de la conexión para monitorear las comunicaciones de paquetes en la FLEX-8600. El decodificador utiliza una capa de adaptación sobre libmodem para la demodulación de paquetes a nivel físico y se integra con el motor de audio para la decodificación en vivo.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a una radio FLEX-8600
- La radio debe estar sintonizada a una frecuencia de paquetes activa (HF o VHF)

## Cómo funciona

La decodificación de paquetes HF extrae el audio demodulado de la transmisión de audio de la radio y lo pasa a través de un decodificador AX.25. Las tramas decodificadas aparecen en un área de texto desplazable a medida que se reciben, mostrando información de origen, destino y carga útil. Un indicador de actividad de señal proporciona retroalimentación visual en tiempo real de la detección de paquetes y el estado de decodificación.

El decodificador admite dos perfiles de módem:
- **HF 300** (300 baudios, AFSK): Utiliza carriles de diversidad de fase de ejecución libre (alfa PLL 0) distribuidos uniformemente en el período de símbolo para una decodificación robusta. El preámbulo TX es de 80 banderas (~2.13 segundos).
- **VHF 1200** (1200 baudios, Bell 202/APRS): Utiliza un banco de carriles demoduladores con múltiples multiplicadores de ganancia de espacio. Nueve carriles utilizan los valores exactos de ganancia de espacio A+ de Direwolf (MIN_G=0.5, MAX_G=4.0) en una serie geométrica. La supresión de duplicados colapsa tramas idénticas vistas por múltiples carriles en una sola emisión, similar a multi_modem.c de Direwolf. El preámbulo TX es de 64 banderas (~0.43 segundos) para VHF 1200 para reducir el tiempo muerto y el tiempo de ranura.

Ambos perfiles utilizan una interfaz de demodulador abstracta (`IAfskDemod`) que permite que los tipos de demodulación VHF (derivado de Direwolf) y HF (libmodem) coexistan en el mismo vector de carriles. El perfil HF 300 utiliza `LibmodemAfskDemod` que envuelve el sinc_corr_afsk_demodulator de libmodem, mientras que VHF 1200 utiliza `DirewolfAfskDemod` que envuelve el AetherAFSKDemod.

La supresión de duplicados colapsa la misma trama vista por múltiples carriles en una sola emisión, como un TNC con múltiples decodificadores (por ejemplo, Dire Wolf).

El diálogo se abre desde el área de modos digitales cuando la decodificación de paquetes HF está activa, o desde una entrada de menú relacionada. El diálogo proporciona cinco pestañas: AX.25 (APRS), KISS TNC, Terminal, Mailbox y D-STAR.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Tramas decodificadas | Área de texto | Pantalla desplazable de tramas AX.25 decodificadas que muestra información de origen, destino y carga útil. Nuevo en v26.5.2.1. |
| Actividad de señal | Widget | Indicador de actividad de señal en tiempo real que muestra la detección de paquetes y el estado de decodificación. Proporcionado por PacketActivityWidget. |

### Navegación por pestañas

El diálogo proporciona cinco pestañas en la parte superior: **AX.25**, **KISS TNC**, **Terminal**, **Mailbox** y **D-STAR**. Haga clic en una pestaña para cambiar a esa página.

- **AX.25 (APRS)** — Pestaña predeterminada que muestra tramas APRS decodificadas, una tabla de estaciones y un área de transmisión.
- **KISS TNC** — Interfaz de servidor KISS TNC para aplicaciones externas.
- **Terminal** — Cliente de terminal AX.25 en modo conectado para chat por teclado.
- **Mailbox** — Buzón del Sistema de Mensajes Personales (PMS) para almacenar y reenviar mensajes.
- **D-STAR** — Página de módem D-STAR para operación de voz digital D-STAR (nuevo en v26.7.4).

### Comportamiento de la barra de estado

La barra de estado debajo del contenido de la pestaña muestra el estado del módem, la etapa de ganancia y la actividad de paquetes. Cuando la pestaña **D-STAR** está activa, la barra de estado se oculta.

El área de transmisión (con el botón Transmit y la entrada de texto) es visible solo en pestañas que no sean D-STAR y solo cuando el modo de depuración de diagnóstico está habilitado.

La descripción del módem en la barra de estado ahora incluye el preámbulo TX exacto en banderas HDLC y milisegundos, por ejemplo `HF 300: 44100 Hz, 300 bps, mark 1600 Hz, space 1800 Hz, Normal, 2 lanes, TXD 80 flags (2133 ms)`. Si ha establecido una anulación de TXDELAY, la pantalla agrega `[override]`.

### Comportamiento del botón Transmit

El botón **Transmit** en la pestaña AX.25 y el botón **Send** en la pestaña Terminal están marcados con indicadores de activación TX. Al hacer clic en cualquiera de los botones se transmite el paquete ingresado y se activa el transmisor.

### Anulación de TXDELAY

A partir de v26.8.4, puede establecer una anulación explícita de TXDELAY (tiempo de espera de activación de transmisión) en banderas HDLC. Cuando se establece, este valor anula el valor predeterminado del perfil (80 banderas en HF 300, 64 banderas en VHF 1200) tanto para la transmisión como para los cálculos de sincronización de enlace. Establecer `txPreambleFlags` en 0 (el valor predeterminado) utiliza el valor predeterminado del perfil.

La anulación es útil al barrer TXDELAY en el aire, o cuando un transverter o amplificador externo necesita más (o menos) tiempo de espera que el predeterminado del perfil. Debido a que el modelo de sincronización de la capa de enlace lee el mismo valor que el modulador, la sincronización T1 rastrea automáticamente su anulación.

## Consejos

- El área de tramas decodificadas se desplaza automáticamente a medida que se reciben nuevas tramas. Use la barra de desplazamiento para revisar tramas anteriores.
- Para obtener los mejores resultados de decodificación, sintonice la radio a una frecuencia clara con actividad de paquetes activa. Las frecuencias típicas de paquetes HF están en el rango de 14.100-14.110 MHz en 20 metros y asignaciones correspondientes en otras bandas. Para VHF 1200, se aplican las frecuencias APRS estándar (144.390 MHz en Norteamérica, 144.800 MHz en Europa, etc.).
- El perfil VHF 1200 ajusta el preámbulo TX automáticamente según el perfil seleccionado. Si usa un transverter, establezca la anulación de TXDELAY para agregar más tiempo de espera para la conmutación T/R.
- La pestaña **D-STAR** proporciona funcionalidad de módem de voz digital D-STAR. Cuando está activa, la barra de estado de actividad de paquetes y el área de transmisión están ocultas.

## Solución de problemas

- **No se decodifican tramas** — Verifique que la radio esté conectada y sintonizada a una frecuencia con actividad de paquetes AX.25 activa. Compruebe que el nivel de audio sea suficiente; el decodificador necesita una señal limpia para demodular.
- **Tramas distorsionadas o parciales** — Señales débiles, interferencia o sintonización incorrecta pueden causar errores de decodificación. Intente ajustar el ancho de banda del receptor o volver a sintonizar para centrar la señal dentro de la banda de paso.
- **Problemas de decodificación VHF 1200** — Asegúrese de que el perfil correcto esté seleccionado. Si usa un transverter, verifique que el preámbulo TX proporcione suficiente tiempo de espera para la conmutación T/R estableciendo una anulación de TXDELAY.
- **La pestaña D-STAR no funciona** — Asegúrese de que la radio esté sintonizada a una frecuencia D-STAR. El módem D-STAR requiere una señal digital limpia para una decodificación adecuada.
