# Resumen de decodificación de paquetes HF

La función de decodificación de paquetes HF decodifica datos de paquetes AX.25 de radioaficionado transmitidos en HF y VHF. Proporciona una vista en tiempo real de las tramas decodificadas, la actividad de la señal y el estado de la conexión para monitorear comunicaciones por paquetes en la FLEX-8600. El decodificador utiliza una capa de adaptación sobre libmodem para la demodulación de paquetes a nivel físico y se integra con el motor de audio para la decodificación en vivo.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a una radio FLEX-8600
- La radio debe estar sintonizada en una frecuencia de paquetes activa (HF o VHF)

## Cómo funciona

La decodificación de paquetes HF extrae el audio demodulado del flujo de audio de la radio y lo pasa a través de un decodificador AX.25. Las tramas decodificadas aparecen en un área de texto desplazable a medida que se reciben, mostrando información de origen, destino y carga útil. Un indicador de actividad de la señal proporciona retroalimentación visual en tiempo real sobre la detección de paquetes y el estado de la decodificación.

El decodificador admite dos perfiles de módem:
- **HF 300** (300 baudios, AFSK): Utiliza canales de diversidad de fase de ejecución libre (PLL alfa 0) distribuidos uniformemente en el período de símbolo para una decodificación robusta. El preámbulo de TX es de 80 banderas (~2.13 segundos).
- **VHF 1200** (1200 baudios, Bell 202/APRS): Utiliza un banco de canales demoduladores con múltiples multiplicadores de ganancia de espacio. Nueve canales usan los valores exactos de ganancia de espacio A+ de Direwolf (MIN_G=0.5, MAX_G=4.0) en una serie geométrica. La supresión de duplicados colapsa las tramas idénticas vistas por múltiples canales en una sola emisión, similar a multi_modem.c de Direwolf. El preámbulo de TX es de 64 banderas (~0.43 segundos) para VHF 1200, reduciendo el tiempo muerto y el tiempo de ranura.

Ambos perfiles utilizan una interfaz de demodulador abstracta (`IAfskDemod`) que permite la coexistencia de tipos de demodulación VHF (derivado de Direwolf) y HF (libmodem) en el mismo vector de canales. El perfil HF 300 utiliza `LibmodemAfskDemod` que envuelve a libmodem sinc_corr_afsk_demodulator, mientras que VHF 1200 utiliza `DirewolfAfskDemod` que envuelve a AetherAFSKDemod.

La supresión de duplicados colapsa la misma trama vista por múltiples canales en una sola emisión, como un TNC multidecodificador (por ejemplo, Dire Wolf).

La función se abre desde el área de modos digitales cuando la decodificación de paquetes HF está activa, o desde una entrada de menú relacionada.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Decoded frames | text_area | Visualización desplazable de tramas AX.25 decodificadas que muestra información de origen, destino y carga útil. Nuevo en v26.5.2.1. |
| Signal activity | widget | Indicador de actividad de señal en tiempo real que muestra la detección de paquetes y el estado de la decodificación. Proporcionado por PacketActivityWidget. |

## Consejos

- El área de tramas decodificadas se desplaza automáticamente al recibir nuevas tramas. Use la barra de desplazamiento para revisar tramas anteriores.
- Para obtener los mejores resultados de decodificación, sintonice la radio en una frecuencia limpia con actividad de paquetes activa. Las frecuencias típicas de paquetes HF están en el rango de 14.100-14.110 MHz en 20 metros y asignaciones correspondientes en otras bandas. Para VHF 1200, se aplican las frecuencias APRS estándar (144.390 MHz en América del Norte, 144.800 MHz en Europa, etc.).
- El perfil VHF 1200 ajusta el preámbulo de TX automáticamente según el perfil seleccionado. Si utiliza un transverter, es posible que deba ajustar el preámbulo VHF 1200 para el tiempo de entrada de conmutación T/R. Configure `kVhf1200TxPreambleFlags` en la configuración para ajustar este valor.

## Solución de problemas

- **No se decodifican tramas** — Verifique que la radio esté conectada y sintonizada a una frecuencia con actividad de paquetes AX.25 activa. Compruebe que el nivel de audio sea suficiente; el decodificador necesita una señal limpia para demodular.
- **Tramas distorsionadas o parciales** — Señales débiles, interferencia o sintonización incorrecta pueden causar errores de decodificación. Intente ajustar el ancho de banda del receptor o volver a sintonizar para centrar la señal dentro de la banda de paso.
- **Problemas de decodificación VHF 1200** — Asegúrese de que el perfil correcto esté seleccionado. Si utiliza un transverter, verifique que el preámbulo de TX proporcione suficiente tiempo de entrada para la conmutación T/R.
