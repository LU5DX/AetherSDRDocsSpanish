---
title: Apoye la Documentación
description: Cómo se construye la documentación de AetherSDR, el proceso de IA detrás de ella y cómo puede apoyar el proyecto.
---

# Apoye la Documentación

!!! tip "Cada contribución ayuda"
    Si esta documentación le ahorró tiempo o le ayudó a poner su radio en el aire más rápido, su apoyo mantiene el sistema en funcionamiento y ayuda a mejorar el asistente.

<div style="text-align:center; margin: 1.5rem 0;">
  <a href="https://ko-fi.com/lu5dx" class="md-button" target="_blank" rel="noopener" style="margin: 0.3rem; font-size: 0.82rem;">
    ☕ Invíteme un café
  </a>
  <a href="https://paypal.me/lu5dx599" class="md-button" target="_blank" rel="noopener" style="margin: 0.3rem; font-size: 0.82rem;">
    💙 Done vía PayPal
  </a>
  <a href="https://github.com/LU5DX" class="md-button" target="_blank" rel="noopener" style="margin: 0.3rem; font-size: 0.82rem;">
    ⭐ Marcar estrella en GitHub
  </a>
</div>

---

## Construido para una aplicación seria

AetherSDR no es un proyecto de fin de semana. Está construido con **C++20 y Qt6** desde el primer día, la mejor tecnología disponible para una aplicación que exige rendimiento DSP en tiempo real, baja latencia y un comportamiento nativo multiplataforma en Linux, macOS y Windows. Ese nivel de ingeniería merece una documentación acorde.

Creo que la documentación es un componente de primera clase de cualquier proyecto de software, no algo secundario. Una buena documentación reduce la fricción para los nuevos usuarios, ayuda a los operadores experimentados a aprovechar al máximo cada función y reduce la barrera de entrada para un pasatiempo que ya tiene una curva de aprendizaje bastante pronunciada.

---

## Un proceso de documentación impulsado por IA

Este manual no está escrito a mano página por página. Es generado por un proceso personalizado que construí para mantener el ritmo de las versiones de AetherSDR:

1. **Ingesta del código fuente**: con cada nueva versión, el proceso extrae el código fuente C++ de AetherSDR directamente del repositorio.
2. **Análisis mediante IA**: un modelo de lenguaje extenso examina cada objeto expuesto al usuario por la aplicación: ventanas, controles, menús, configuraciones y comportamientos.
3. **Resultado de alta calidad**: el modelo produce documentación estructurada y precisa en inglés natural, cubriendo qué hace cada función, cómo usarla y las opciones de configuración relevantes.

El resultado es un manual vivo que evoluciona con el software, no un documento estático que queda obsoleto tras dos versiones.

---

## Athena — su asistente de IA

Cada página de este sitio incluye a **Athena**, un asistente de IA que puede abrir en cualquier momento haciendo clic en el botón de chat en la esquina inferior derecha.

Athena funciona con **RAG — Generación Aumentada por Recuperación**. Esto es lo que significa en lenguaje sencillo:

> En lugar de depender únicamente de lo que un modelo de lenguaje aprendió durante el entrenamiento, RAG primero *recupera* los pasajes más relevantes de una base de conocimiento real —en este caso, la documentación real— y luego *genera* una respuesta basada en ese contenido.

Esto significa que Athena no inventa funciones que no existen ni describe comportamientos de una versión diferente del software. Sus respuestas están ancladas en la documentación actual de AetherSDR, con enlaces a las fuentes para que usted pueda verificar todo lo que dice.

Internamente:

- **Base de datos vectorial**: los fragmentos de documentación se incrustan y almacenan para una búsqueda semántica rápida
- **Incrustaciones Voyage AI**: incrustaciones de texto de última generación para precisión en la recuperación
- **Claude (Anthropic)**: el modelo de lenguaje que sintetiza el contexto recuperado en respuestas claras
- **Backend FastAPI**: desplegado en Railway para respuestas fiables y de baja latencia
- **Modo avanzado**: active ⚙️ para buscar también en el código fuente de AetherSDR, no solo en la documentación

Athena mejora continuamente. Nueva documentación, mejor ajuste de la recuperación y avisos más inteligentes se envían con cada iteración.

---

## Código abierto, siempre que sea posible

Este proyecto se apoya en el código abierto en cada capa:

| Componente | Tecnología |
|---|---|
| Sitio de documentación | [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) |
| Renderizado Markdown en el chat | [marked.js](https://marked.js.org/) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| Almacén vectorial | [ChromaDB](https://www.trychroma.com/) |
| Marco de trabajo API | [FastAPI](https://fastapi.tiangolo.com/) |
| Alojamiento | [GitHub Pages](https://pages.github.com/) (docs) + [Railway](https://railway.app/) (backend) |

---

## La infraestructura tiene costos reales

GitHub Pages aloja la documentación de forma gratuita. Todo lo demás no:

- **Base de datos vectorial**: incrustaciones ajustadas y almacenamiento persistente para cada versión de AetherSDR
- **Llamadas a la API del modelo de lenguaje**: cada pregunta que responde Athena tiene un costo en tokens
- **Incrustaciones Voyage AI**: la búsqueda semántica de alta calidad requiere una API de incrustaciones de pago
- **Despliegue en Railway**: backend siempre activo para el asistente

Si encuentra útil esta documentación, si le ahorró una hora buscando en foros o le ayudó a poner su radio en el aire más rápido, su apoyo realmente ayuda a mantener este sistema en funcionamiento y lo mejora con el tiempo.

---

*Proceso de documentación y asistente de IA creados por [LU5DX](https://github.com/LU5DX).*
*AetherSDR es desarrollado por [ten9876](https://github.com/ten9876/AetherSDR).*
