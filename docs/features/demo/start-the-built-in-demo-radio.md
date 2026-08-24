# Iniciar la radio de demostración integrada

La radio de demostración integrada simula una FLEX-8600 con ruido RF sintético, lo que le permite explorar las funciones de AetherSDR sin tener una radio física conectada. Esto es útil para aprender la interfaz, probar configuraciones o demostrar el software.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución.
- No es necesario conectar ninguna FlexRadio física.

## Pasos

1. Abra **Settings > Connect to Radio...** desde la barra de menú.
2. En el diálogo de conexión, seleccione **Demo** en la lista de radios.
3. Haga clic en **Connect**.

La ventana principal ahora muestra un panadapter y una pantalla de espectro con ruido sintético. El panel del applet Demo Mode estará disponible en la bandeja en la parte inferior de la ventana.

## Qué hace cada control

El panel del applet Demo Mode aparece únicamente cuando la radio de demostración está conectada. Contiene los siguientes controles:

| Control | Tipo | Comportamiento |
|---------|------|----------|
| Conmutadores de canal de ruido | Casilla de verificación | Activan o desactivan fuentes de ruido individuales (ruido rosa, ruido blanco, ráfagas de QRM, birdies). Pase el cursor sobre cualquier conmutador para escuchar cómo suena ese ruido en un equipo de HF real y cómo lidiar con él. |
| Deslizadores de nivel de ruido | Deslizador | Ajustan la amplitud de cada fuente de ruido activada de forma independiente. Pase el cursor sobre cualquier deslizador para ver la misma información educativa. |
| Ajustes preestablecidos de escena | Botón pulsador | Botones de un clic que configuran todos los canales de ruido para que coincidan con un escenario específico (tormenta, noche en 40 m, pileup de concurso, banda silenciosa, etc.). Los botones se envuelven en nuevas líneas cuando el panel es demasiado estrecho, de modo que cada etiqueta permanezca completamente visible. |

## Consejos

- La radio de demostración no admite operaciones de transmisión.
- Cada canal de ruido tiene una información sobre herramientas al pasar el cursor que explica qué es ese sonido en una banda real: qué lo causa y qué puede hacer al respecto. Jugar con la demostración funciona como una introducción a la HF: por ejemplo, pase el cursor sobre el conmutador **Birdie carrier** para aprender que se trata de una portadora no deseada constante (heterodino), a menudo un espurio de la electrónica cercana, y que un filtro de muesca es la solución clásica.

## Relacionados

- [Información general del Modo Demo](overview.md)
- [Dé forma al ruido RF sintético con controles por canal](shape-synthetic-rf-noise-with-per-channel-controls.md)
- [Cargue un ajuste preestablecido de escena de ruido para una simulación de banda realista](load-a-noise-scene-preset-for-realistic-band-simulation.md)
