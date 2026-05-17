# Resumen de decodificación de paquetes HF

La función de decodificación de paquetes HF decodifica datos de paquetes AX.25 de radioaficionados transmitidos en HF. Proporciona una vista en tiempo real de las tramas decodificadas, la actividad de la señal y el estado de la conexión para monitorear las comunicaciones por paquetes en el FLEX-8600. El decodificador utiliza una capa de adaptación sobre libmodem para la demodulación de paquetes a nivel físico y se integra con el motor de audio para la decodificación en vivo.

## Antes de comenzar

- Asegúrese de que AetherSDR esté conectado a una radio FLEX-8600
- La radio debe estar sintonizada a una frecuencia activa de paquetes HF

## Cómo funciona

La decodificación de paquetes HF extrae el audio demodulado del flujo de audio de la radio y lo pasa a través de un decodificador AX.25. Las tramas decodificadas aparecen en un área de texto desplazable a medida que se reciben, mostrando información de origen, destino y carga útil. Un indicador de actividad de la señal proporciona retroalimentación visual en tiempo real sobre la detección de paquetes y el estado de la decodificación.

La función se abre desde el área de modos digitales cuando la decodificación de paquetes HF está activa, o desde una entrada de menú relacionada.

## Función de cada control

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Tramas decodificadas | text_area | Visualización desplazable de tramas AX.25 decodificadas que muestra información de origen, destino y carga útil. Nuevo en v26.5.2.1. |
| Actividad de la señal | widget | Indicador de actividad de la señal en tiempo real que muestra la detección de paquetes y el estado de la decodificación. Proporcionado por PacketActivityWidget. |

## Consejos

- El área de tramas decodificadas se desplaza automáticamente a medida que se reciben nuevas tramas. Use la barra de desplazamiento para revisar tramas anteriores.
- Para obtener los mejores resultados de decodificación, sintonice la radio a una frecuencia clara con actividad activa de paquetes HF. Las frecuencias típicas de paquetes HF se encuentran en el rango de 14.100-14.110 MHz en la banda de 20 metros y en asignaciones correspondientes en otras bandas.

## Solución de problemas

- **No se decodifican tramas** — Verifique que la radio esté conectada y sintonizada a una frecuencia con actividad activa de paquetes AX.25. Compruebe que el nivel de audio sea suficiente; el decodificador necesita una señal limpia para demodular.
- **Tramas distorsionadas o parciales** — Las señales débiles, la interferencia o una sintonización incorrecta pueden causar errores de decodificación. Intente ajustar el ancho de banda del receptor o volver a sintonizar para centrar la señal dentro de la banda de paso.
