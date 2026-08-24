# Cargue un preset de escena de ruido para una simulación realista de banda

Esta página explica cómo cargar un preset de escena de ruido con un solo clic en el Modo Demo, dando forma instantáneamente al ruido RF sintético para simular una condición de banda específica.

## Antes de comenzar

- La radio Demo integrada debe estar conectada (consulte [Iniciar la radio demo integrada](start-the-built-in-demo-radio.md))
- El applet del Modo Demo debe ser visible en el Panel de Applets

## Pasos

1. Localice el applet del Modo Demo en la bandeja del Panel de Applets (busque la etiqueta "DEMO").
2. Busque la sección **Presets de escena** que contiene los botones de presets. Los botones se ajustan a varias líneas si el panel de applets es estrecho, por lo que todas las etiquetas permanecen completamente visibles.
3. Haga clic en el preset que coincida con el escenario de banda deseado (por ejemplo, **tormenta**, **noche-40m**, **pileup de concurso**, **banda tranquila**, etc.).

La escena de ruido se actualiza de inmediato: todos los canales de ruido (ruido rosa, ruido blanco, ráfagas de QRM, birdies, etc.) y sus niveles se configuran para coincidir con el preset seleccionado.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| **Alternadores de canal de ruido** (casillas de verificación) | Activan o desactivan fuentes de ruido individuales (ruido rosa, ruido blanco, ráfagas de QRM, birdies, etc.) |
| **Deslizadores de nivel de ruido** | Ajustan el nivel por canal de cada fuente de ruido |
| **Presets de escena** (botones pulsadores) | Botones de un clic que configuran todos los canales para coincidir con un escenario específico (tormenta, noche-40m, pileup de concurso, banda tranquila, etc.) |

## Consejos

- Los presets de escena anulan cualquier alternador de canal y deslizador de nivel que haya configurado manualmente.
- Después de cargar un preset, aún puede ajustar finamente los canales de ruido individuales usando los alternadores y deslizadores.
- Pase el cursor sobre cualquier alternador de canal de ruido o deslizador de nivel para ver una explicación de una línea sobre cómo suena esa fuente de ruido en una banda real de HF.
- Si los botones de preset aparecen recortados, ensanche el panel de applets — los botones ahora se ajustan en lugar de comprimirse, por lo que cada etiqueta permanece legible.

## Relacionado

- [Descripción general del Modo Demo](overview.md)
- [Dé forma al ruido RF sintético con controles por canal](shape-synthetic-rf-noise-with-per-channel-controls.md)
