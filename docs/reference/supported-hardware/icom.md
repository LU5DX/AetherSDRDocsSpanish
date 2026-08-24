---
title: Icom en red
---

# Icom en red

!!! warning "Experimental / temprano"
    El soporte de Icom en red está en una etapa **temprana** — todavía no es una
    familia de radio soportada. Solo el IC-705 y el IC-7300MK2 están verificados
    contra sus propias guías CI-V. Un modelo no reconocido conecta **sin scope y
    sin transmisión**, en lugar de usar valores predeterminados optimistas.

AetherSDR habla con radios Icom en red (IC-705, IC-7300MK2, IC-9700) sobre el
**transporte UDP de RS-BA1**, que transporta comandos **CI-V**. La radio ejecuta
el software RS-BA1 de Icom; AetherSDR es el cliente.

## Conexión

1. Inicia **RS-BA1** en la red y confirma que la radio es accesible.
2. Abre **Conectar a Radio** y elige el tipo de radio manual **Icom (red)**.
3. Ingresa el host, el usuario y los puertos, más la contraseña (guardada en el
   **llavero del sistema operativo**, nunca en el archivo de configuración).
4. La ruta de conexión **le pregunta a la radio su propia dirección CI-V** en
   lugar de asumir una — de modo que la dirección correcta se autodetecta.

## Qué funciona

- **IC-705** — recepción, scope, transmisión y FT8.
- **IC-7300MK2** — controles, medidores, ATU, transmisión WSPR, enrutamiento de
  PC Audio y el decodificador de CW (completado contra hardware real).
- **IC-9700** — parcial (recuperación CI-V, modo FM-D, límites de potencia por
  banda).
- **Un planificador de comandos CI-V** — cada lectura de medidor, escritura de
  control y transición de PTT pasa por un plano de comandos ordenado con ranuras
  de 25 ms.
- **Perfiles de capacidades basados en evidencia** — el comportamiento del
  IC-705, IC-7300MK2 e IC-9700 se describe con perfiles tipados que fallan de
  forma segura para radios desconocidas.
- **Tono de repetidor FM, dúplex, offset y XFC momentáneo**.
- **Filtros RX reales** — el ancho de FI real de la radio, PBT gemelo y cortes de
  TX.
- **Teclado de CW por texto CI-V** (CWK).
- **Transmisión WSPR** desde la radio (confirmada al aire).
- **Modos DATA** (DIGU/DIGL/FM-D) llegan a la radio correctamente.
- **Enrutamiento de PC Audio** — cambia solo la entrada de modulación DATA OFF
  específica del modelo, y solo con un clic del operador.
- **Salud de la radio** — los registros de salud/estado que reporta la radio se
  muestran en Ayuda ▸ Salud de la radio….

## En qué se diferencia de FlexRadio

- **Sin IQ / sin scope en la mayoría de los modelos:** ningún Icom en red emite
  muestras, por lo que no hay ruta DAX/IQ y el espectro no lo genera la radio.
- **La radio es dueña del modulador:** la radio modula a partir del audio PCM que
  tu computadora envía; el host no modula.
- **La radio es dueña de su estado:** un Icom recuerda su propia frecuencia, modo
  y filtro entre ciclos de encendido, por lo que AetherSDR nunca empuja un estado
  restaurado.

## Limitaciones

- Etapa temprana; solo IC-705 e IC-7300MK2 están completamente verificados.
- Sin flujos DAX/IQ (ningún Icom en red produce muestras).
- La renovación del arrendamiento de RS-BA1 debe mantenerse sana — si el
  arrendamiento de medios falla, el panadapter se congela (esto está manejado,
  pero mantén RS-BA1 en ejecución).

Consulta [Hardware compatible](index.md) para el panorama completo.
