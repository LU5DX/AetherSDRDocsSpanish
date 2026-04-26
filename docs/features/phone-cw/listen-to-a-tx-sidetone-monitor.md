# Escuchar el monitor de sidetone de TX

El applet Phone/CW proporciona dos formas independientes de monitorear el audio transmitido: un monitor de banda lateral del lado del radio (modos Phone) y un monitor de sidetone CW del lado del radio (modo CW). Utilícelos para escuchar su propia señal durante la transmisión sin depender de rutas de audio externas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Phone/CW solo funciona cuando hay una conexión de radio activa.
- El applet P/CW debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón de bandeja **P/CW** en la barra lateral derecha para abrirlo.
- Confirme en qué modo se encuentra el slice activo. El applet muestra automáticamente el panel Phone en modos de voz y el panel CW en modo CW.

## Pasos

### Modos Phone (SSB, AM, FM)

1. Abra el applet **P/CW** desde la barra lateral derecha.
2. Confirme que se muestra el panel Phone (no el panel CW).
3. Haga clic en **MON** para activar el monitor de banda lateral. El botón se ilumina cuando está activo.
4. Arrastre el control deslizante **Monitor volume** para ajustar el nivel del monitor. Rango válido: 0–100.

### Modo CW

1. Abra el applet **P/CW** desde la barra lateral derecha.
2. Confirme que se muestra el panel CW. Si el slice activo está en un modo CW, el applet cambia a él automáticamente.
3. Haga clic en **Sidetone** para activar el monitor de sidetone CW del radio. El botón se ilumina cuando está activo.
4. Arrastre el control deslizante **Sidetone volume** para ajustar el nivel del monitor. Rango válido: 0–100.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|---|
| **MON** | Botón de alternancia | — | On / Off | — | Activa el monitor de banda lateral para los modos Phone. |
| **Monitor volume** | Control deslizante | — | 0–100 | — | Ajusta el volumen del monitor de banda lateral. |
| **Sidetone** | Botón de alternancia | — | On / Off | — | Activa el monitor de sidetone CW del radio. |
| **Sidetone volume** | Control deslizante | — | 0–100 | — | Ajusta el volumen del monitor CW. |

## Consejos

- El monitor de sidetone CW del lado del radio enruta el audio a través de la ruta DAX del radio. Si necesita menor latencia (aproximadamente 10 ms) para trabajar con paddle, manipulador recto o CWX, utilice en su lugar el sidetone **Local STn** del lado del cliente. Consulte [Activar el sidetone CW local de baja latencia (Local STn) para trabajo rápido con paddle / manipulador recto / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md).
- **MON** y **Sidetone** son controles separados en paneles distintos. Activar uno no afecta al otro.

## Relacionados

- [Activar el sidetone CW local de baja latencia (Local STn) para trabajo rápido con paddle / manipulador recto / CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Cambiar el tono CW / frecuencia de sidetone](change-cw-pitch-sidetone-frequency.md)
- [Ajustar el volumen del sidetone local independientemente del monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
