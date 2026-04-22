# Mezclar el realce Poo con Mix

El control **Poo / Mix** determina qué proporción de la señal de baja frecuencia procesada se mezcla de vuelta en el audio seco. Ajústelo para añadir solo el realce de graves necesario sin saturar la señal.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Consulte [Omitir PUDU de la cadena](bypass-pudu-from-the-chain.md) si el subcontenedor PUDU no está visible.
- El subcontenedor PUDU debe estar visible en el panel del applet. Si está oculto, haga doble clic en la etapa PUDU (Enh) en el widget CHAIN, o haga clic derecho en la barra de título del subcontenedor PUDU y seleccione la opción de mostrar.

## Pasos

1. Localice el grupo **Poo** en el subcontenedor PUDU. Es el grupo izquierdo de tres controles, identificado por la etiqueta de corchete **Poo** que aparece encima de ellos.
2. Encuentre el tercer control de ese grupo, etiquetado **Mix**.
3. Gire el control **Mix** hacia la derecha para aumentar la proporción de señal de baja frecuencia procesada en la salida, o hacia la izquierda para reducirla.
4. Observe el pulso de brillo del logotipo de PooDoo para confirmar el nivel de la señal húmeda. Un valor de **Mix** más alto produce un pulso más pronunciado.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Clave persistida |
|---|---|---|---|
| **Poo / Mix** | 30 % | 0 % a 100 % | `ClientPuduTxPooMix` |

El control utiliza un mapeo lineal. Con 0 %, el procesador Poo no tiene efecto sobre la salida. Con 100 %, la señal de bajas frecuencias procesada reemplaza completamente la contribución seca de la etapa Poo. Los valores entre 20 % y 40 % son adecuados para la mayoría de las aplicaciones de voz.

## Consejos

- Ajuste **Poo / Drive** y **Poo / Tune** antes de fijar un valor de **Mix**. Drive y Tune determinan lo que produce el procesador Poo; Mix solo controla qué proporción de ese resultado llega a la salida.
- Si los graves suenan pesados o retumbantes, reduzca **Mix** antes de reducir **Drive**. Los cambios en Mix son inmediatos y facilitan identificar el umbral en el que el realce se vuelve audible.
- En el modo **Even**, la etapa Poo utiliza saturación LF asimétrica. En el modo **Odd**, utiliza un compresor de graves con alimentación hacia adelante. El nivel apropiado de **Mix** puede diferir entre los dos modos.

## Relacionados

- [Ajustar Poo Drive para el grosor de bajas frecuencias](dial-poo-drive-for-lf-thickness.md)
- [Sintonizar Poo al fundamental de su voz](tune-poo-to-the-fundamental-of-your-voice.md)
- [Mezclar el realce Doo con Mix](blend-the-doo-excitement-with-mix.md)
- [Elegir el carácter Aphex (Even) o Behringer (Odd)](pick-aphex-even-vs-behringer-odd-character.md)
- [Omitir PUDU de la cadena](bypass-pudu-from-the-chain.md)
