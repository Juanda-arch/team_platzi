# FASE 2 — DISEÑO
**Líder de fase:** Diego
**Insumo de entrada:** backlog priorizado y matriz de riesgos de la Fase 1.

## 8. Modelo de arquitectura

Aunque el proyecto no requiere programación en código, sí exige que el equipo demuestre que entiende cómo encajaría la app dentro del ecosistema real de Platzi (integración obligatoria con web, app y LMS, según el caso). Se define una arquitectura en 4 capas:

1. **App móvil (cliente)** — el prototipo navegable de alta fidelidad, sin lógica de negocio real.
2. **API Gateway / BFF** — capa que orquestaría las llamadas hacia los servicios, punto único de entrada.
3. **Servicios nuevos**: Progreso académico (avance y rutas activas), Suscripción Expert (simulador de renovación), Notificaciones (alertas de vencimiento).
4. **Sistemas existentes de Platzi**: LMS y catálogo (cursos y rutas activas), Suscripciones (billing y renovaciones), Autenticación (login y sesión).

La app **nunca inventa datos de suscripción o certificación**: siempre los consulta desde los sistemas existentes de Platzi, cumpliendo la restricción del caso de no alterar precios ni beneficios reales. (Diagrama de arquitectura mostrado arriba en la conversación.)

## 9. Diagramas de actividad

Se modela el flujo de mayor impacto en el objetivo de negocio (reducir churn): la alerta de vencimiento con simulador de renovación (diagrama mostrado arriba), que conecta HU-08, HU-10 y HU-12.

**Flujo complementario — primer uso del estudiante (onboarding a la ruta):**
1. Estudiante inicia sesión (reutiliza autenticación existente de Platzi).
2. La app consulta su ruta activa en el LMS.
3. Se muestra el resumen de progreso (HU-01) y el calendario de próximas clases (HU-04).
4. Si hay una entrega o evaluación próxima (≤7 días), se destaca en la pantalla principal (HU-05, HU-06).
5. Si el estudiante lleva 5+ días sin actividad, se dispara un mensaje educativo de hábitos de estudio (HU-09).

Este segundo flujo no se diagrama gráficamente en esta entrega por ser secuencial y lineal (sin decisiones), pero debe documentarse igual en el entregable final como evidencia de trazabilidad.

## 10. Diseño de base de datos (modelo conceptual)

No se implementa base de datos real (restricción del proyecto), pero se define el modelo conceptual que sustenta los datos mostrados en el prototipo, para justificar de dónde saldría cada dato si se llevara a producción:

| Entidad | Atributos clave | Relación |
|---|---|---|
| `Estudiante` | id, nombre, email, fecha_registro | 1 — N con `Suscripcion`, `Progreso` |
| `RutaAprendizaje` | id, nombre, descripción | 1 — N con `Curso` |
| `Curso` | id, nombre, ruta_id, estado | N — 1 con `RutaAprendizaje`; 1 — N con `Progreso` |
| `Progreso` | id, estudiante_id, curso_id, porcentaje_avance, fecha_actualizacion | N — 1 con `Estudiante` y `Curso` |
| `ClaseEnVivo` | id, curso_id, fecha, tipo (Platzi Live) | N — 1 con `Curso` |
| `Entrega` | id, curso_id, estudiante_id, fecha_limite, estado | N — 1 con `Curso` y `Estudiante` |
| `Evaluacion` | id, curso_id, estudiante_id, fecha_limite, estado | N — 1 con `Curso` y `Estudiante` |
| `Suscripcion` | id, estudiante_id, tipo (Expert), fecha_inicio, fecha_vencimiento, estado | N — 1 con `Estudiante` |
| `Notificacion` | id, estudiante_id, tipo, fecha_envio, leida | N — 1 con `Estudiante` |
| `Certificacion` | id, estudiante_id, curso_id, fecha_emision, id_validacion | N — 1 con `Estudiante` y `Curso` |

Este modelo es la base para que Implementación (Nicolás) sepa qué datos ficticios necesita poblar en el prototipo, y para que Pruebas (Hugo Alejandro) valide que cada pantalla muestra información consistente con estas entidades.

## 11. Prototipo de interfaz (mapa de pantallas)

| Pantalla | Épica / Historias que cubre | Elementos clave |
|---|---|---|
| Inicio / Resumen de progreso | E1 (HU-01, HU-15) | Barra de avance por ruta, próxima acción recomendada |
| Detalle de curso | E1 (HU-02, HU-03) | Estado de lecciones, certificado si aplica |
| Calendario | E2 (HU-04, HU-05, HU-06) | Vista semanal con clases en vivo, entregas y evaluaciones |
| Notificaciones | E3 (HU-07, HU-08, HU-09) | Historial de alertas, configuración de frecuencia |
| Suscripción / Platzi Expert | E4 (HU-10, HU-11, HU-12) | Fecha de renovación, comparativa de beneficios, simulador |
| Perfil / Cuenta | Transversal | Datos del estudiante, acceso a certificaciones |

**Criterios de diseño a respetar (definidos en Análisis, sección 3.3 RNF):**
- Máximo 3 toques para llegar a cualquier función clave (RNF-03).
- Todo texto de beneficios de suscripción debe salir de la guía de contenido validada por Legal (mitigación R-02/R-04), no redactarse libremente en esta fase.
- Datos mostrados en el prototipo deben ser ficticios/anonimizados (mitigación R-09).

## 12. Handoff a Fase 3 (Implementación — Nicolás)

- Mapa de pantallas (sección 10) como guía de los mockups navegables a construir.
- Modelo de entidades (sección 9) para poblar datos ficticios consistentes entre pantallas.
- Arquitectura de referencia (sección 7) para justificar, en la documentación, cómo se integraría con los sistemas reales de Platzi.

