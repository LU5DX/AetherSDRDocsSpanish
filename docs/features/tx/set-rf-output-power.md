# Configurar la potencia de salida de RF

Use el control deslizante **RF Power** en el applet de Controles de TX para ajustar el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita sobreexcitar su amplificador o violar los límites de potencia de la banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet de Controles de TX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet de Controles de TX. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente, mostrando el formato "XX%".
3. Confirme que el valor mostrado en la lectura sea el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control                  | Descripción                                                                          | Valor predeterminado |
|--------------------------|--------------------------------------------------------------------------------------|----------------------|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión (0-100% del máximo). Arrastrar el valor muestra el formato "XX%". | 100                  |
| Control deslizante **Tune Pwr** | Establece el nivel de potencia de la portadora de sintonía (0-100% del máximo). Arrastrar el valor muestra el formato "XX%". | 10                   |
| Medidor **RF Pwr**       | Muestra la potencia directa real en la salida del excitador.                         | —                    |
| Medidor **SWR**           | Muestra la relación de ondas estacionarias en el excitador.                          | —                    |
| Cuadro combinado **TX Profile** | Selecciona un perfil de transmisión (p. ej., SSB, Digital) de los disponibles en la radio. | —                    |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda independientemente de este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonía y la inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador separado. Si está utilizando un amplificador externo, ajuste este control deslizante al nivel de excitación que espera su amplificador.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura de PEP más alta durante 2 segundos, luego disminuye suavemente hacia el nivel de potencia actual. El pico se borra inmediatamente a cero cuando el transmisor se desactiva.
- Los controles deslizantes de potencia ahora muestran los valores como porcentajes (0-100%) de la potencia máxima para su modelo de radio, en lugar de vatios.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en la versión v0.9.5.1 para reflejar la activación/desactivación por frecuencia que se encuentra en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya reporta una concordancia exitosa (el indicador **Success** está encendido) y no ha cambiado la frecuencia desde la última sintonía, hacer clic en **ATU** nuevamente cambia el sintonizador a modo bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonía, incluso si el estado anterior fue exitoso.

El indicador **Byp** se enciende en naranja cuando el sintonizador está en modo bypass. El indicador **Success** se enciende en verde cuando una concordancia está activa. El indicador **Mem** se enciende en verde cuando el sintonizador está usando una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin sintonía previa, o la frecuencia ha cambiado | Inicia un ciclo de sintonía |
| Concordancia exitosa/OK, misma frecuencia que la última sintonía | Cambia a modo bypass |
| Bypass activo | Inicia un nuevo ciclo de sintonía en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE.

### Menú contextual del botón ATU

Hacer clic derecho en el botón **ATU** abre un menú contextual con dos opciones adicionales:

- **Pre-tune bands…** — Abre un diálogo para ejecutar un barrido de pre-sintonía en una o más bandas. Esta opción solo está disponible cuando las memorias del ATU están habilitadas (el botón **MEM** está activado).
- **Clear ATU memories…** — Solicita confirmación, luego borra todas las memorias del ATU almacenadas en la radio.

## Uso del menú contextual del botón TUNE

Hacer clic derecho en el botón **TUNE** abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonización. Hay dos opciones disponibles:

- **Mono Tone** — Una sola portadora de tono.
- **Two Tone** — Dos portadoras de tono simultáneas.

Seleccionar cualquiera de las opciones es una configuración de un solo uso. El modo de sintonización de la radio se almacena en un estado volátil y AetherSDR no persiste esta elección entre reinicios. El modo actualmente activo se muestra con una marca de verificación.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. Cuando está activo, el botón se vuelve rojo.

En la versión v0.9.7, hacer clic en **MOX** enruta la solicitud PTT a través del coordinador de tono Quindar en lugar de activar la radio directamente. Esto significa:

- En modos de telefonía (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la tira de canales de audio, el tono K se reproduce cuando activa MOX y el tono BK se reproduce cuando lo desactiva.
- Si Quindar está deshabilitado, o el slice de TX activo no está en un modo de telefonía, el comportamiento es idéntico a versiones anteriores: la radio se activa y desactiva inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar son controlados completamente por la configuración **QUIN** en la tira de canales de audio.

## Uso del grupo APD (Predistorsión Adaptativa)

El botón de alternancia **APD** habilita o deshabilita la predistorsión adaptativa en la radio. Cuando APD está activado, tres indicadores de estado muestran el progreso:

- **Cal** (verde) — APD está encendido y aún está calibrando.
- **Avail** (verde) — Una calibración está disponible pero aún no se ha aplicado.
- **Active** (verde) — El ecualizador se aplica activamente.

La progresión típica es Cal → Avail → Active. Cuando APD está desactivado, los tres indicadores están atenuados.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea PTT esté afirmada. También verifique que el control deslizante **RF Power** no esté configurado en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — La conexión de la radio puede haberse caído. Verifique el estado de la conexión y reconéctese a través de `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonía aunque Success estuviera encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde la última sintonía. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de sintonía.
- **Los tonos Quindar no se reproducen al usar MOX** — Confirme que el slice activo esté configurado en un modo de telefonía y que el chip **QUIN** esté habilitado en la tira de canales de audio. Los tonos Quindar se suprimen en modos que no son de telefonía, independientemente de la configuración de QUIN.

## Relacionado

- [Descripción general de Controles de TX](overview.md)
- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
