# Ágora: Sistema Interagéntico de Evaluación Ética y Auditoría Académica

Este repositorio constituye la base técnica y conceptual de una investigación en curso desarrollada por J. Víctor Faccio Lucero (UNRC) y Noemí Luján P. (UAM-X).

El sistema Ágora es una arquitectura orquestada de agentes de Inteligencia Artificial diseñada para asistir a la persona docente en la evaluación de la integridad académica bajo un enfoque constructivista. A diferencia de los detectores comerciales binarios, este sistema promueve la fricción productiva y la co-construcción de saberes mediante un proceso de debate y auditoría ética.

# 1. Estructura Epistemológica y Contextual

El "Por Qué" de este Desarrollo

La crisis epistemológica provocada por la irrupción de los Grandes Modelos de Lenguaje (LLMs) demanda soluciones que no caigan en el determinismo tecnológico. Los detectores tradicionales fallan sistemáticamente al procesar el español latinoamericano y son incapaces de distinguir el ensamblaje modular del trabajo colaborativo humano de la generación sintética.

Ágora no emite veredictos automáticos. Su propósito es proveer evidencia estructurada para la sesión de réplica, garantizando la validez pedagógica y legal en entornos universitarios al mantener siempre a la persona docente como el centro de la decisión final (Human-In-The-Loop - HITL).

## 2. Arquitectura Técnica Low-Code

El sistema opera como un pipeline de procesamiento secuencial de nodos. La orquestación puede realizarse en plataformas como n8n, Make o Copilot Studio.

graph TD
    A[Ingesta: Texto + Notas Docentes + Perfil] --> B[Nodo 1: Cicerón]
    B --> C[Nodo 2: Séneca]
    C --> D[Nodo 3: Hortensia]
    D --> E[Salida: Dictamen Integrado + Banco de Preguntas]
    E --> F[Sesión de Réplica Oral]

### Los Agentes del Ágora

Cicerón (Analista Forense): Genera la ficha de identificación (título, integrantes, anexos). Analiza la estilometría buscando falta de ráfaga (burstiness), muletillas algorítmicas y colapso deíctico.

Séneca (Auditor Bibliográfico): Con la función de grounding activa, busca en Google Scholar los títulos o DOIs de la bibliografía para identificar fuentes reales o alucinaciones sintéticas.

Hortensia (Contextualizadora Ética): Refuta las anomalías detectadas por Cicerón. Identifica las notas docentes (mayúsculas, comentarios intercalados) para evitar que se procesen como ruido y defiende el proceso humano frente al "impuesto neurotípico".

Resiliencia Técnica: Manejo de Ruido

El sistema posee una instrucción específica para identificar e ignorar (o integrar pedagógicamente) las intervenciones de la persona docente dentro del documento (texto en MAYÚSCULAS, notas en otros colores o comentarios). Esto permite procesar borradores reales con retroalimentación previa sin contaminar el análisis forense.

## 3. Reproducibilidad y Colaboración


Carga de JSON: Importar los archivos agent_ciceron.json, agent_seneca.json y agent_hortensia.json en los nodos respectivos de la plataforma low-code.

Definición de Variables: Configurar la inyección de {{texto_estudiante}}, {{notas_docente}} y {{modelo_educativo}}.

Concatenación: Asegurar que la salida del Nodo 1 (Cicerón) alimente el contexto de los nodos subsecuentes.

Escalabilidad Institucional

Para adaptar Ágora de la UAM-X a la UNRC o cualquier otra institución, sólo es necesario modificar el contexto pedagógico en el payload de la variable {{modelo_educativo}}. La arquitectura de agentes permanece intacta.
