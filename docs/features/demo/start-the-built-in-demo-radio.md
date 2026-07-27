# Iniciar la radio de demostración incorporada

La radio de demostración incorporada simula una FLEX-8600 con ruido RF sintético, permitiéndole explorar las funciones de AetherSDR sin una radio física conectada. Esto es útil para aprender la interfaz, probar configuraciones o demostrar el software.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución.
- No es necesario conectar ningún FlexRadio físico.

## Pasos

1. Abra **Settings > Connect to Radio...** desde la barra de menú.
2. En el cuadro de diálogo de conexión, seleccione **Demo** de la lista de radios.
3. Haga clic en **Connect**.

La ventana principal ahora muestra un panadapter y una pantalla de espectro con ruido sintético. El panel del applet Demo Mode estará disponible en la bandeja en la parte inferior de la ventana.

## Función de cada control

El panel del applet Demo Mode aparece solo cuando la radio de demostración está conectada. Contiene los siguientes controles:

| Control | Tipo | Comportamiento |
|---------|------|----------------|
| Conmutadores de canal de ruido | Casilla de verificación | Activa o desactiva fuentes de ruido individuales (ruido rosa, ruido blanco, ráfagas QRM, birdies). |
| Deslizadores de nivel de ruido | Deslizador | Ajusta la amplitud de cada fuente de ruido activada de forma independiente. |
| Escenas predefinidas | Botón pulsador | Botones de un solo clic que configuran todos los canales de ruido para que coincidan con un escenario específico (tormenta, noche-40m, pileup de concurso, banda silenciosa, etc.). |

## Consejos

- La radio de demostración no admite operaciones de transmisión.

## Relacionados

- [Demo Mode overview](overview.md)
- [Shape synthetic RF noise with per-channel controls](shape-synthetic-rf-noise-with-per-channel-controls.md)
- [Load a noise scene preset for realistic band simulation](load-a-noise-scene-preset-for-realistic-band-simulation.md)
