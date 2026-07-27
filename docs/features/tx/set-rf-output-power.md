# Configurar la potencia de salida de RF

Utilice el control deslizante **RF Power** en el applet Controles de TX para ajustar el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita sobrecargar su amplificador o violar los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet Controles de TX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet Controles de TX. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente, mostrando el formato "XX%".
3. Confirme que el valor mostrado en la lectura sea el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.
4. Pase el cursor del mouse sobre el medidor **RF Pwr** o **SWR** para ver la lectura numérica exacta en una información sobre herramientas emergente. La información emergente de **RF Pwr** muestra el valor en vatios (ej., "45 W"), y la de **SWR** muestra la relación en formato convencional (ej., "1.42:1"). Esto es útil para lecturas precisas entre las marcas de graduación.

## Función de cada control

| Control                    | Descripción                                                                                | Predeterminado |
|----------------------------|--------------------------------------------------------------------------------------------|----------------|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión (0-100% del máximo). El valor arrastrado muestra el formato "XX%". | 100            |
| Control deslizante **Tune Pwr**  | Establece el nivel de potencia de la portadora de sintonía (0-100% del máximo). El valor arrastrado muestra el formato "XX%". | 10             |
| Medidor **RF Pwr**         | Muestra la potencia directa real en la salida del excitador con retención de pico PEP. Pase el cursor para ver la potencia exacta en vatios. | —              |
| Medidor **SWR**            | Muestra la relación de onda estacionaria en el excitador. Pase el cursor para ver la relación exacta en formato N.N:1. | —              |
| Cuadro combinado **TX Profile** | Selecciona un perfil de transmisión (ej., SSB, Digital) de los disponibles en la radio.    | —              |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda independientemente de este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonía y las configuraciones de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador separado. Si está utilizando un amplificador externo, ajuste este control deslizante al nivel de excitación que su amplificador espera.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos, luego disminuye suavemente hacia el nivel de potencia actual. El pico se limpia inmediatamente a cero cuando el transmisor desactiva la transmisión.
- Los controles deslizantes de potencia ahora muestran los valores como porcentajes (0-100%) de la potencia máxima para su modelo de radio, en lugar de vatios.
- Pasar el cursor sobre el medidor **RF Pwr** o **SWR** muestra una lectura numérica exacta en una información sobre herramientas emergente, eliminando la necesidad de estimar entre las marcas de graduación durante la transmisión.

## Uso del botón TUNE

El botón **TUNE** inicia o detiene una portadora de sintonía. Mientras está activo, el texto del botón cambia a "TUNING..." con un fondo rojo.

### Menú contextual del botón TUNE

Al hacer clic derecho en el botón **TUNE** se abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Hay dos opciones disponibles:

- **Mono Tone** — Un solo tono de portadora.
- **Two Tone** — Dos tonos de portadora simultáneos.

Seleccionar cualquiera de las opciones es una configuración de un solo uso. El modo de sintonía de la radio se almacena en un estado volátil y AetherSDR no persiste esta elección entre reinicios. El modo actualmente activo se muestra con una marca de verificación.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. El botón tiene un estilo visual distintivo: un borde y texto de color ámbar cuando está inactivo (modo recepción) para identificarlo claramente como el botón de transmisión, y se vuelve rojo con un borde rojo brillante cuando está activo (modo transmisión). Este color de acento se puede editar en el Editor de temas bajo los tokens `color.tx.mox.*`.

Cuando está activo, el botón se vuelve rojo ("QPushButton { background: #cc2222; border: 1px solid #ff4444; ...}").

En la versión v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar directamente la radio. Esto significa:

- En modos de voz (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la Tira de canales de audio, el tono K suena cuando activa MOX y el tono BK suena cuando lo desactiva.
- Si Quindar está deshabilitado, o la porción de TX activa no está en un modo de voz, el comportamiento es idéntico a versiones anteriores: la radio activa y desactiva la transmisión inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar se controlan completamente mediante la configuración **QUIN** en la Tira de canales de audio.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en la versión v0.9.5.1 para reflejar la activación/desactivación por frecuencia que se encuentra en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya informa una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado la frecuencia desde la última sintonización, al hacer clic en **ATU** nuevamente se cambia el sintonizador a bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior fue exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando una coincidencia está activa. El indicador **Mem** se ilumina en verde cuando el sintonizador utiliza una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin sintonización previa, o la frecuencia ha cambiado | Inicia el ciclo de sintonización |
| Coincidencia Éxito/OK, misma frecuencia que la última sintonización | Cambia a bypass |
| Bypass activo | Inicia un nuevo ciclo de sintonización en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE.

### Menú contextual de ATU

Al hacer clic derecho en el botón **ATU** se abre un menú contextual con dos opciones adicionales:

- **Pre-tune bands…** — Abre un diálogo para ejecutar un barrido de pre-sintonización en una o más bandas. Esta opción solo está disponible cuando las memorias ATU están habilitadas (el botón **MEM** está encendido).
- **Clear ATU memories…** — Solicita confirmación, luego borra todas las memorias ATU almacenadas en la radio.

## Uso del botón de alternancia MEM

El botón **MEM** activa o desactiva la recuperación de la memoria ATU. Cuando está habilitado, el sintonizador puede usar datos de sintonización almacenados para frecuencias previamente sintonizadas. Este botón está deshabilitado cuando el transvertidor TGXL está en modo OPERATE.

## Uso del grupo APD (Pre-Distorsión Adaptativa)

El botón de alternancia **APD** activa o desactiva la pre-distorsión adaptativa en la radio. Cuando APD está activado, tres indicadores de estado muestran el progreso:

- **Cal** (verde) — APD está activado y aún calibrando.
- **Avail** (verde) — Hay una calibración disponible pero aún no se ha aplicado.
- **Active** (verde) — El ecualizador se aplica activamente.

La progresión típica es Cal → Avail → Active. Cuando APD está desactivado, los tres indicadores están atenuados.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea PTT esté activada. También verifique que el control deslizante **RF Power** no esté configurado en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — Es posible que la conexión de la radio se haya interrumpido. Verifique el estado de la conexión y vuelva a conectarse a través de `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonización aunque Success estuviera encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde la última sintonización. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de sintonización.
- **Los tonos Quindar no suenan al usar MOX** — Confirme que la porción activa esté configurada en un modo de voz y que el chip **QUIN** esté habilitado en la Tira de canales de audio. Los tonos Quindar se suprimen en modos que no son de voz, independientemente de la configuración QUIN.

## Relacionados

- [TX Controls overview](overview.md)
- [Set tune-carrier power](set-tune-carrier-power.md)
- [Start a tune carrier to check SWR](start-a-tune-carrier-to-check-swr.md)
- [Toggle MOX to manually key the transmitter](toggle-mox-to-manually-key-the-transmitter.md)
- [Switch TX profiles (e.g. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
