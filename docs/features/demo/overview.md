# Descripción general del modo Demo

El modo Demo es una función de simulación integrada que le permite explorar AetherSDR sin una radio física. Genera ruido RF sintético a través de múltiples canales configurables, lo que le permite practicar la sintonización, el filtrado y la operación en condiciones de banda realistas.

## Cómo funciona

El modo Demo crea una "radio" virtual que se comporta como una FLEX-8600 física, pero genera ruido RF artificial en lugar de recibir señales reales. La escena de ruido es totalmente configurable, lo que la hace útil para capacitación, demostraciones o para probar funciones de AetherSDR cuando no hay ninguna radio disponible.

La simulación opera a través del applet Demo Mode, que solo se vuelve visible cuando la radio Demo integrada está conectada.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Conmutadores de canal de ruido | casilla de verificación | Habilita o deshabilita fuentes de ruido individuales: ruido rosa, ruido blanco, ráfagas de QRM, birdies y otras. Pase el cursor sobre un conmutador o su control deslizante de nivel para ver una descripción de una línea de cómo suena esa fuente de ruido en un equipo HF real y qué la causa. |
| Controles deslizantes de nivel de ruido | control deslizante | Ajusta el nivel de cada fuente de ruido habilitada de forma independiente. Pase el cursor sobre un control deslizante para ver la misma información descriptiva que en su conmutador de canal. |
| Presets de escena | botón | Aplica un preset con un solo clic que configura todos los canales de ruido para que coincidan con una condición de banda simulada específica, como tormenta, 40m nocturnos o pileup de concurso. |

## Referencia de fuentes de ruido

Cada conmutador de canal de ruido y control deslizante de nivel muestra una información sobre herramientas que explica qué es ese sonido, qué lo causa en un receptor real y cómo manejarlo. Jugar con la demo sirve también como una introducción a la HF:

| Canal | Qué es | Nota práctica |
|---|---|---|
| Tono CW | Una señal en código Morse: una señal deseada | Sus filtros y notch deben preservar esta señal. |
| Voz (habla) | Una señal de voz en SSB | El audio deseado que la reducción de ruido debe preservar, no eliminar. |
| Blanco / AWGN | Ruido térmico plano del propio receptor | El silbido de base que determina la señal más débil que puede escuchar. |
| Rosa / silbido | Ruido atmosférico de banda, más fuerte en bandas bajas | El silbido siempre presente detrás de toda señal de HF. |
| Chasquido QRN | Estática de rayos de tormentas distantes | Peor en verano y en 160/80/40 m. Un eliminador de ruido ayuda. |
| Línea eléctrica | Zumbido de red (50/60 Hz más armónicos) | Típicamente causado por proximidad a líneas eléctricas o aisladores con arcos. |
| Estallido estático | Estallidos fuertes de un frente de tormenta cercano | Las ráfagas que dominan todo cuando el clima está cerca. |
| Portadora birdie | Una portadora no deseada y constante (heterodino) | A menudo un espurio de electrónica cercana: el objetivo clásico del filtro notch. |
| Ruido SMPS | Ruido de banda ancha de fuentes de alimentación conmutadas | Cargadores de teléfono, lámparas LED, inversores solares cerca de la antena. |
| Pájaro carpintero | Un raspado pulsante de radar over-the-horizon | Llamado así por el "Woodpecker" ruso de la Guerra Fría, escuchado en todo el mundo. |

## Antes de comenzar

- AetherSDR debe estar en ejecución y ninguna radio física conectada (o debe usar intencionalmente la radio Demo).

## Cómo comenzar

1. Abra el panel **Connect**.
2. Seleccione la radio **Demo** de la lista de radios disponibles.
3. Haga clic en **Connect**.
4. El applet Demo Mode aparece en la bandeja del Applet Panel.

## Consejos

- El applet Demo Mode solo aparece mientras la radio Demo está conectada; si no lo ve, verifique que está conectado a la radio Demo y no a una FLEX-8600 física.
- Los presets de escena son una forma rápida de simular condiciones de banda realistas sin ajustar manualmente cada canal de ruido.
- Las filas de botones de preset e inyección de fallas se ajustan a múltiples líneas cuando el applet está acoplado en una bandeja estrecha, por lo que cada etiqueta de botón permanece completamente visible en cualquier ancho.

## Relacionado

- [Iniciar la radio demo integrada](start-the-built-in-demo-radio.md)
- [Dar forma al ruido RF sintético con controles por canal](shape-synthetic-rf-noise-with-per-channel-controls.md)
- [Cargar un preset de escena de ruido para simulación de banda realista](load-a-noise-scene-preset-for-realistic-band-simulation.md)
