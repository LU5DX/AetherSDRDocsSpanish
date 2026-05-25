# Ajustar la potencia de salida de RF

Use el control deslizante de **RF Power** en el applet de Controles de TX para establecer el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita la sobrecarga de su amplificador o la violación de los límites de potencia por banda.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet de Controles de TX debe estar visible. Si no lo está, haga clic en el botón de bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el control deslizante **RF Power** en el applet de Controles de TX. Aparece debajo del medidor **SWR**.
2. Arrastre el control deslizante hacia la izquierda o derecha para establecer el nivel de potencia deseado. La lectura numérica a la derecha del control deslizante se actualiza inmediatamente, mostrando el formato "XX W".
3. Confirme que el valor mostrado en la lectura sea el que desea. El medidor **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control                      | Descripción                                                                                          | Valor predeterminado |
|------------------------------|------------------------------------------------------------------------------------------------------|----------------------|
| Control deslizante **RF Power** | Establece el nivel de potencia de RF de transmisión enviado a la radio. El valor al arrastrar muestra el formato "XX W". | 100                  |
| Control deslizante **Tune Pwr** | Establece el nivel de potencia de la portadora de sintonía. El valor al arrastrar muestra el formato "XX W". | 10                   |
| Medidor **RF Pwr**           | Muestra la potencia directa real en la salida del excitador.                                        | —                    |
| Medidor **SWR**              | Muestra la relación de onda estacionaria en el excitador.                                            | —                    |
| Cuadro combinado **TX Profile** | Selecciona un perfil de transmisión (p. ej., SSB, Digital) de los disponibles en la radio.           | —                    |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede establecer límites de potencia por banda independientemente de este control deslizante. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonía y los ajustes de inhibición para cada banda.
- El control deslizante **RF Power** controla el nivel de salida del excitador, no un amplificador independiente. Si está utilizando un amplificador externo, ajuste este control deslizante al nivel de excitación que espera su amplificador.
- El medidor **RF Pwr** incluye una barra de retención de pico que mantiene la lectura PEP más alta durante 2 segundos, luego disminuye suavemente hacia el nivel de potencia actual. El pico se restablece inmediatamente a cero cuando el transmisor se desactiva.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en v0.9.5.1 para reflejar la conmutación por frecuencia encontrada en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonía ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya reporta una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado de frecuencia desde la última sintonía, al hacer clic en **ATU** nuevamente, el sintonizador cambia a bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de la frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonía, incluso si el estado anterior era exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando una coincidencia está activa. El indicador **Mem** se ilumina en verde cuando el sintonizador utiliza una memoria almacenada.

| Escenario                                      | Resultado del botón ATU                          |
|------------------------------------------------|--------------------------------------------------|
| Sin sintonía previa, o la frecuencia ha cambiado | Inicia un ciclo de sintonía                       |
| Coincidencia exitosa/OK, misma frecuencia que la última sintonía | Cambia a bypass                                 |
| Bypass activo                                  | Inicia un nuevo ciclo de sintonía en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE.

### Menú contextual del botón ATU

Hacer clic derecho en el botón **ATU** abre un menú contextual con dos opciones adicionales:

- **Pre-tune bands…** — Abre un diálogo para ejecutar un barrido de pre-sintonía en una o más bandas. Esta opción solo está disponible cuando las memorias ATU están habilitadas (el botón **MEM** está activado).
- **Clear ATU memories…** — Solicita confirmación y luego borra todas las memorias ATU almacenadas en la radio.

## Uso del menú contextual del botón TUNE

Hacer clic derecho en el botón **TUNE** abre un menú contextual para seleccionar la forma de la portadora para el próximo ciclo de sintonía. Están disponibles dos opciones:

- **Mono Tone** — Una única portadora de tono.
- **Two Tone** — Dos portadoras de tono simultáneas.

Seleccionar cualquiera de las opciones es una configuración de un solo uso. El modo de sintonía de la radio se almacena en estado volátil y AetherSDR no persiste esta elección entre reinicios. El modo activo actual se muestra con una marca de verificación.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. Cuando está activo, el botón se vuelve rojo.

En v0.9.7, al hacer clic en **MOX**, la solicitud de PTT se enruta a través del coordinador de tonos Quindar en lugar de activar la radio directamente. Esto significa:

- En modos de fonía (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la tira de canales de audio, el tono K suena cuando activa MOX y el tono BK suena cuando lo desactiva.
- Si Quindar está deshabilitado, o la slice de TX activa no está en un modo de fonía, el comportamiento es idéntico al de versiones anteriores: la radio se activa y desactiva inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar son controlados completamente por la configuración **QUIN** en la tira de canales de audio.

## Uso del grupo APD (Predistorsión Adaptativa)

El botón de conmutación **APD** habilita o deshabilita la predistorsión adaptativa en la radio. Cuando APD está activado, tres indicadores de estado muestran el progreso:

- **Cal** (verde) — APD está activado y aún calibrando.
- **Avail** (verde) — Hay una calibración disponible pero aún no aplicada.
- **Active** (verde) — El ecualizador está aplicado activamente.

La progresión típica es Cal → Avail → Active. Cuando APD está desactivado, los tres indicadores están apagados.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio está realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea PTT esté activada. También verifique que el control deslizante **RF Power** no esté configurado en 0.
- **El control deslizante se mueve pero la potencia directa no cambia** — La conexión con la radio puede haberse perdido. Verifique el estado de la conexión y vuelva a conectar mediante `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonía aunque Success estuviera encendido** — Confirme que no ha cambiado la frecuencia de transmisión desde la última sintonía. Cualquier cambio de frecuencia borra el registro de la frecuencia sintonizada almacenada y obliga a un nuevo ciclo de sintonía.
- **Los tonos Quindar no suenan al usar MOX** — Confirme que la slice activa está configurada en un modo de fonía y que el chip **QUIN** está habilitado en la tira de canales de audio. Los tonos Quindar se suprimen en modos que no son de fonía, independientemente de la configuración QUIN.

## Relacionados

- [Descripción general de Controles de TX](overview.md)
- [Establecer la potencia de portadora de sintonía](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonía para verificar SWR](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (p. ej., SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
