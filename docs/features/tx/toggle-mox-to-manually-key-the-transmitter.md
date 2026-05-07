# Activar MOX para poner manualmente el transmisor en onda

MOX le permite poner el transmisor en onda sin un pedal o línea PTT. Úselo para verificar el audio, probar su señal o transmitir cuando no haya PTT por hardware disponible.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. MOX no tiene efecto cuando el equipo está desconectado.
- Confirme que su perfil de TX y el nivel de potencia de RF estén configurados correctamente antes de poner el transmisor en onda.
- En v0.9.7, si tiene los tonos Quindar habilitados en la tira del canal de audio (Audio Channel Strip), los tonos K y BK se reproducirán automáticamente al activar y desactivar MOX en modos de fonía. No se requiere configuración adicional.

## Pasos

1. Si el applet de controles de TX (TX Controls) no está visible, haga clic en el botón de bandeja **TX** en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para poner el transmisor en onda. El botón se vuelve rojo mientras la TX está activa.
4. Haga clic en **MOX** nuevamente para sacar el transmisor de onda. El botón vuelve a su estado apagado.

## Qué hace cada control

| Control          | Comportamiento                                                                                                                                                                                                                                                           | Por defecto |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| **MOX**          | Activa o desactiva la transmisión manual. El botón se vuelve rojo mientras el transmisor está en onda. En v0.9.7, el clic pasa por el coordinador de tonos Quindar, por lo que los tonos K/BK se reproducen al activar/desactivar en modos de fonía cuando Quindar está habilitado en la tira del canal de audio (Audio Channel Strip). | Apagado     |
| **RF Power**     | Establece el nivel de potencia de RF de transmisión enviado al equipo.                                                                                                                                                                                                   | 100         |
| **RF Pwr** medidor | Muestra la potencia directa a la salida del excitador. Se vuelve rojo por encima de 100 W (sin amplificador) o 500 W (Aurora 500W).                                                                                                                                      | —           |
| **SWR** medidor  | Muestra la relación de onda estacionaria (ROE) en el excitador. Se vuelve rojo por encima de 2.5.                                                                                                                                                                        | —           |

## Comportamiento del botón ATU

A partir de v0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonía y puentear el acoplador, coincidiendo con el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que hace clic en él:

- **Primer clic en una frecuencia nueva** — inicia un ciclo de sintonía del ATU.
- **Segundo clic en la misma frecuencia, después de una sintonía exitosa** — cambia el ATU a modo puente.
- **Cualquier clic después de un cambio de frecuencia** — inicia un nuevo ciclo de sintonía, incluso si la sintonía anterior fue exitosa.

Al ingresar al modo puente se borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un nuevo ciclo de sintonía.

Los botones **ATU** y **MEM** están deshabilitados cuando el TGXL está en modo OPERATE.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** tan pronto como active MOX. Si la ROE supera 2.5 (zona roja), desactive inmediatamente e investigue su sistema de antena.
- Ajuste **RF Power** a un valor bajo antes de usar MOX por primera vez en una banda nueva.
- MOX pone el equipo en transmisión a máxima potencia en el modo que esté activo. Si solo necesita verificar la ROE o sintonizar un ATU, use **TUNE** en su lugar: transmite una portadora al nivel de **Tune Pwr**, que es más bajo.
- Después de una sintonía exitosa del ATU, al hacer clic en **ATU** nuevamente en la misma frecuencia, el acoplador pasa a modo puente. Para volver a sintonizar después de cambiar de banda o frecuencia, simplemente haga clic una vez en **ATU** en la nueva frecuencia.
- Si los tonos Quindar están habilitados en la tira del canal de audio (Audio Channel Strip), al cambiar a un modo digital o CW se suprimen los tonos K/BK automáticamente. El comportamiento de MOX es el mismo independientemente del modo.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR esté conectado al equipo. El applet de controles de TX (TX Controls) requiere una conexión activa al equipo.
- **El transmisor se activa pero no se muestra potencia de RF** — Verifique que **RF Power** no esté en 0 y que el perfil de TX correcto esté cargado en el selector **TX Profile**.
- **El equipo permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente de PTT (pedal, VOX, comando CAT) podría estar manteniendo el equipo en transmisión. Revise el hardware de PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una nueva sintonía en lugar de puentear** — La frecuencia de transmisión ha cambiado desde la última sintonía exitosa. El botón ATU siempre iniciará un nuevo ciclo de sintonía cuando la frecuencia difiera de aquella en la que el acoplador reportó por última vez una adaptación exitosa.
- **Los tonos Quindar no suenan al hacer clic en MOX** — Confirme que el chip QUIN esté habilitado en la tira del canal de audio (Audio Channel Strip) y que el slice de TX activo esté en un modo de fonía (SSB, AM, FM). Los tonos Quindar no se generan en modos CW o digitales.

## Relacionado

- [Descripción general de controles de TX](overview.md)
- [Iniciar una portadora de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ajustar la potencia de salida de RF](set-rf-output-power.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Haga su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
