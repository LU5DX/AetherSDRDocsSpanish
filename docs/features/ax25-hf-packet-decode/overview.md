# Resumen de decodificación de paquetes HF

La función de decodificación de paquetes HF decodifica datos de paquetes AX.25 de radioaficionado transmitidos en HF y VHF. Proporciona una vista en tiempo real de las tramas decodificadas, la actividad de la señal y el estado de la conexión para monitorear comunicaciones por paquetes en el FLEX-8600. El decodificador utiliza una capa de adaptación sobre libmodem para la demodulación de paquetes a nivel físico y se integra con el motor de audio para la decodificación en vivo.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a un radio FLEX-8600
- El radio debe estar sintonizado en una frecuencia activa de paquetes (HF o VHF)

## Cómo funciona

La decodificación de paquetes HF extrae el audio demodulado del flujo de audio del radio y lo pasa a través de un decodificador AX.25. Las tramas decodificadas aparecen en un área de texto desplazable a medida que se reciben, mostrando información de origen, destino y carga útil. Un indicador de actividad de la señal proporciona retroalimentación visual en tiempo real sobre la detección de paquetes y el estado de la decodificación.

El decodificador admite dos perfiles de módem:
- **HF 300** (300 baudios, AFSK): Utiliza canales de diversidad de fase de ejecución libre (PLL alfa 0) distribuidos uniformemente en el período de símbolo para una decodificación robusta. El preámbulo de TX es de 80 banderas (~2.13 segundos).
- **VHF 1200** (1200 baudios, Bell 202/APRS): Utiliza un banco de canales demoduladores con múltiples multiplicadores de ganancia espacial. Nueve canales utilizan los valores exactos de ganancia espacial A+ de Direwolf (MIN_G=0.5, MAX_G=4.0) en una serie geométrica. La supresión de duplicados colapsa las tramas idénticas vistas por múltiples canales en una sola emisión, similar a multi_modem.c de Direwolf. El preámbulo de TX es de 64 banderas (~0.43 segundos) para VHF 1200, para reducir el tiempo muerto y el tiempo de ranura.

Ambos perfiles utilizan una interfaz de demodulador abstracta (`IAfskDemod`) que permite que los tipos de demodulación VHF (derivado de Direwolf) y HF (libmodem) coexistan en el mismo vector de canales. El perfil HF 300 utiliza `LibmodemAfskDemod` envolviendo el sinc_corr_afsk_demodulator de libmodem, mientras que VHF 1200 utiliza `DirewolfAfskDemod` envolviendo el AetherAFSKDemod.

La supresión de duplicados colapsa la misma trama vista por varios canales en una sola emisión, como un TNC multidecodificador (por ejemplo, Dire Wolf).

El diálogo se abre desde el área de modos digitales cuando la decodificación de paquetes HF está activa, o desde una entrada de menú relacionada. El diálogo proporciona cinco pestañas: AX.25 (APRS), KISS TNC, Terminal, Mailbox y D-STAR.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Tramas decodificadas | text_area | Pantalla desplazable de tramas AX.25 decodificadas que muestra información de origen, destino y carga útil. Nuevo en v26.5.2.1. |
| Actividad de señal | widget | Indicador de actividad de señal en tiempo real que muestra la detección de paquetes y el estado de decodificación. Proporcionado por PacketActivityWidget. |

### Navegación por pestañas

El diálogo proporciona cinco pestañas en la parte superior: **AX.25**, **KISS TNC**, **Terminal**, **Mailbox** y **D-STAR**. Haga clic en una pestaña para cambiar a esa página.

- **AX.25 (APRS)** — Pestaña predeterminada que muestra tramas APRS decodificadas, una tabla de estaciones y un área de transmisión.
- **KISS TNC** — Interfaz de servidor KISS TNC para aplicaciones externas.
- **Terminal** — Cliente terminal AX.25 en modo conectado para chat por teclado.
- **Mailbox** — Buzón del Sistema de Mensajes Personales (PMS) para almacenar y reenviar mensajes.
- **D-STAR** — Página de módem D-STAR para operación de voz digital D-STAR (nuevo en v26.7.4).

### Comportamiento de la barra de estado

La barra de estado debajo del contenido de la pestaña muestra el estado del módem, la etapa de ganancia y la actividad de paquetes. Cuando la pestaña **D-STAR** está activa, la barra de estado está oculta.

El área de transmisión (con el botón Transmit y la entrada de texto) solo es visible en las pestañas que no son D-STAR y solo cuando el modo de depuración de diagnóstico está activado.

### Comportamiento del botón Transmit

El botón **Transmit** en la pestaña AX.25 y el botón **Send** en la pestaña Terminal están marcados con indicadores de activación de TX. Al hacer clic en cualquiera de los botones, se transmite el paquete ingresado y se activa el transmisor.

## Consejos

- El área de tramas decodificadas se desplaza automáticamente a medida que se reciben nuevas tramas. Use la barra de desplazamiento para revisar tramas más antiguas.
- Para obtener los mejores resultados de decodificación, sintonice el radio a una frecuencia clara con actividad activa de paquetes. Las frecuencias típicas de paquetes HF están en el rango de 14.100-14.110 MHz en 20 metros y asignaciones correspondientes en otras bandas. Para VHF 1200, se aplican las frecuencias APRS estándar (144.390 MHz en América del Norte, 144.800 MHz en Europa, etc.).
- El perfil VHF 1200 ajusta el preámbulo de TX automáticamente según el perfil seleccionado. Si usa un transvertidor, es posible que el preámbulo VHF 1200 necesite ajuste para el tiempo de inicio de conmutación T/R. Configure `kVhf1200TxPreambleFlags` en la configuración para ajustar este valor.
- La pestaña **D-STAR** proporciona funcionalidad de módem de voz digital D-STAR. Cuando está activa, la barra de estado de actividad de paquetes y el área de transmisión están ocultos.

## Solución de problemas

- **No se decodifican tramas** — Verifique que el radio esté conectado y sintonizado en una frecuencia con actividad activa de paquetes AX.25. Compruebe que el nivel de audio sea suficiente; el decodificador necesita una señal limpia para demodular.
- **Tramas distorsionadas o parciales** — Las señales débiles, la interferencia o la sintonización incorrecta pueden causar errores de decodificación. Intente ajustar el ancho de banda del receptor o volver a sintonizar para centrar la señal dentro de la banda de paso.
- **Problemas de decodificación VHF 1200** — Asegúrese de que el perfil correcto esté seleccionado. Si usa un transvertidor, verifique que el preámbulo de TX proporcione suficiente tiempo de inicio para la conmutación T/R.
- **La pestaña D-STAR no funciona** — Asegúrese de que el radio esté sintonizado en una frecuencia D-STAR. El módem D-STAR requiere una señal digital limpia para una decodificación adecuada.
