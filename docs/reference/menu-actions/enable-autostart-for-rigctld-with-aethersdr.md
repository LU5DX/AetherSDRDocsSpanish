# Habilitar el inicio automático de rigctld con AetherSDR

Cuando esta configuración está habilitada, AetherSDR inicia automáticamente un servidor CAT rigctld cada vez que se abre la aplicación. Esto permite que los programas de registro y otro software externo utilicen la interfaz Hamlib rigctld sin necesidad de iniciarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar instalado y poder conectarse a su radio Flex.
- rigctld debe estar instalado y ser accesible en el PATH de su sistema.

## Pasos

1. Haga clic en `Settings` en la barra de menú.
2. Haga clic en `Autostart rigctld with AetherSDR`.

El elemento de menú es un interruptor seleccionable. Una marca de verificación junto a la etiqueta indica que la configuración está activa. La preferencia se guarda en `AutoStartRigctld` y persiste entre reinicios.

Para deshabilitar el inicio automático, repita los mismos pasos. La marca de verificación se eliminará y rigctld dejará de iniciarse al abrir la aplicación.

## Consejos

- Si también utiliza puertos serie virtuales para el control CAT, consulte [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md) — ambas funciones sirven para casos de uso distintos y pueden utilizarse de forma independiente o conjunta.
- Los cambios surten efecto en el siguiente inicio de la aplicación. Activar o desactivar la configuración no inicia ni detiene un proceso rigctld que ya esté en ejecución.

## Solución de problemas

- **rigctld no se inicia al abrir la aplicación** — Confirme que rigctld está instalado y disponible en el PATH de su sistema. AetherSDR no incluye rigctld; debe instalarse por separado (generalmente a través del paquete Hamlib de su distribución).
- **La marca de verificación desaparece después de reiniciar** — Verifique que AetherSDR tenga acceso de escritura al almacenamiento de configuraciones. Si la aplicación no puede guardar la configuración, `AutoStartRigctld` volverá a su estado predeterminado sin marcar.

## Relacionado

- [Habilitar el inicio automático de CAT con AetherSDR](enable-autostart-for-cat-with-aethersdr.md)
- [Habilitar el inicio automático de TCI con AetherSDR](enable-autostart-for-tci-with-aethersdr.md)
- [Habilitar el inicio automático de DAX con AetherSDR](enable-autostart-for-dax-with-aethersdr.md)
- [Primeros pasos](getting-started.md)
