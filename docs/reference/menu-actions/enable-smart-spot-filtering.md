# Activar el Filtrado Inteligente de Spots

El Filtrado Inteligente de Spots atenúa los spots de SSB en el panadapter cuando no se detecta una señal de voz dentro de ±1 kHz de la frecuencia del spot, lo que le ayuda a concentrarse en conversaciones activas. Los spots de CW y digitales no se ven afectados. Esta función requiere que el Historial de Señales esté habilitado.

## Antes de comenzar

- Asegúrese de que el Historial de Señales esté habilitado en AetherSDR.
- Verifique que tenga una conexión activa con una radio FLEX-8600.

## Pasos

1. Abra el menú **View**.
2. Haga clic en **Smart Spot Filtering** para activarlo (aparece una marca de verificación cuando está habilitado).

## Qué hace cada control

| Control | Comportamiento |
|---------|----------|
| Smart Spot Filtering (elemento del menú) | Marcable; desactivado por defecto. Cuando está habilitado, los spots de SSB sin señal de voz detectada dentro de ±1 kHz se atenúan. Clave de configuración persistida: `SmartSpotFilterEnabled`. |

## Consejos

- El Filtrado Inteligente de Spots funciona mejor en condiciones de banda con mucho tráfico, donde se muestran muchos spots de SSB.
- El filtro se aplica en tiempo real a medida que el Historial de Señales se actualiza.

## Relacionado

- [Configurar el Plan de Banda](configure-band-plan.md)
- [Activar las Condiciones de Propagación](enable-propagation-conditions.md)
