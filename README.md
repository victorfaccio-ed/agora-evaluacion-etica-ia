# Sistema Ágora: Sistema Interagéntico para Evaluación Ética de IA

Sistema de auditoría académica basado en flujos low-code y modelos de lenguaje de gran tamaño (LLMs) con enfoque Human-In-The-Loop (HITL).

## 📖 Descripción del Proyecto

Este repositorio contiene la configuración en JSON de un sistema multi-agente diseñado para asistir a las personas docentes en la evaluación de trabajos de investigación formativa. El objetivo del sistema no es "detectar plagio" de forma punitiva, sino generar un debate automatizado (acusación vs. defensa vs. verificación de hechos) que provea a la persona docente de un dictamen estructurado y un banco de preguntas para la defensa oral del estudiantado.

Diseñado inicialmente para auditar el Sistema Modular de la UAM-Xochimilco, el sistema está construido de forma modular. Puede ser desplegado en cualquier institución de educación superior (como la UNRC u otras universidades) simplemente modificando las variables de entorno inyectadas, adaptándose a cualquier metodología de investigación formativa.

## 🧠 Arquitectura de Agentes

El flujo de trabajo se compone de tres nodos agénticos (microservicios) que se ejecutan de manera secuencial:

### Cicerón (Analista Forense Lingüístico): }
Función: Analiza la estilometría, la coherencia temporal de la investigación y detecta "muletillas algorítmicas" o falta de ráfaga (burstiness). Extrae metadatos y crea la ficha de identificación inicial.

Configuración: agent_ciceron.json

### Hortensia (Contextualizadora Ética):

Función: Actúa como defensora. Duda activamente de Cicerón integrando variables pedagógicas (trabajo en equipo, iteraciones por comentarios docentes, neurodivergencias) para mitigar sesgos de los detectores de IA contra el español latinoamericano.

Configuración: agent_hortensia.json

### Séneca (Auditor Bibliográfico Neutral):

Función: Utiliza herramientas de búsqueda web (Grounding) para verificar la existencia real de las fuentes bibliográficas citadas por los estudiantes (DOIs, títulos, autores), detectando alucinaciones sintéticas.

Configuración: agent_seneca.json

## ⚙️ Implementación en Plataformas Low-Code

Este sistema está diseñado para ser implementado en plataformas de automatización (como Make, n8n, Microsoft Copilot Studio, Power Automate o LangChain).

Para que los agentes funcionen, el nodo disparador (trigger) debe inyectar las siguientes variables dinámicas en el payload de las llamadas a la API:

{{perfil_estudiante}}: Datos demográficos e integrantes del equipo.

{{modelo_educativo}}: Variable clave para la escalabilidad. Aquí se define si el agente evaluará bajo las reglas de la UAM-X, de la UNRC, o cualquier otro modelo de investigación formativa.

{{reporte_similitud}}: % de similitud de herramientas externas (ej. iThenticate, Turnitin).

{{texto_estudiante}}: El documento de investigación completo.

{{analisis_ciceron}}: Variable dinámica que pasa el análisis del Agente 1 al Agente 2.

## Parámetros de API Recomendados

Todos los agentes están optimizados para utilizar la API de Gemini 3 Pro con capacidades de razonamiento profundo.

Thinking Level: High (Vital para evitar alucinaciones lógicas).

Temperature: Variable (0.8 para forense, 0.9 para defensa, 0.2 para auditoría bibliográfica).

Max Output Tokens: 65536.

## 🧑‍🏫 Humano en el Bucle / Human in the Loop (HITL)

Este sistema es una herramienta de asistencia, no un juez automatizado. La salida final del orquestador es un Dictamen Preliminar consolidado. La decisión ética final recae exclusiva y obligatoriamente en la Persona Docente, quien utilizará los hallazgos y el "Banco de Preguntas" generado por los agentes para interrogar a los estudiantes en una sesión de réplica presencial o sincrónica.
