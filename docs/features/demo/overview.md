# Visión general del modo Demo

El modo Demo es una función de simulación integrada que le permite explorar AetherSDR sin necesidad de un equipo físico. Genera ruido RF sintético a través de múltiples canales configurables, lo que permite practicar sintonización, filtrado y operación en condiciones de banda realistas.

## Cómo funciona

El modo Demo crea una "radio" virtual que se comporta como un FLEX-8600 físico, pero genera ruido RF artificial en lugar de recibir señales reales. La escena de ruido es totalmente configurable, lo que la hace útil para entrenamiento, demostraciones o pruebas de funciones de AetherSDR cuando no se dispone de una radio.

La simulación opera a través del applet Modo Demo, que se vuelve visible solo cuando la radio Demo integrada está conectada.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Activación de canales de ruido | casilla de verificación | Activa o desactiva fuentes de ruido individuales: ruido rosa, ruido blanco, ráfagas de QRM, birdies y otros. |
| Deslizadores de nivel de ruido | deslizador | Ajusta el nivel de cada fuente de ruido activada de forma independiente. |
| Preajustes de escena | botón pulsador | Aplica un preajuste con un solo clic que configura todos los canales de ruido para simular una condición de banda específica, como tormenta, noche-40m o pileup de concurso. |

## Antes de comenzar

- AetherSDR debe estar ejecutándose y no debe tener una radio física conectada (o debe usar intencionalmente la radio Demo).

## Primeros pasos

1. Abra el panel **Connect**.
2. Seleccione la radio **Demo** de la lista de radios disponibles.
3. Haga clic en **Connect**.
4. El applet Modo Demo aparece en la bandeja del Applet Panel.

## Consejos

- El applet Modo Demo solo aparece mientras la radio Demo está conectada. Si no lo ve, verifique que esté conectado a la radio Demo y no a un FLEX-8600 físico.
- Los preajustes de escena son una forma rápida de simular condiciones de banda realistas sin ajustar manualmente cada canal de ruido.

## Relacionado

- [Iniciar la radio Demo integrada](start-the-built-in-demo-radio.md)
- [Dar forma al ruido RF sintético con controles por canal](shape-synthetic-rf-noise-with-per-channel-controls.md)
- [Cargar un preajuste de escena de ruido para simulación de banda realista](load-a-noise-scene-preset-for-realistic-band-simulation.md)
