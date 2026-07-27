# Cargue un preajuste de escena de ruido para simulación realista de banda

Esta página explica cómo cargar un preajuste de escena de ruido con un solo clic en el Modo Demo, dando forma instantáneamente al ruido RF sintético para simular una condición de banda específica.

## Antes de comenzar

- La radio Demo incorporada debe estar conectada (consulte [Iniciar la radio demo incorporada](start-the-built-in-demo-radio.md))
- El applet de Modo Demo debe estar visible en el Panel de Applets

## Pasos

1. Localice el applet de Modo Demo en la bandeja del Panel de Applets (busque la etiqueta "DEMO").
2. Encuentre la sección **Scene presets** que contiene botones de preajuste.
3. Haga clic en el preajuste que coincida con el escenario de banda deseado (por ejemplo, **storm**, **night-40m**, **contest pileup**, **quiet band**, etc.).

La escena de ruido se actualiza de inmediato: todos los canales de ruido (ruido rosa, ruido blanco, ráfagas de QRM, birdies, etc.) y sus niveles se configuran para coincidir con el preajuste seleccionado.

## Qué hace cada control

| Control | Comportamiento |
|---------|----------------|
| **Noise channel toggles** (casillas de verificación) | Activan o desactivan fuentes de ruido individuales (ruido rosa, ruido blanco, ráfagas de QRM, birdies, etc.) |
| **Noise level sliders** | Ajustan el nivel por canal para cada fuente de ruido |
| **Scene presets** (botones pulsadores) | Botones de un solo clic que configuran todos los canales para que coincidan con un escenario específico (storm, night-40m, contest pileup, quiet band, etc.) |

## Consejos

- Los preajustes de escena anulan cualquier activación manual de canales y controles deslizantes de nivel que haya configurado.
- Después de cargar un preajuste, aún puede ajustar finamente los canales de ruido individuales usando los interruptores y controles deslizantes.

## Relacionados

- [Descripción general del Modo Demo](overview.md)
- [Dé forma al ruido RF sintético con controles por canal](shape-synthetic-rf-noise-with-per-channel-controls.md)
