# Descripción general de la decodificación de paquetes HF

La función de decodificación de paquetes HF descodifica datos de paquetes AX.25 de radioaficionados transmitidos en HF y VHF. Proporciona una vista en tiempo real de las tramas decodificadas, la actividad de la señal y el estado de la conexión para monitorear comunicaciones por paquetes en el FLEX-8600. El decodificador utiliza una capa de adaptación sobre libmodem para la demodulación de paquetes a nivel físico y se integra con el motor de audio para la decodificación en vivo.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a un radio FLEX-8600
- El radio debe estar sintonizado en una frecuencia de paquetes activa (HF o VHF)

## Cómo funciona

La decodificación de paquetes HF extrae el audio demodulado del flujo de audio del radio y lo pasa a través de un decodificador AX.25. Las tramas decodificadas aparecen en un área de texto desplazable a medida que se reciben, mostrando información de origen, destino y carga útil. Un indicador de actividad de señal proporciona retroalimentación visual en tiempo real sobre la detección de paquetes y el estado de la decodificación.

El decodificador admite dos perfiles de módem:
- **HF 300** (300 baudios, AFSK): Utiliza carriles de diversidad de fase de ejecución libre (PLL alfa 0) distribuidos uniformemente en el período de símbolo para una decodificación robusta. El preámbulo de TX es de 80 banderas (~2.13 segundos).
- **VHF 1200** (1200 baudios, Bell 202/APRS): Utiliza un banco híbrido de carriles demoduladores. Los carriles de diversidad de fase de ejecución libre decodifican ráfagas limpias y cortas. Los carriles con seguimiento Gardner y dos anchos de banda de PLL (alfa 0.010 y 0.025) persiguen activamente el reloj de símbolos para tolerar la desviación del reloj TX/RX y el desvanecimiento en ráfagas más largas o débiles. El preámbulo de TX es de 64 banderas (~0.43 segundos) para VHF 1200 para reducir el tiempo muerto y el tiempo de ranura.

El perfil VHF 1200 proporciona supresión de duplicados, colapsando tramas idénticas vistas por múltiples carriles en una sola emisión, similar a un TNC multi-decodificador como Dire Wolf.

La función se abre desde el área de modos digitales cuando la decodificación de paquetes HF está activa, o desde una entrada de menú relacionada.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Decoded frames | text_area | Pantalla desplazable de tramas AX.25 decodificadas que muestra información de origen, destino y carga útil. Nuevo en v26.5.2.1. |
| Signal activity | widget | Indicador de actividad de señal en tiempo real que muestra la detección de paquetes y el estado de la decodificación. Proporcionado por PacketActivityWidget. |

## Consejos

- El área de tramas decodificadas se desplaza automáticamente a medida que se reciben nuevas tramas. Use la barra de desplazamiento para revisar tramas anteriores.
- Para obtener los mejores resultados de decodificación, sintonice el radio a una frecuencia clara con actividad de paquetes activa. Las frecuencias típicas de paquetes HF están en el rango de 14.100-14.110 MHz en la banda de 20 metros y asignaciones correspondientes en otras bandas. Para VHF 1200, se aplican las frecuencias estándar de APRS (144.390 MHz en América del Norte, 144.800 MHz en Europa, etc.).
- El perfil VHF 1200 ajusta el preámbulo de TX automáticamente según el perfil seleccionado. Si usa un transverter, es posible que deba ajustar el preámbulo VHF 1200 para el tiempo de adelanto de conmutación T/R. Configure `kVhf1200TxPreambleFlags` en la configuración para ajustar este valor.

## Solución de problemas

- **No se decodifican tramas** — Verifique que el radio esté conectado y sintonizado en una frecuencia con actividad de paquetes AX.25 activa. Compruebe que el nivel de audio sea suficiente; el decodificador necesita una señal limpia para demodular.
- **Tramas distorsionadas o parciales** — Señales débiles, interferencias o sintonización incorrecta pueden causar errores de decodificación. Intente ajustar el ancho de banda del receptor o volver a sintonizar para centrar la señal dentro de la banda de paso.
- **Problemas de decodificación VHF 1200** — Asegúrese de que el perfil correcto esté seleccionado. Si usa un transverter, verifique que el preámbulo de TX proporcione suficiente tiempo de adelanto para la conmutación T/R.
