# FASE 1 — ANÁLISIS
## Caso 3 — Platzi | App móvil de gestión de ruta de aprendizaje
**Líder de fase:** Juan David Buitrago
**Equipo:** Diego, Nicolás, Hugo Alejandro, Juan Sebastián

---

## 1. Introducción a la fase

Antes de diseñar cualquier pantalla, un equipo serio necesita entender **para quién** está construyendo, **qué dolor real** resuelve y **qué restricciones** no puede ignorar. Platzi ya identificó el síntoma (aumento de churn, confusión sobre beneficios, soporte saturado), pero no la causa raíz ni el alcance exacto. Esta fase convierte ese contexto de negocio en artefactos accionables para Diseño e Implementación.

**Entregables de esta fase (según el documento del docente):**
1. Identificación de stakeholders
2. Historias de usuario / requerimientos
3. Backlog priorizado
4. Matriz de riesgos inicial

---

## 2. Identificación de Stakeholders

Se clasifican por poder de decisión sobre el alcance (Influencia) y qué tanto se ve afectado por el resultado (Interés), usando una matriz Poder–Interés, que es el estándar que cualquier PM usaría aquí en lugar de una lista plana.

| # | Stakeholder | Tipo | Interés principal | Influencia | Interés | Estrategia |
|---|---|---|---|---|---|---|
| 1 | Dirección de Producto / Retención (cliente simulado) | Interno | Reducir churn, aumentar renovaciones anticipadas | Alta | Alta | Gestionar de cerca |
| 2 | Equipo Legal / Compliance | Interno | Protección de datos, claridad en certificaciones y beneficios | Alta | Alta | Gestionar de cerca |
| 3 | Marketing / Growth | Interno | Lanzamiento rápido antes del semestre | Alta | Media | Mantener satisfecho |
| 4 | Equipo de Contenidos Académicos | Interno | Integridad de rutas de aprendizaje y catálogo | Media | Alta | Mantener informado |
| 5 | Soporte al cliente / Comunidad | Interno | Reducir volumen de consultas repetitivas | Baja | Alta | Mantener informado |
| 6 | Equipo de Desarrollo del LMS/Web (integración) | Interno | Contrato de datos/API estable | Media | Media | Monitorear |
| 7 | Estudiante suscriptor Platzi Expert (usuario primario) | Externo | Ver su progreso, no perder beneficios, evitar confusión | Baja | Alta | Mantener informado / co-diseño |
| 8 | Estudiante free / en prueba (usuario secundario) | Externo | Entender qué gana si se suscribe | Baja | Media | Monitorear |
| 9 | Instructores (clases en vivo) | Externo | Que el calendario y asistencia reflejen bien sus sesiones | Baja | Baja | Monitorear |
| 10 | Entidades reguladoras (Habeas Data Ley 1581/2012 en Colombia, RGPD en España) | Externo | Cumplimiento normativo en datos académicos | Alta | Baja | Mantener satisfecho |
| 11 | Docente evaluador (Fabian Danilo Pérez Díaz) | Académico | Evaluar gestión, no solo el prototipo | Alta | Alta | Gestionar de cerca |

**Nota de análisis:** los stakeholders 1, 2 y 3 (Retención, Legal, Marketing) tienen objetivos que **compiten entre sí** — Marketing quiere velocidad, Legal quiere exhaustividad, Retención quiere agresividad comercial. Esta tensión debe quedar explícita porque es el origen de varios riesgos (ver sección 5) y debe mencionarse en la sustentación como evidencia de análisis crítico, no solo descriptivo.

---

## 3. Historias de Usuario y Requerimientos

### 3.1 Épicas identificadas

A partir del objeto del caso se agrupan los requerimientos en 5 épicas:

- **E1. Progreso académico** — visualización de avance y rutas activas
- **E2. Calendario y entregas** — clases en vivo, proyectos, evaluaciones
- **E3. Notificaciones y hábitos de estudio** — recordatorios y mensajes educativos
- **E4. Suscripción y renovación** — beneficios de Platzi Expert, simulación de renovación anticipada
- **E5. Cumplimiento y transparencia** — requisitos impuestos por Legal (transversal a todas)

### 3.2 Historias de usuario (backlog inicial de requerimientos)

| ID | Épica | Historia de usuario | Criterios de aceptación (resumen) |
|---|---|---|---|
| HU-01 | E1 | Como **estudiante**, quiero ver un resumen de mi progreso académico, para saber qué tan cerca estoy de completar mi ruta. | Muestra % de avance por ruta activa; se actualiza al completar una lección. |
| HU-02 | E1 | Como **estudiante**, quiero ver el detalle de cursos completados y en curso, para retomar donde quedé. | Lista cursos con estado (completado/en curso/no iniciado). |
| HU-03 | E1 | Como **estudiante**, quiero ver mis certificaciones obtenidas, para compartirlas o validarlas. | Certificado visible con fecha e ID de validación. |
| HU-04 | E2 | Como **estudiante**, quiero consultar un calendario con mis clases en vivo, para no perderme sesiones importantes. | Calendario filtrable por ruta/curso; distingue Platzi Live. |
| HU-05 | E2 | Como **estudiante**, quiero ver fechas límite de entregas de proyectos, para organizarme. | Fecha límite visible con contador de días restantes. |
| HU-06 | E2 | Como **estudiante**, quiero ver evaluaciones pendientes, para planificar mi estudio. | Lista de evaluaciones con estado pendiente/realizada. |
| HU-07 | E3 | Como **estudiante**, quiero recibir recordatorios automáticos de estudio, para no abandonar mi ruta. | Notificación push configurable en frecuencia. |
| HU-08 | E3 | Como **estudiante**, quiero recibir alertas antes del vencimiento de mi suscripción, para decidir con tiempo. | Alerta a 30/15/7/1 días antes del vencimiento. |
| HU-09 | E3 | Como **estudiante**, quiero recibir mensajes educativos sobre hábitos de estudio, para mantener constancia. | Mensaje contextual según inactividad detectada (ej. 5 días sin actividad). |
| HU-10 | E4 | Como **estudiante**, quiero simular los beneficios de renovar anticipadamente Platzi Expert, para decidir si me conviene. | Simulador muestra ahorro/beneficio sin alterar precios reales. |
| HU-11 | E4 | Como **estudiante**, quiero entender claramente qué incluye Platzi Expert vs. Platzi Live, para no confundirme. | Comparativa clara de beneficios, aprobada por Legal. |
| HU-12 | E4 | Como **estudiante**, quiero ver la fecha exacta de renovación de mi suscripción, para evitar cobros inesperados. | Fecha visible en sección de cuenta/suscripción. |
| HU-13 | E5 | Como **encargado de Legal**, quiero que toda información de certificaciones y beneficios use lenguaje aprobado, para evitar riesgo normativo. | Textos de beneficios y certificados versionados y trazables. |
| HU-14 | E5 | Como **estudiante**, quiero que mis datos de progreso estén protegidos, para confiar en la plataforma. | Cumple lineamientos de protección de datos personales del caso. |
| HU-15 | E1 | Como **estudiante**, quiero ver una recomendación de próximo curso dentro de mi ruta, para no perder continuidad. | Sugerencia basada en ruta activa, no en catálogo general. |

### 3.3 Requerimientos no funcionales (RNF)

| ID | Requerimiento | Justificación |
|---|---|---|
| RNF-01 | El prototipo debe ser navegable en dispositivo móvil (mock de alta fidelidad), sin backend real | Restricción explícita del proyecto (no se requiere código) |
| RNF-02 | Todo dato académico mostrado debe respetar los lineamientos de protección de datos definidos en el caso | Exigencia del stakeholder Legal |
| RNF-03 | La navegación debe permitir llegar a cualquier función clave en máximo 3 toques | Estándar de usabilidad para reducir fricción y abandono |
| RNF-04 | Los textos sobre beneficios/suscripción no pueden alterar precios ni beneficios reales de Platzi Expert | Restricción técnica explícita del caso |
| RNF-05 | El diseño debe ser consistente con el ecosistema visual existente de Platzi (web/app/LMS) | Integración obligatoria mencionada en el caso |

---

## 4. Backlog priorizado

Priorización usando **MoSCoW**, cruzada con impacto en el objetivo de negocio (reducir churn) para justificar el orden ante el "cliente".

| ID | Historia | Prioridad | Justificación de prioridad | Sprint sugerido |
|---|---|---|---|---|
| HU-01 | Resumen de progreso académico | Must | Núcleo del objeto del caso; sin esto no hay producto | Sprint 1 |
| HU-04 | Calendario de clases en vivo | Must | Reduce consultas de soporte; alto valor percibido | Sprint 1 |
| HU-05 | Fechas límite de entregas | Must | Ataca directamente el abandono de cursos | Sprint 1 |
| HU-08 | Alertas de vencimiento de suscripción | Must | Impacto directo en churn (objetivo #1 del negocio) | Sprint 1 |
| HU-02 | Detalle de cursos completados/en curso | Should | Complementa HU-01, no bloquea el MVP | Sprint 2 |
| HU-06 | Evaluaciones pendientes | Should | Alto valor, pero puede lanzarse una iteración después | Sprint 2 |
| HU-07 | Recordatorios automáticos de estudio | Should | Refuerza retención, no es bloqueante | Sprint 2 |
| HU-10 | Simulador de renovación anticipada | Should | Alto valor comercial, requiere validación de Legal primero | Sprint 2 |
| HU-11 | Comparativa Platzi Expert vs. Platzi Live | Should | Depende de aprobación de textos por Legal (riesgo) | Sprint 2 |
| HU-12 | Fecha de renovación visible | Must | Requisito mínimo de transparencia legal | Sprint 1 |
| HU-03 | Certificaciones obtenidas | Could | Valor secundario, no ataca el churn directamente | Sprint 3 |
| HU-09 | Mensajes educativos de hábitos de estudio | Could | Deseable, bajo impacto inmediato medible | Sprint 3 |
| HU-15 | Recomendación de próximo curso | Could | Mejora de experiencia, no crítica para el MVP | Sprint 3 |
| HU-13 | Textos aprobados por Legal | Must (transversal) | Bloquea HU-10 y HU-11 si no se resuelve temprano | Sprint 1 (paralelo) |
| HU-14 | Protección de datos personales | Must (transversal) | No negociable, aplica a todas las historias | Sprint 1 (paralelo) |

**Criterio de secuenciación:** las historias "Must" que reducen churn de forma directa (progreso, calendario, entregas, vencimiento de suscripción) van primero porque son las que el "cliente" (Retención) más va a evaluar en el Seguimiento 1. Las historias que dependen de aprobación legal (HU-10, HU-11) se dejan para Sprint 2 a propósito, dando tiempo a que HU-13 se resuelva primero — esto evita retrabajo, que es justamente el tipo de riesgo que un ingeniero con experiencia anticipa.

---

## 5. Matriz de riesgos inicial

Escala: Probabilidad e Impacto en **Baja(1) / Media(2) / Alta(3)**. Nivel = Probabilidad × Impacto (1-3 Bajo, 4-6 Medio, 7-9 Alto).

| ID | Riesgo | Categoría | Prob. | Impacto | Nivel | Estrategia | Responsable | Plan de contingencia |
|---|---|---|---|---|---|---|---|---|
| R-01 | Cambios en catálogo de cursos o modelo de suscripción a mitad de proyecto | Alcance | 3 | 3 | 9 – Alto | Mitigar | Juan David (Análisis) | Backlog modular; congelar alcance por sprint; registrar cambio como solicitud formal |
| R-02 | Intervención constante de Legal que bloquea textos de beneficios | Cumplimiento | 3 | 2 | 6 – Medio | Mitigar | Juan Sebastián (Cliente) | Validar textos clave (HU-13) desde Sprint 1, no al final |
| R-03 | Expectativa de reducción inmediata de churn no alineada con alcance de un prototipo no navegable en producción | Negocio | 2 | 3 | 6 – Medio | Aceptar / Comunicar | Juan David | Dejar explícito en el acta que se mide percepción/usabilidad, no churn real |
| R-04 | Desbalance entre objetivos comerciales (Marketing) y claridad educativa (Legal/Contenidos) | Stakeholders | 3 | 2 | 6 – Medio | Mitigar | Diego (Diseño) | Definir guías de tono/contenido antes de diseñar pantallas de suscripción |
| R-05 | Desviación presupuestal por encima del ±10% permitido | Financiero | 2 | 3 | 6 – Medio | Mitigar | Hugo Alejandro (Seguimiento) | Seguimiento quincenal estricto del gasto vs. plan |
| R-06 | Mala estimación de historias que baje el cumplimiento por debajo del 80% exigido | Gestión | 2 | 2 | 4 – Medio | Mitigar | Todo el equipo | Refinamiento de backlog antes de cada sprint |
| R-07 | Situación caótica introducida por el docente (cliente inconforme, recorte, requerimiento urgente) | Externo/Simulado | 3 | 2 | 6 – Medio | Aceptar | Todo el equipo | Reserva de contingencia en cronograma y presupuesto |
| R-08 | Falta de integración visual coherente entre fases (Análisis→Diseño→Implementación) por rotación de líderes | Gestión | 2 | 2 | 4 – Medio | Mitigar | Todo el equipo | Handoff documentado al cierre de cada fase |
| R-09 | Confusión de datos "sensibles" simulados que violen los lineamientos de protección de datos del caso | Cumplimiento | 2 | 3 | 6 – Medio | Mitigar | Juan David | Usar datos ficticios/anonimizados en todo el prototipo |

**Riesgos base según exigencia del docente (2.9):** R-01, R-02 y R-05 cubren alcance, cumplimiento y presupuesto respectivamente — los tres frentes mínimos que la matriz debe contemplar.

---


## 7. Handoff a Fase 2 (Diseño — Diego)

Para que la siguiente fase arranque sin fricción, Análisis entrega:
- Backlog priorizado (sección 4) como insumo directo del Sprint 1.
- Guía de tono/contenido pendiente de definir con Legal antes de diseñar pantallas de HU-10/HU-11 (mitigación de R-02 y R-04).
- Lista de datos ficticios a usar en mockups (mitigación de R-09).

---

