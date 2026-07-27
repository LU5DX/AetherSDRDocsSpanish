# Silenciar todos los segmentos a la vez haciendo doble clic en el botón de silencio

Silencie o reactive el audio de todos sus segmentos en una sola acción, sin tener que silenciar cada uno individualmente.

## Antes de comenzar

- Debe tener más de un segmento activo (las pestañas A a la H deben estar visibles en el applet de Controles de RX).
- El botón de silencio es el ícono del altavoz (🔊 / 🔇) en el applet de Controles de RX.

## Pasos

1. En el applet de Controles de RX, haga doble clic en el botón de silencio (🔊 cuando está activado, 🔇 cuando está silenciado).
2. Todos sus segmentos se silencian o reactivan juntos, coincidiendo con el nuevo estado del botón.

## Función de cada control

| Control | Etiqueta | Valor predeterminado |
|---------|----------|----------------------|
| Pestañas de segmento (A..H) | A..H | Ninguno |
| Distintivo de segmento | A | A |
| Bloqueo de sintonía | 🔓 / 🔒 | 🔓 (desbloqueado) |
| Antena RX | ANT1 | ANT1 |
| Antena TX | ANT1 | ANT1 |
| Ancho de filtro | 2.7K | 2.7K |
| QSK | QSK | Apagado (gris) |
| Distintivo TX | TX | Ninguno |
| Menú desplegable de modo | USB | USB |
| Etiqueta de frecuencia | 0.000.000 | 0.000.000 |
| Edición de frecuencia | (campo de texto) | Ninguno |
| STEP | (control giratorio) | 100 Hz (índice 2) |
| Valores predefinidos de ancho de filtro | (botones) | Por modo |
| Widget de banda pasante del filtro | (asas de arrastre) | Ninguno |
| Modo de tono (FM) | Off | Off |
| Valor del tono CTCSS | (menú desplegable) | Ninguno |
| Desplazamiento (FM) | 0.0 MHz | 0.0 MHz |
| Desplazamiento hacia abajo | − | Ninguno |
| Simplex | Simplex | Marcado |
| Desplazamiento hacia arriba | + | Ninguno |
| REV | REV | Ninguno |
| Botón de silencio | 🔊 / 🔇 | 🔊 (activo) |
| Ganancia AF | (deslizador) | 70 |
| Panorámica L / R | (deslizador) | 50 |
| SQL | SQL | Ninguno |
| Nivel de silenciador | (deslizador) | 20 |
| Modo CAG | Med | Med |
| Umbral CAG | (deslizador) | 65 |
| RIT | RIT | Ninguno |
| RIT 0 | RIT 0 | Ninguno |
| Desplazamiento RIT | +0 Hz | +0 Hz |
| XIT | XIT | Ninguno |
| XIT 0 | XIT 0 | Ninguno |
| Desplazamiento XIT | +0 Hz | +0 Hz |

## Consejos

- La acción de un solo clic se retrasa por el intervalo de discriminación de doble clic de la plataforma (~400 ms), por lo que un doble clic cancela el temporizador de un solo clic y activa la acción sobre todos los segmentos.
- El estado de silencio no se guarda ni se restaura al reconectar: la radio es la fuente de referencia para el silencio de audio.
- La lectura del ancho de filtro se comparte con el panel del VFO para mantener un formato coherente. El método `stepFilterWidth()` recorre las listas de valores predefinidos por modo, de modo que los atajos de ensanchar/estrechar produzcan una geometría de bordes correcta según el modo.
- Al cambiar a RTTY o modos digitales (DIGU, DIGL), el silenciador se desactiva automáticamente; de lo contrario, eliminaría los caracteres FSK e impediría la decodificación.
- Al salir del modo RADE mediante el menú desplegable de modo, el applet emite `radeActivated(false)` solo si el segmento estaba realmente en RADE, evitando señales de desactivación obsoletas al cambiar de modo en un segmento que no está en RADE.
- El menú de antena RX ahora incluye tokens de antena virtual de un KiwiSDR conectado si el administrador de KiwiSDR está activo. Al seleccionar una antena virtual de KiwiSDR, se emite `kiwiRxAntennaSelected(sliceId, profileId)` en lugar de llamar a `setRxAntenna()` directamente.

## Relacionado

- [Resumen de Controles de RX](overview.md)
- [Cambie entre múltiples segmentos usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprenda por qué el estado de silencio no se restaura al reconectar (política de autoridad de la radio #2489)](../../getting-started/setup/understand-why-mute-state-is-not-restored-on-reconnect-radio-authoritative-policy-2489.md)
