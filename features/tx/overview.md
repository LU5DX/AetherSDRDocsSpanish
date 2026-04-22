# Descripción general de los controles de transmisión

El applet TX Controls le da acceso a todas las funciones de transmisión en un solo panel: medición de potencia, ajuste de potencia de RF y sintonía, selección de perfil TX, activación manual del transmisor, control del ATU y predistorsión adaptativa. Ábralo siempre que necesite supervisar o ajustar la cadena de transmisión de su estación.

## Cómo funciona

El applet TX Controls se encuentra en el panel de applets (barra lateral derecha) y está siempre accesible. Active o desactive su visibilidad con el botón TX de la bandeja en la barra lateral derecha. El applet requiere una conexión de radio activa para funcionar.

El applet está organizado en cinco áreas funcionales:

**Medidores de potencia** — Dos barras de nivel horizontales en la parte superior muestran lecturas de transmisión en tiempo real. "RF Pwr" muestra la potencia directa a la salida del excitador en vatios; la escala va de 0 a 120 W para operación estándar, con la zona roja a partir de 100 W. En una radio Aurora con capacidad de 500 W, la escala se extiende de 0 a 600 W, con rojo por encima de 500 W. "SWR" muestra la relación de onda estacionaria en una escala de 1.0 a 3.0, con rojo por encima de 2.5.

**Controles deslizantes de potencia** — "RF Power" establece el nivel de potencia de RF de transmisión de 0 a 100 (valor predeterminado: 100). "Tune Pwr" establece el nivel de potencia de la portadora de sintonía de 0 a 100 (valor predeterminado: 10). Un indicador numérico a la derecha de cada control deslizante muestra el valor actual.

**Perfil TX** — El menú desplegable "TX Profile" muestra los perfiles de transmisión disponibles en la radio conectada. Al seleccionar un perfil, este se carga de inmediato. Los tres pequeños indicadores junto al menú desplegable ("Success", "Byp", "Mem") reflejan el estado del ATU:

| Indicador | Color cuando está encendido | Significado |
|-----------|---------------------------|-------------|
| Success | Verde | El ATU sintonizó correctamente o el estado es correcto |
| Byp | Naranja | El ATU está en modo Bypass o ManualBypass |
| Mem | Verde | El ATU está usando una memoria almacenada |

**Botones TUNE / MOX / ATU / MEM** — Cuatro botones controlan la activación del transmisor y la sintonía de antena:

| Botón | Tipo | Comportamiento |
|-------|------|----------------|
| TUNE | Botón momentáneo | Inicia o detiene una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras la portadora está activa. |
| MOX | Botón de alternancia | Activa el transmisor manualmente. El botón se pone rojo mientras el TX está activado. |
| ATU | Botón momentáneo | Inicia el ciclo de sintonía del ATU interno. Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM | Botón de alternancia | Habilita o deshabilita la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |

**APD** — El botón de alternancia "APD" habilita la Predistorsión Adaptativa en la radio, lo cual linealiza el transmisor. Tres indicadores muestran el progreso del APD:

| Indicador | Color cuando está encendido | Significado |
|-----------|---------------------------|-------------|
| Cal | Verde | El APD está activo y calibrando |
| Avail | Verde | El APD está activo y hay una calibración disponible, pero aún no se ha aplicado |
| Active | Verde | El APD está activo y el ecualizador se aplica de forma activa |

La progresión normal después de habilitar el APD es Cal → Avail → Active.

## Temas relacionados

- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ajustar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de sintonía para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para transmitir manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar el APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Hacer su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
