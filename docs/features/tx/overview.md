# Descripción general de TX Controls

El applet TX Controls le da acceso directo a todas las funciones de transmisión desde un único panel: medición de potencia, ajuste del nivel de salida, selección de perfiles, sintonía de antena y linealización de señal. Ábralo cuando necesite ajustar la configuración de transmisión o monitorear la salida durante un QSO.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. TX Controls requiere una conexión de radio activa.
- Confirme que el panel de applets esté visible. Si no lo está, haga clic en `View > Applet Panel` para mostrarlo.

## Cómo funciona

El applet TX Controls siempre está presente en el panel de applets del lado derecho. Alterne su visibilidad con el botón TX de la barra lateral derecha. El applet se divide en cinco áreas funcionales:

**Medidores de potencia** — dos barras indicadoras horizontales en la parte superior del applet muestran la salida del transmisor en tiempo real.

- **RF Pwr** muestra la potencia directa en la salida del excitador. La escala es de 0–120 W en hardware FLEX-8600 estándar (zona roja por encima de 100 W) o de 0–600 W en hardware Aurora de 500 W (zona roja por encima de 500 W). La escala cambia automáticamente según el modelo de radio conectado.
- **SWR** muestra la relación de onda estacionaria en el excitador. La escala va de 1.0 a 3.0; la barra se vuelve roja por encima de 2.5.

**Controles deslizantes de potencia** — dos controles deslizantes permiten establecer los niveles de salida antes de transmitir.

- **RF Power** establece el nivel de potencia RF de transmisión. El rango es de 0–100, con valor predeterminado de 100.
- **Tune Pwr** establece el nivel de potencia de la portadora de sintonía. El rango es de 0–100, con valor predeterminado de 10. Manténgalo bajo para proteger el amplificador final y la antena durante la sintonía.

A la derecha de cada control deslizante se muestra un indicador numérico con el valor actual.

**TX Profile** — un selector desplegable con los perfiles almacenados en la radio. Al seleccionar un perfil, este se carga inmediatamente en la radio. Utilícelo para cambiar entre configuraciones como SSB, digital o modos de concurso.

**Indicadores de estado del ATU** — tres pequeños indicadores junto al selector TX Profile informan el estado del sintonizador de antena interno:

| Indicador | Se enciende cuando |
|-----------|-------------|
| Success | La sintonía del ATU se completó correctamente (apagado en caso contrario) |
| Byp | El ATU está en bypass o bypass manual (naranja) |
| Mem | El ATU opera desde una memoria almacenada (verde) |

**Botones de acción** — una fila de cuatro botones controla las operaciones de transmisión y sintonía:

| Botón | Tipo | Comportamiento |
|--------|------|----------|
| TUNE | Pulsador | Inicia una portadora de sintonía. La etiqueta cambia a "TUNING..." con fondo rojo mientras está activo. Haga clic de nuevo para detenerlo. |
| MOX | Conmutador | Activa el transmisor manualmente. Se vuelve rojo mientras TX está activo. |
| ATU | Pulsador | Inicia el ciclo de sintonía del ATU interno. Deshabilitado cuando el TGXL está en modo OPERATE. |
| MEM | Conmutador | Habilita o deshabilita la recuperación de memoria del ATU. Deshabilitado cuando el TGXL está en modo OPERATE. |

**APD (Predistorsión Adaptativa)** — la fila inferior contiene el conmutador APD y su grupo de indicadores de estado.

- **APD** activa o desactiva la predistorsión adaptativa en la radio. Cuando está habilitado, el botón se ilumina en verde.
- Tres indicadores en el panel interior a la derecha de APD muestran el progreso del proceso APD:

| Indicador | Significado |
|-----------|---------|
| Cal | APD está activado y actualmente calibrando |
| Avail | APD está activado y hay una calibración disponible pero aún no aplicada |
| Active | APD está activado y el ecualizador está aplicado activamente |

La progresión normal tras habilitar APD es Cal → Avail → Active.

## Consejos

- Establezca **Tune Pwr** en un valor bajo (10 es el predeterminado) antes de ejecutar el ATU o verificar el SWR. Sintonizar con alta potencia puede dañar un sistema de antena no adaptado.
- El botón **TUNE** envía una portadora continua en la frecuencia y modo actuales. Asegúrese de estar dentro de la banda autorizada por su licencia antes de activarlo.
- **MOX** no depende de ningún modo ni de ninguna entrada PTT: activa el transmisor de forma incondicional. Úselo con precaución.
- Los botones ATU y MEM se deshabilitan cuando el amplificador TGXL está en modo OPERATE para evitar interferencias con el estado de sintonía propio del amplificador.

## Relacionado

- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Establecer la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Cambiar perfiles TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
- [Iniciar una portadora de sintonía para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Activar MOX para teclear el transmisor manualmente](toggle-mox-to-manually-key-the-transmitter.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Recuperar una memoria del ATU](recall-an-atu-memory.md)
- [Habilitar APD para linealizar el transmisor](enable-apd-to-linearise-the-transmitter.md)
- [Ejecutar una sintonía de dos tonos](run-a-two-tone-tune.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
