# Omitir el compresor de la cadena

El widget CHAIN controla si la etapa del compresor está activa u omitida. Utilícelo para retirar el compresor de la ruta de señal TX sin modificar ninguno de sus ajustes.

## Antes de comenzar

- AetherSDR debe estar abierto con el contenedor principal PooDoo Audio (TXDSP) visible.
- El mosaico del subcontenedor COMPRESSOR solo se muestra cuando la etapa del compresor está habilitada (modo bypass desactivado). Cuando está en bypass, el mosaico se oculta automáticamente.

## Pasos

1. Localice el widget CHAIN dentro del contenedor principal PooDoo Audio (TXDSP).
2. Haga clic una vez en la etapa Comp del widget CHAIN para activar o desactivar el bypass del compresor.

Cuando el bypass está desactivado, `ClientCompTxEnabled` se establece en true y el mosaico del subcontenedor COMPRESSOR se vuelve visible. Cuando el bypass está activado, `ClientCompTxEnabled` se establece en false y el mosaico se oculta.

## Consejos

- Los ajustes de umbral, relación, ataque, liberación y ganancia de compensación se conservan al activar el bypass. Al volver a habilitar el compresor, este se restaura exactamente como se dejó.
- Para abrir el editor completo con los controles de rodilla y limitador, haga doble clic en la etapa Comp del widget CHAIN en lugar de un solo clic.

## Relacionado

- [Descripción general del compresor](overview.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Observar la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
