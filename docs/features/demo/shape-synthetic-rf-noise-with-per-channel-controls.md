# Dé forma al ruido RF sintético con controles por canal

Modele el entorno de RF simulado cuando utilice la radio Demo incorporada habilitando o deshabilitando fuentes de ruido individuales y ajustando sus niveles.

## Antes de comenzar

- Conéctese a la radio Demo incorporada desde el diálogo **Settings > Connect to Radio...** o desde el panel Connect

## Pasos

1. Abra el applet Demo Mode desde la bandeja del Applet Panel (el botón DEMO de la bandeja aparece solo cuando la radio Demo está conectada).
2. En el applet, localice la sección **Noise channel toggles**. Cada casilla de verificación controla una fuente de ruido independiente: ruido rosa, ruido blanco, ráfagas de QRM, birdies y otras.
3. Marque una casilla para habilitar esa fuente de ruido; desmárquela para deshabilitarla.
4. Para cada fuente de ruido habilitada, ajuste su **Noise level slider** para definir la intensidad.
5. Opcionalmente, haga clic en un botón de **Scene presets** para configurar todos los canales a la vez para un escenario específico (tormenta, noche-40m, pileup de concurso, banda silenciosa, etc.).

## Qué hace cada control

| Control | Acción |
|---------|--------|
| Noise channel toggles (casillas de verificación) | Habilitan o deshabilitan fuentes de ruido individuales. Fuentes disponibles: ruido rosa, ruido blanco, ráfagas de QRM, birdies y otras. |
| Noise level sliders | Ajustan el nivel de cada fuente de ruido habilitada de forma independiente. |
| Scene presets (botones) | Aplican una combinación preconfigurada de canales y niveles de ruido para simular una condición de banda específica. |

## Referencia de fuentes de ruido

Pase el cursor sobre cualquier conmutador de canal de ruido o control deslizante de nivel para ver una descripción de una línea sobre qué es ese sonido y qué lo causa en un equipo real de HF. Las fuentes incluyen:

| Fuente | Qué simula |
|--------|-------------------|
| CW tone | Una señal de código Morse: una señal deseada que el filtro y el notch deben preservar |
| Voice (speech) | Una señal de voz SSB: el audio deseado que la reducción de ruido debe conservar |
| White / AWGN | Ruido térmico plano del propio receptor: el siseo base que define la sensibilidad |
| Pink / hiss | Ruido atmosférico de banda, más fuerte en bandas bajas |
| QRN crackle | Estática de rayos de tormentas lejanas; los blankers de ruido ayudan |
| Power-line | Zumbido de red eléctrica (50/60 Hz más armónicos) de líneas eléctricas o aisladores con arco |
| Static crash | Estallidos fuertes de un frente de tormenta cercano |
| Birdie carrier | Una portadora no deseada y constante (heterodino): el objetivo clásico del filtro notch |
| SMPS hash | Ruido de banda ancha de fuentes de alimentación conmutadas (cargadores de teléfono, lámparas LED, inversores solares) |
| Woodpecker | Un chirrido pulsante de radar over-the-horizon |

## Consejos

- Comience con todas las fuentes de ruido deshabilitadas (todas las casillas sin marcar) para escuchar la simulación más limpia; luego habilite las fuentes una a la vez para comprender su carácter.
- Use los Scene presets como punto de partida rápido y luego ajuste los controles deslizantes individuales.
- Las descripciones emergentes de las fuentes de ruido funcionan también como una introducción a HF: explican la causa de cada sonido en una banda real y qué hacer al respecto.

## Relacionado

- [Start the built-in demo radio](start-the-built-in-demo-radio.md)
- [Load a noise scene preset for realistic band simulation](load-a-noise-scene-preset-for-realistic-band-simulation.md)
- [Demo Mode overview](overview.md)
