# Reproducir el audio PUDU capturado

Use el botón de reproducción en el applet PooDoo Audio Chain para escuchar el audio que ya grabó a través de la cadena TX DSP. Esto le permite auditar cómo suena su señal después del procesamiento sin necesidad de transmitir.

## Antes de comenzar

- El contenedor PooDoo Audio (TXDSP) debe estar visible. Si no lo está, haga clic en el botón de la bandeja etiquetado **PUDU** en la barra lateral derecha.
- Debe haber capturado previamente una grabación usando el botón Record. El botón Play permanece deshabilitado hasta que exista una grabación.
- La grabación no debe estar activa cuando inicie la reproducción.

## Pasos

1. Confirme que el botón **TX** está seleccionado en el encabezado de la cadena (está seleccionado por defecto).
2. Localice el botón Play (▶) en la fila del encabezado, a la derecha del botón Record.
3. Haga clic en ▶ para iniciar la reproducción. El botón parpadea en verde mientras se reproduce el audio.
4. Para detener la reproducción antes de que termine, haga clic en ▶ nuevamente.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Notas |
|---|---|---|---|
| ▶ (Play) | Inicia la reproducción del audio PUDU capturado; haga clic de nuevo para cancelar. | Sin marcar | Habilitado solo cuando existe una grabación y la grabación no está activa. Parpadea en verde durante la reproducción. |
| ⏺ (Record) | Captura hasta 30 s de audio TX post-PUDU; haga clic de nuevo para detener. La reproducción inicia automáticamente al detener la grabación. | Sin marcar | Requiere MIC configurado en PC y DAX desactivado. Deshabilitado mientras la reproducción está en curso. |

## Consejos

- La reproducción inicia automáticamente cuando detiene una grabación haciendo clic en ⏺ por segunda vez. No es necesario hacer clic en ▶ manualmente después de cada grabación.
- Mientras la reproducción está en curso, el botón Record está deshabilitado. Espere a que termine la reproducción, o haga clic en ▶ para cancelarla, antes de iniciar una nueva grabación.

## Solución de problemas

- **▶ aparece en gris** — Aún no existe ninguna grabación, o hay una grabación en curso. Complete o detenga la grabación primero.
- **La reproducción no produce audio** — Verifique que la salida de audio de su sistema esté configurada correctamente. AetherSDR reproduce a través del dispositivo de salida de audio predeterminado.

## Temas relacionados

- [Grabar hasta 30 segundos de audio TX post-PUDU](record-up-to-30-seconds-of-post-pudu-tx-audio.md)
- [Descripción general de PooDoo Audio Chain](overview.md)
- [Omitir todas las etapas TX a la vez](bypass-every-tx-stage-at-once.md)
