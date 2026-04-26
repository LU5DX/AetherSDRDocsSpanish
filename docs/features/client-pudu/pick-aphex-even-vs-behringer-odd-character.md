# Seleccionar el carácter Aphex (Even) o Behringer (Odd)

El excitador PUDU ofrece dos algoritmos de modelado armónico. Cambiar entre ellos modifica el carácter tonal de los procesadores Poo (baja frecuencia) y Doo (alta frecuencia) de forma simultánea. Elija Even para un sonido más cálido, de linaje Aphex; elija Odd para un sonido más brillante, de linaje Behringer.

## Antes de comenzar

- La etapa PUDU debe estar habilitada en la cadena PooDoo Audio. Si el subcontenedor PUDU no está visible, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa PUDU (Enh) en el widget CHAIN para abrir el editor flotante de PUDU.
- El applet PUDU se encuentra dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice los dos botones etiquetados **Even** y **Odd** cerca de la parte superior del applet PUDU, debajo del logotipo de PooDoo.
2. Haga clic en **Even** para seleccionar el modelado asimétrico de linaje Aphex — predominantemente armónicos pares, más cálido, con saturación LF Big Bottom.
3. Haga clic en **Odd** para seleccionar el modelado simétrico tanh de linaje Behringer — armónicos impares puros, más brillante, con un compresor de graves de alimentación directa (feed-forward).

El botón seleccionado se resalta en ámbar. El cambio surte efecto de inmediato y se guarda en `ClientPuduTxMode`.

## Qué hace cada control

| Control | Comportamiento | Clave persistida |
|---------|----------------|------------------|
| **Even** | Selecciona el modelado asimétrico de linaje Aphex. Produce predominantemente armónicos pares con saturación LF Big Bottom. Exclusivo con **Odd**. | `ClientPuduTxMode` |
| **Odd** | Selecciona el modelado simétrico tanh de linaje Behringer. Produce armónicos impares puros con un compresor de graves feed-forward. Exclusivo con **Even**. | `ClientPuduTxMode` |

## Consejos

- El modo Even tiende a favorecer la voz e instrumentos cálidos; el modo Odd tiende a favorecer señales que necesitan más presencia y definición.
- Cambiar de modo no restablece ninguno de los controles de Poo o Doo, por lo que puede auditar ambos caracteres con los mismos ajustes de drive y mezcla para compararlos directamente.
- El logotipo de PooDoo pulsa con el nivel de señal procesada — obsérvelo mientras alterna entre modos para confirmar que el excitador está activo.

## Relacionado

- [Descripción general del excitador PUDU](overview.md)
- [Ajustar el Poo Drive para mayor grosor en baja frecuencia](dial-poo-drive-for-lf-thickness.md)
- [Añadir aire con los armónicos Doo](add-air-with-doo-harmonics.md)
- [Omitir PUDU desde la cadena](bypass-pudu-from-the-chain.md)
