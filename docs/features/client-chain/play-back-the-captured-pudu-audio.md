# Reproducir el audio PUDU capturado

Use el botón Play en la cadena PooDoo Audio para escuchar el audio que ya grabó a través de la cadena TX DSP. Esto le permite oír exactamente cómo sonó su señal después de cada etapa de procesamiento, sin necesidad de transmitir.

## Antes de comenzar

- Debe tener al menos una grabación capturada con el botón Record. El botón Play permanece deshabilitado hasta que exista una grabación.
- La grabación no debe estar activa. No es posible reproducir mientras haya una captura en curso.
- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de bandeja etiquetado **PUDU** en la barra lateral derecha para mostrarlo.
- El botón de modo **TX** debe estar seleccionado (predeterminado). Los botones de monitoreo forman parte de la vista de la cadena TX.

## Pasos

1. Confirme que el botón **TX** en el encabezado de la cadena PooDoo Audio esté marcado. Si no lo está, haga clic en **TX**.
2. Confirme que el botón Record (símbolo de círculo) no esté encendido ni pulsando en rojo. Si lo está, haga clic en él para detener la grabación actual antes de continuar.
3. Haga clic en el botón Play (símbolo de triángulo ▶) en la fila del encabezado de la cadena PooDoo Audio.
4. El botón Play pulsa en verde mientras la reproducción está en curso.
5. Para detener la reproducción antes de que finalice, haga clic nuevamente en el botón Play (símbolo de triángulo ▶).

## Qué hace cada control

| Control | Comportamiento | Habilitado cuando | Estado visual |
|---|---|---|---|
| Play (símbolo de triángulo) | Inicia la reproducción del audio PUDU capturado. Haga clic nuevamente para cancelar. | Existe una grabación y la grabación no está activa. Durante la reproducción, permanece habilitado para que pueda cancelarla. | Pulsa en verde (alternando entre brillante y tenue cada 500 ms) durante la reproducción. Atenuado e inactivo en reposo. |
| Record (símbolo de círculo) | Captura el audio TX posterior a PUDU. Deshabilitado durante la reproducción. | La entrada MIC está lista (fuente configurada en PC, DAX desactivado) y la reproducción no está en curso. | Pulsa en rojo durante la grabación. |

## Sugerencias

- La reproducción se inicia automáticamente al completarse una grabación. No es necesario hacer clic en Play manualmente si acaba de detener el botón Record.
- El botón Play permanece habilitado durante la reproducción, de modo que puede cancelarla en cualquier momento haciendo clic en él nuevamente.
- El pulso verde en el botón Play es el único indicador en pantalla de que la reproducción está en curso. Obsérvelo si no está seguro de si el audio se está reproduciendo.

## Resolución de problemas

- **El botón Play (símbolo de triángulo) está deshabilitado y en gris** — Aún no se ha capturado ninguna grabación, o la grabación está activa en este momento. Si el botón Record pulsa en rojo, haga clic en él para detener la grabación primero. Luego haga clic en Play.
- **El botón Play está habilitado pero no se escucha audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. AetherSDR reproduce el audio capturado a través del sistema de audio del equipo anfitrión; revise el mezclador de su sistema operativo y la selección del dispositivo de salida.

## Relacionados

- [Grabar hasta 30 segundos de audio TX posterior a PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Descripción general de la cadena PooDoo Audio](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
