# Escuchar el monitor de tono lateral (sidetone) de TX

AetherSDR ofrece dos rutas separadas de monitor de tono lateral: un monitor en el lado del radio (disponible en los modos Phone y CW) y un tono lateral local de baja latencia en el lado del cliente para CW (con aproximadamente 10 ms de latencia). Esta página cubre ambas opciones para que pueda escuchar su propio audio transmitido mientras opera.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El applet Phone/CW requiere una conexión de radio activa.
- Abra el panel de applets. Si no está visible, haga clic en View > Applet Panel.

## Pasos

### Modo Phone: activar el monitor de banda lateral

1. Haga clic en el botón P/CW de la barra lateral derecha para abrir el applet Phone/CW.
2. Confirme que el applet muestra el panel Phone (el slice activo debe estar en un modo de voz como SSB o AM).
3. Haga clic en MON para activar el monitor de banda lateral de TX. El botón se resalta cuando está activo.
4. Ajuste el control deslizante Monitor volume para establecer el nivel de reproducción (0–100).

### Modo CW: activar el monitor de tono lateral del radio

1. Cambie el slice activo al modo CW. El applet muestra automáticamente el panel CW.
2. Haga clic en Sidetone para activar el monitor CW del radio alimentado por DAX. El botón se resalta cuando está activo.
3. Ajuste el control deslizante Sidetone volume para establecer el nivel (0–100).

### Modo CW: activar el tono lateral local de baja latencia

1. En el panel CW, haga clic en Local STn para activar el generador de tono lateral en el lado del cliente. El botón se resalta cuando está activo.
2. Ajuste el control deslizante Local sidetone volume para establecer el nivel (0–100; valor predeterminado 50).
3. Para controlar el tono:
   - Deje Follow activado (predeterminado) para que el tono local siga automáticamente la configuración de tono CW del radio.
   - Haga clic en Follow para desactivarlo y luego use el control deslizante Local sidetone pitch para establecer un tono manual (100–2000 Hz; predeterminado 600 Hz).

## Qué hace cada control

| Control | Función | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| MON | Activa el monitor de banda lateral de TX (panel Phone). | — | On / Off | — |
| Monitor volume | Establece el nivel de reproducción del monitor de banda lateral. | — | 0–100 | — |
| Sidetone | Activa el monitor CW del radio alimentado por DAX (panel CW). | — | On / Off | — |
| Sidetone volume | Establece el nivel de reproducción del monitor CW del radio. | — | 0–100 | — |
| Local STn | Activa el tono lateral CW de baja latencia en el lado del cliente (~10 ms). | Off | On / Off | `CwLocalSidetoneEnabled` |
| Local sidetone volume | Establece el nivel de reproducción del tono lateral local, independientemente del monitor del radio. | 50 | 0–100 | `CwLocalSidetoneVolume` |
| Follow | Cuando está activado, el tono del tono lateral local sigue el tono CW del radio. Cuando está desactivado, se habilita el control deslizante de tono manual. | On | On / Off | `CwLocalSidetonePitchFollow` |
| Local sidetone pitch | Ajuste manual del tono del tono lateral local (solo activo cuando Follow está desactivado). | 600 Hz | 100–2000 Hz | `CwLocalSidetonePitchHz` |

## Consejos

- El tono lateral del radio (botón Sidetone, panel CW) se enruta a través de DAX y tiene mayor latencia que el tono lateral local. Si nota un eco o retardo al manipular, use Local STn en su lugar.
- Local STn funciona con manipulación de paleta, manipulador recto y transmisiones generadas por CWX, por lo que puede usarse independientemente de cómo manipule el radio.
- Las dos rutas de monitor CW (Sidetone y Local STn) son independientes. Puede usar ambas simultáneamente o solo una de ellas.
- El botón MON y el botón Sidetone son controles separados en paneles distintos. MON se aplica a los modos de voz; Sidetone se aplica al modo CW.

## Solución de problemas

- **El botón MON o Sidetone no tiene efecto** — Confirme que el radio está conectado y que el modo del slice activo coincide con el panel que se muestra (Phone o CW). El applet cambia de panel automáticamente según el modo del slice activo.
- **Local STn no produce audio** — Verifique que la salida de audio del sistema esté configurada correctamente. El tono lateral local es generado en el lado del cliente por AetherSDR; no depende del enrutamiento de audio del radio.
- **El tono del tono lateral local no cambia al mover el control deslizante Local sidetone pitch** — Confirme que Follow está desactivado. Mientras Follow está activado, el control deslizante de tono está deshabilitado y el tono es controlado por la configuración de tono CW del radio.

## Relacionados

- [Activar el tono lateral CW local de baja latencia (Local STn) para paleta rápida, manipulador recto o trabajo con CWX](enable-the-low-latency-local-cw-sidetone-local-stn-for-fast-paddle-straight-key-cwx-work.md)
- [Ajustar el volumen del tono lateral local independientemente del monitor del radio](set-the-local-sidetone-volume-independently-of-the-radio-monitor.md)
- [Hacer que el tono del tono lateral local siga el tono CW del radio, o establecerlo manualmente con el control deslizante](make-the-local-sidetone-pitch-follow-the-radio-s-cw-pitch-or-set-it-manually-with-the-slider.md)
- [Cambiar la frecuencia del tono CW / tono lateral](change-cw-pitch-sidetone-frequency.md)
