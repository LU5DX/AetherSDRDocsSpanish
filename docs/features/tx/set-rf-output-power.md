# Configurar la potencia de salida de RF

Use el deslizador de **RF Power** en el applet de Controles de TX para configurar el nivel de potencia de transmisión enviado a su antena. Ajustarlo antes de transmitir evita sobrecargar su amplificador o violar los límites de potencia de la banda.

## Antes de empezar

- AetherSDR debe estar conectado a una radio FLEX-8600. Si no es así, vaya a `Settings > Connect to Radio...`.
- El applet de Controles de TX debe estar visible. Si no lo está, haga clic en el botón de la bandeja **TX** en la barra lateral derecha para mostrarlo.

## Pasos

1. Localice el deslizador **RF Power** en el applet de Controles de TX. Aparece debajo del indicador **SWR**.
2. Arrastre el deslizador hacia la izquierda o derecha para configurar el nivel de potencia deseado. La lectura numérica a la derecha del deslizador se actualiza inmediatamente.
3. Confirme que el valor mostrado en la lectura sea el que desea. El indicador **RF Pwr** reflejará la potencia directa real una vez que transmita.

## Qué hace cada control

| Control             | Descripción                                          | Predeterminado |
|---------------------|------------------------------------------------------|----------------|
| Deslizador **RF Power** | Configura el nivel de potencia de RF de transmisión enviado a la radio. | 100            |
| Medidor **RF Pwr**      | Muestra la potencia directa real en la salida del excitador. | —              |
| Medidor **SWR**         | Muestra la relación de onda estacionaria en el excitador.   | —              |

## Consejos

- La escala del medidor **RF Pwr** cambia automáticamente según el modelo de su radio. En una FLEX-8600 estándar, la zona roja comienza por encima de 100 W.
- Puede configurar límites de potencia por banda independientemente de este deslizador. Vaya a `Settings > TX Band Settings...` para configurar la potencia, la potencia de sintonía y las configuraciones de inhibición para cada banda.
- El deslizador **RF Power** controla el nivel de salida del excitador, no un amplificador externo. Si está usando un amplificador externo, configure este deslizador al nivel de excitación que su amplificador espera.

## Uso del botón ATU

El comportamiento del botón **ATU** cambió en la v0.9.5.1 para reflejar la activación/desactivación por frecuencia que se encuentra en SmartSDR.

- **Primer clic** (o cualquier clic después de un cambio de frecuencia): inicia un nuevo ciclo de sintonización del ATU.
- **Segundo clic en la misma frecuencia**: si el sintonizador ya reporta una coincidencia exitosa (el indicador **Success** está encendido) y no ha cambiado de frecuencia desde la última sintonización, al hacer clic en **ATU** nuevamente se cambia el sintonizador a bypass en lugar de iniciar un nuevo ciclo.
- **Después de cualquier cambio de frecuencia**: el registro de frecuencia sintonizada se borra automáticamente. El siguiente clic siempre inicia un nuevo ciclo de sintonización, incluso si el estado anterior era exitoso.

El indicador **Byp** se ilumina en naranja cuando el sintonizador está en bypass. El indicador **Success** se ilumina en verde cuando una coincidencia está activa. El indicador **Mem** se ilumina en verde cuando el sintonizador está usando una memoria almacenada.

| Escenario | Resultado del botón ATU |
|---|---|
| Sin sintonización previa, o la frecuencia ha cambiado | Inicia ciclo de sintonización |
| Coincidencia exitosa/OK, misma frecuencia que la última sintonización | Cambia a bypass |
| Bypass activo | Inicia un nuevo ciclo de sintonización en el siguiente clic |

> **Nota:** Los botones **ATU** y **MEM** están deshabilitados cuando el transvertidor TGXL está en modo OPERATE.

## Uso del botón MOX

El botón **MOX** activa manualmente el transmisor. Cuando está activo, el botón se vuelve rojo.

En la v0.9.7, al hacer clic en **MOX** se enruta la solicitud de PTT a través del coordinador de tonos Quindar en lugar de activar la radio directamente. Esto significa:

- En modos de fonía (SSB, AM, FM, etc.), si el chip **QUIN** está habilitado en la tira de canales de audio, el tono K se reproduce cuando activa MOX y el tono BK se reproduce cuando lo desactiva.
- Si Quindar está deshabilitado, o la slice de TX activa no está en un modo de fonía, el comportamiento es idéntico al de versiones anteriores: la radio se activa y desactiva inmediatamente.

No se requiere ningún cambio en la forma de operar el botón. Los tonos Quindar se controlan completamente mediante la configuración **QUIN** en la tira de canales de audio.

## Solución de problemas

- **El medidor RF Pwr muestra 0 W durante la transmisión** — Confirme que la radio esté realmente activada. Verifique que MOX esté activo (el botón **MOX** está rojo) o que su línea de PTT esté activada. También verifique que el deslizador **RF Power** no esté configurado en 0.
- **El deslizador se mueve pero la potencia directa no cambia** — La conexión de la radio puede haberse perdido. Verifique el estado de la conexión y reconéctese a través de `Settings > Connect to Radio...` si es necesario.
- **El botón ATU inicia una nueva sintonización aunque Success estuviera encendido** — Confirme que no haya cambiado la frecuencia de transmisión desde la última sintonización. Cualquier cambio de frecuencia borra el registro de frecuencia sintonizada almacenado y fuerza un nuevo ciclo de sintonización.
- **Los tonos Quindar no se reproducen al usar MOX** — Confirme que la slice activa esté configurada en un modo de fonía y que el chip **QUIN** esté habilitado en la tira de canales de audio. Los tonos Quindar se suprimen en modos que no son de fonía independientemente de la configuración QUIN.

## Relacionados

- [Descripción general de Controles de TX](overview.md)
- [Configurar la potencia de la portadora de sintonía](set-tune-carrier-power.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Alternar MOX para activar manualmente el transmisor](toggle-mox-to-manually-key-the-transmitter.md)
- [Cambiar perfiles de TX (ej. SSB, Digital)](switch-tx-profiles-e-g-ssb-digital.md)
