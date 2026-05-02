# Activar MOX para clave el transmisor manualmente

MOX le permite clave el transmisor sin un pedal de pie ni una línea PTT. Úselo para verificar el audio, probar su señal o transmitir cuando el PTT por hardware no esté disponible.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. MOX no tiene efecto cuando el radio está desconectado.
- Confirme que su perfil TX y el nivel de RF Power estén configurados correctamente antes de clave.

## Pasos

1. Si el applet TX Controls no está visible, haga clic en el botón **TX** de la bandeja en la barra lateral derecha para mostrarlo.
2. Localice el botón **MOX** en la fila de botones junto a TUNE, ATU y MEM.
3. Haga clic en **MOX** para clave el transmisor. El botón se torna rojo mientras TX está activo.
4. Haga clic en **MOX** nuevamente para desclave el transmisor. El botón regresa a su estado apagado.

## Qué hace cada control

| Control          | Comportamiento                                                                                                      | Predeterminado |
|------------------|---------------------------------------------------------------------------------------------------------------------|----------------|
| **MOX**          | Activa o desactiva la transmisión manual. El botón se torna rojo mientras el transmisor está clavado.               | Off            |
| **RF Power**     | Establece el nivel de potencia RF de transmisión enviado al radio.                                                  | 100            |
| **RF Pwr** meter | Muestra la potencia directa en la salida del excitador. Se torna rojo por encima de 100 W (barefoot) o 500 W (Aurora 500W). | —         |
| **SWR** meter    | Muestra la relación de onda estacionaria en el excitador. Se torna rojo por encima de 2.5.                          | —              |

## Comportamiento del botón ATU

A partir de la versión v0.9.5.1, el botón **ATU** alterna entre iniciar un ciclo de sintonización y puentear el sintonizador, siguiendo el comportamiento por frecuencia de SmartSDR.

El botón sigue esta lógica cada vez que se hace clic en él:

- **Primer clic en una nueva frecuencia** — inicia un ciclo de sintonización del ATU.
- **Segundo clic en la misma frecuencia, tras una sintonización exitosa** — cambia el ATU al modo bypass.
- **Cualquier clic tras un cambio de frecuencia** — inicia un nuevo ciclo de sintonización, incluso si la sintonización anterior fue exitosa.

Entrar en bypass borra la frecuencia sintonizada recordada, por lo que el siguiente clic siempre inicia un nuevo ciclo de sintonización.

Los botones **ATU** y **MEM** están deshabilitados cuando TGXL se encuentra en modo OPERATE.

## Consejos

- Observe los medidores **RF Pwr** y **SWR** en cuanto active MOX. Si el SWR supera 2.5 (zona roja), desactive inmediatamente y revise su sistema de antena.
- Establezca **RF Power** a un valor bajo antes de usar MOX por primera vez en una nueva banda.
- MOX transmite el radio a plena potencia en cualquier modo que esté activo. Si solo necesita verificar el SWR o sintonizar un ATU, use **TUNE** en su lugar — transmite una portadora al nivel inferior de **Tune Pwr**.
- Tras una sintonización exitosa del ATU, hacer clic en **ATU** nuevamente en la misma frecuencia pone el sintonizador en bypass. Para resintonizar tras cambiar de banda o frecuencia, simplemente haga clic en **ATU** una vez en la nueva frecuencia.

## Solución de problemas

- **El botón MOX no responde** — Confirme que AetherSDR está conectado al radio. El applet TX Controls requiere una conexión activa con el radio.
- **El transmisor se activa pero no se muestra potencia RF** — Verifique que **RF Power** no esté en 0 y que el perfil TX correcto esté cargado en el selector **TX Profile**.
- **El radio permanece en transmisión después de hacer clic en MOX por segunda vez** — Otra fuente PTT (pedal de pie, VOX, comando CAT) puede estar manteniendo el radio clavado. Revise el hardware PTT externo y cualquier cliente CAT conectado.
- **El botón ATU inicia una nueva sintonización en lugar de pasar a bypass** — La frecuencia de transmisión ha cambiado desde la última sintonización exitosa. El botón ATU siempre iniciará un nuevo ciclo de sintonización cuando la frecuencia difiera de aquella en la que el sintonizador reportó por última vez una coincidencia exitosa.

## Relacionados

- [Descripción general de TX Controls](overview.md)
- [Iniciar una portadora de sintonización para verificar el SWR](start-a-tune-carrier-to-check-swr.md)
- [Configurar la potencia de salida RF](set-rf-output-power.md)
- [Usar el ATU interno](run-the-internal-atu.md)
- [Realizar su primer QSO con AetherSDR](../../getting-started/tutorials/first-qso.md)
