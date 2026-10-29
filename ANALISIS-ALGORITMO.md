# Análisis del algoritmo de Pausa

## 1. Qué mide el prototipo

Pausa contiene nueve afirmaciones propias sobre ánimo, interés, desesperanza, tensión, preocupación, relajación, energía, sobrecarga e interferencia cotidiana, más una pregunta opcional de seguridad. Las cuatro respuestas registran frecuencia percibida durante las últimas dos semanas.

Esto **no es el WHO-5, PHQ-9 ni GAD-7**, ni una traducción/adaptación validada de esas escalas. El WHO-5 oficial, por ejemplo, tiene cinco afirmaciones positivas y seis opciones de respuesta; mide bienestar subjetivo. Cambiar sus ítems o su escala cambia el instrumento y no permite heredar su validación. [Ficha del WHO-5 de la OMS](https://www.who.int/publications/m/item/WHO-UCN-MSD-MHE-2024.01).

## 2. Espacio de combinaciones

- Nueve respuestas principales con cuatro opciones cada una: `4^9 = 262.144` perfiles completos.
- La pregunta opcional de seguridad tiene cinco estados (sin respuesta y cuatro frecuencias): `262.144 × 5 = 1.310.720` estados posibles en total.
- Las nueve respuestas principales generan `9 × 8 / 2 = 36` parejas distintas.
- Cada pareja puede tomar `4 × 4 = 16` combinaciones, es decir, `36 × 16 = 576` estados de pareja.

No conviene redactar 1.310.720 mensajes a mano: eso sería frágil e incoherente. El algoritmo interpreta todas las combinaciones con reglas compartidas, conserva la respuesta exacta a cada ítem y arma una devolución específica con las áreas y parejas más relevantes.

## 3. Estructura usada

| Área descriptiva | Ítems | Cómo se resume |
| --- | --- | --- |
| Ánimo e interés | Ánimo bajo, pérdida de interés, desesperanza/baja valoración | Cuenta cuántas respuestas quedaron en las dos opciones de mayor frecuencia; conserva también la respuesta individual más alta |
| Preocupación y tensión | Nerviosismo/tensión, preocupación difícil de detener, dificultad para relajarse | Mismo conteo descriptivo |
| Energía y sobrecarga | Poca energía, sentirse sobrepasado/a | Mismo conteo descriptivo |
| Interferencia cotidiana | Sueño, concentración, estudio, trabajo o relaciones | Se conserva aparte; no se mezcla con las áreas anteriores |
| Seguridad | Pensamientos de no querer estar o hacerse daño | Se conserva aparte y activa orientación de apoyo; nunca reduce ni aumenta una etiqueta diagnóstica |

Los conteos solo ordenan las respuestas del demo: no son baremos, puntos de corte ni niveles clínicos. Usar conteos y conservar cada frecuencia evita suponer que la distancia entre las categorías de respuesta sea igual. Se eliminó el doble conteo de la energía, que en la versión anterior influía a la vez en dos áreas.

## 4. Análisis de parejas

Para cada perfil se recorren las 36 parejas entre las nueve respuestas principales. Cada pareja se clasifica en tres relaciones descriptivas:

- **Coincidencia frecuente:** ambas respuestas tienen valor 2 o 3 (“Más de la mitad de los días” o “Casi todos los días”).
- **Coincidencia:** ambas respuestas son mayores que cero. La devolución conserva sus frecuencias exactas.
- **Diferencia de frecuencia:** los valores difieren en dos o más puntos; el resultado las describe por separado.

Algunas parejas comparten un tema comprensible para el usuario: ánimo bajo con pérdida de interés/desesperanza; tensión con preocupación/dificultad para relajarse; y poca energía con sobrecarga. Las demás parejas se describen como respuestas que coexisten o difieren, sin atribuirles una relación psicológica validada. La pareja destacada se ordena por coincidencia frecuente, relación temática y frecuencia marcada.

La interferencia cotidiana se analiza como contexto: si aparece a menudo, la devolución lo menciona; si aparece algunos días, sugiere observar cuándo ocurre; si se marcó “Nunca”, señala que esa respuesta no invalida las demás.

## 5. Seguridad y límites

Una respuesta positiva a la pregunta opcional de seguridad no se interpreta como una evaluación de riesgo ni como prueba de intención. El texto indica que el demo no puede valorar inmediatez y ofrece buscar apoyo humano. Una respuesta “Nunca” o una omisión tampoco se tratan como prueba de ausencia de riesgo.

Incluso cuestionarios con validación clínica se usan como apoyo de detección, no como diagnóstico automático. La OMS describe el WHO-5 como medida de bienestar; el PHQ-9 y el GAD-7 son instrumentos distintos con ítems, puntuación y evidencia propios. Para un diagnóstico hacen falta evaluación clínica y contexto, no solo una combinación de casillas. [OMS: WHO-5](https://www.who.int/publications/m/item/WHO-UCN-MSD-MHE-2024.01) · [Estudio original del GAD-7](https://pubmed.ncbi.nlm.nih.gov/16717171/) · [Revisión sobre detección PHQ-9](https://pmc.ncbi.nlm.nih.gov/articles/PMC4995584/).

## 6. Qué significa “personalizado” en esta versión

El párrafo toma las respuestas más frecuentes, el área descriptiva dominante o mixta, la pareja más marcada, la interferencia cotidiana y el estado de la pregunta opcional. Cambia según el perfil, pero usa frases transparentes y reglas explícitas; **no hay un modelo generativo conectado ni inferencia de causas**.

Para presentarlo en clase: “Evaluamos combinaciones de respuesta con una matriz de interacciones y construimos una orientación descriptiva; la lógica es explicable y el contenido no pretende diagnosticar. El siguiente paso de una versión clínica sería elegir un instrumento validado, obtener revisión profesional y estudiar desempeño y seguridad con la población objetivo”.
