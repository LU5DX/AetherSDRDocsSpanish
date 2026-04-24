---
title: Acerca de esta documentación
description: Cómo se construye la documentación de AetherSDR, el pipeline de IA detrás de ella y cómo podés apoyar el proyecto.
---

# Acerca de esta documentación

## Construida para una aplicación seria

AetherSDR no es un proyecto de fin de semana. Está construido con **C++20 y Qt6** desde el primer día — la mejor tecnología disponible para una aplicación que exige rendimiento DSP en tiempo real, baja latencia y comportamiento nativo multiplataforma en Linux, macOS y Windows. Ese nivel de ingeniería merece una documentación que esté a la altura.

Creo que la documentación es un componente de primera clase en cualquier proyecto de software — no algo que se agrega como afterthought. Una buena documentación reduce la fricción para los nuevos usuarios, ayuda a los operadores experimentados a sacar el máximo provecho de cada función, y baja la barrera de entrada a un hobby que ya tiene una curva de aprendizaje suficientemente empinada.

---

## Un pipeline de documentación impulsado por IA

Este manual no se escribe página por página a mano. Es generado por un pipeline personalizado que construí para mantener el ritmo con las versiones de AetherSDR:

1. **Ingesta del código fuente** — con cada nueva versión, el pipeline descarga el código fuente C++ de AetherSDR directamente desde el repositorio.
2. **Análisis con IA** — un modelo de lenguaje de última generación escanea cada objeto orientado al usuario que expone la aplicación: ventanas, controles, menús, configuraciones y comportamientos.
3. **Salida de alta calidad** — el modelo produce documentación estructurada y precisa en lenguaje natural, cubriendo qué hace cada función, cómo usarla y las opciones de configuración relevantes.

El resultado es un manual vivo que evoluciona con el software — no un documento estático que queda desactualizado dos versiones después.

---

## Quimey — tu asistente de IA

Cada página de este sitio incluye a **Quimey**, un asistente de IA que podés abrir en cualquier momento haciendo clic en el botón de chat en la esquina inferior derecha.

Quimey está impulsado por **RAG — Generación Aumentada por Recuperación**. Esto es lo que significa en términos simples:

> En lugar de depender únicamente de lo que un modelo de lenguaje aprendió durante su entrenamiento, RAG primero *recupera* los pasajes más relevantes de una base de conocimiento real — en este caso, la documentación actual — y luego *genera* una respuesta fundamentada en ese contenido.

Esto significa que Quimey no inventa funciones que no existen ni describe comportamientos de una versión diferente del software. Sus respuestas están ancladas a la documentación actual de AetherSDR, con links a las fuentes para que puedas verificar todo lo que dice.

Por dentro:

- **Base de datos vectorial** — los fragmentos de documentación se indexan con embeddings para búsqueda semántica rápida
- **Embeddings Voyage AI** — representaciones vectoriales de texto de última generación para máxima precisión en la recuperación
- **Claude (Anthropic)** — el modelo de lenguaje que sintetiza el contexto recuperado en respuestas claras
- **Backend FastAPI** — desplegado en Railway para respuestas confiables y de baja latencia
- **Modo avanzado** — activá ⚙️ para buscar también en el código fuente de AetherSDR, no solo en los docs

Quimey mejora constantemente. Nueva documentación, mejor ajuste de la recuperación y prompts más inteligentes se incorporan en cada iteración.

---

## Open source, donde sea posible

Este proyecto se apoya en tecnología open source en cada capa:

| Componente | Tecnología |
|---|---|
| Sitio de documentación | [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) |
| Renderizado de markdown en el chat | [marked.js](https://marked.js.org/) + [DOMPurify](https://github.com/cure53/DOMPurify) |
| Base de datos vectorial | [ChromaDB](https://www.trychroma.com/) |
| Framework de API | [FastAPI](https://fastapi.tiangolo.com/) |
| Hosting | [GitHub Pages](https://pages.github.com/) (docs) + [Railway](https://railway.app/) (backend) |

---

## La infraestructura tiene costos reales

GitHub Pages hospeda la documentación de forma gratuita. Todo lo demás, no:

- **Base de datos vectorial** — embeddings ajustados y almacenamiento persistente para cada versión de AetherSDR
- **Llamadas a la API del LLM** — cada pregunta que responde Quimey tiene un costo en tokens
- **Embeddings Voyage AI** — la búsqueda semántica de calidad requiere una API de embeddings paga
- **Despliegue en Railway** — backend siempre disponible para el asistente

Si encontrás útil esta documentación — si te ahorró una hora de buscar en foros, o te ayudó a poner tu radio en el aire más rápido — tu apoyo genuinamente ayuda a mantener este sistema funcionando y a mejorarlo con el tiempo.

---

## Apoyá el proyecto

!!! tip "Cada contribución ayuda"
    Incluso una pequeña contribución compensa los costos de API e infraestructura, y motiva seguir mejorando tanto los docs como el asistente.

<div style="text-align:center; margin: 2rem 0;">
  <a href="https://ko-fi.com/lu5dx" class="md-button md-button--primary" target="_blank" rel="noopener" style="margin: 0.5rem;">
    ☕ Invitame un café
  </a>
  <a href="https://paypal.me/lu5dx599" class="md-button md-button--primary" target="_blank" rel="noopener" style="margin: 0.5rem;">
    💙 Donar por PayPal
  </a>
  <a href="https://github.com/LU5DX" class="md-button" target="_blank" rel="noopener" style="margin: 0.5rem;">
    ⭐ Star en GitHub
  </a>
</div>

---

*Pipeline de documentación y asistente de IA desarrollados por [LU5DX](https://github.com/LU5DX).*
*AetherSDR es desarrollado por [ten9876](https://github.com/ten9876/AetherSDR).*
