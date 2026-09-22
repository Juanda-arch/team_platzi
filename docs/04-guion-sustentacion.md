# GUION DE SUSTENTACIÓN — FASE 1 Y 2 (ANÁLISIS Y DISEÑO)
## Caso 3 – Platzi | Duración total sugerida: ~22-25 min

Participan los 5: **Juan David** (líder del equipo) abre y cierra; cada quien presenta el bloque más cercano a su fase, aunque esta entrega sea de Análisis y Diseño — así se nota que todo el equipo entiende el caso completo, no solo su parte.

---

## 1. Apertura y contexto del caso — Juan David (2 min)

"Buenos días/tardes. Somos el equipo asignado al Caso 3 — Platzi. Hoy les vamos a presentar el resultado de las dos primeras fases del proyecto: Análisis y Diseño.

Platzi nos plantea un problema muy concreto: tienen cerca de 5 millones de estudiantes registrados, pero después de que alguien se suscribe a Platzi Expert empiezan los problemas — no llevan control claro de su progreso, se les olvidan las entregas, no entienden bien qué incluye su suscripción, y todo eso está aumentando el churn, es decir, la tasa de gente que no renueva.

Nuestra tarea fue diseñar una app móvil que centralice la ruta de aprendizaje del estudiante y ayude a reducir ese abandono, sin tocar el modelo de precios real ni el LMS existente. Les vamos a mostrar cómo llegamos de ese problema de negocio a un prototipo navegable concreto."

*(Transición hacia stakeholders — Juan David continúa.)*

---

## 2. Stakeholders — Juan David (3 min)

"Antes de escribir una sola historia de usuario, necesitábamos saber quién tenía poder de decisión sobre el alcance y a quién le importaba el resultado. Usamos una matriz de poder-interés en vez de una lista plana de actores.

Encontramos algo importante: tres áreas de Platzi tienen objetivos que chocan entre sí. Marketing quiere lanzar rápido antes del semestre. Legal exige claridad absoluta en todo lo que tenga que ver con certificaciones y beneficios, y eso frena. Y Retención quiere agresividad comercial para bajar el churn ya. Esa tensión no la inventamos nosotros, está en el caso, y la dejamos documentada porque de ahí salen varios de los riesgos que van a ver más adelante.

También identificamos al estudiante suscriptor de Platzi Expert como el usuario primario — es bajo en influencia formal, pero alto en interés, porque es quien vive el problema todos los días."

*(Transición: "Con los stakeholders claros, el siguiente paso fue convertir ese contexto en requerimientos concretos. Eso lo trabajó Nicolás.")*

---

## 3. Historias de usuario y requerimientos — Nicolás (4 min)

"Nosotros no partimos de 'qué pantallas se ven bonitas', sino de historias de usuario reales, agrupadas en 5 épicas: progreso académico, calendario y entregas, notificaciones y hábitos de estudio, suscripción y renovación, y cumplimiento y transparencia — esta última porque Legal la exige de forma transversal.

En total documentamos 15 historias de usuario con criterios de aceptación. Les doy un ejemplo concreto: *'Como estudiante quiero simular los beneficios de renovar anticipadamente Platzi Expert, para decidir si me conviene'*. El criterio de aceptación es que el simulador muestre el beneficio sin alterar los precios reales — porque el caso nos prohíbe explícitamente tocar el modelo de precios.

Además de las historias, definimos requerimientos no funcionales: por ejemplo, que cualquier función clave se pueda alcanzar en máximo 3 toques, o que el diseño sea consistente con el ecosistema visual que Platzi ya tiene en web y LMS."

*(Transición: "Tener 15 historias no sirve de nada si no sabemos por cuál empezar. De eso se encargó Hugo Alejandro.")*

---

## 4. Backlog priorizado — Hugo Alejandro (4 min)

"Priorizamos con MoSCoW, pero no de forma arbitraria: cruzamos cada historia con su impacto real sobre el objetivo de negocio, que es reducir el churn.

Por eso, en el primer sprint van las historias que atacan el churn directamente: el resumen de progreso, el calendario de clases en vivo, las fechas límite de entregas y, sobre todo, las alertas de vencimiento de suscripción.

Aquí quiero destacar una decisión que tomamos a propósito: el simulador de renovación anticipada y la comparativa de beneficios los dejamos para el segundo sprint, no porque sean poco importantes, sino porque dependen de que Legal apruebe los textos primero. Si los hubiéramos metido en el sprint uno, corríamos el riesgo de retrabajo. Esa es una decisión de gestión, no solo de diseño."

*(Transición: "Y justamente ese tipo de dependencias y bloqueos es lo que documentamos formalmente en la matriz de riesgos, que preparó Juan Sebastián.")*

---

## 5. Matriz de riesgos — Juan Sebastián (4 min)

"Identificamos 9 riesgos, pero quiero resaltar los tres que el mismo documento del profesor nos exige cubrir sí o sí: alcance, cumplimiento y presupuesto.

El de mayor nivel es que Platzi cambie el catálogo de cursos o el modelo de suscripción a mitad de camino — lo calificamos como riesgo alto, probabilidad y impacto altos. Nuestra estrategia es mantener un backlog modular y congelar el alcance por sprint, para que un cambio no nos obligue a rehacer todo.

También documentamos el riesgo de que la intervención constante de Legal bloquee los textos de beneficios — por eso, como ya mencionó Hugo, decidimos validar esos textos desde el sprint uno y no dejarlos para el final.

Y en la parte financiera, el riesgo de superar la desviación presupuestal máxima permitida, que es del 10% según el presupuesto asignado de $232.000.000. Ahí la mitigación es seguimiento quincenal estricto, que es justamente mi rol como responsable de relación con el cliente y gestión de cambios."

*(Transición: "Con el análisis cerrado, pasamos a diseño. Ahí Diego lideró la definición de cómo se construiría esto en la práctica.")*

---

## 6. Fase de Diseño — arquitectura, flujo y base de datos — Diego (6 min)

"Tomamos el backlog y la matriz de riesgos de Análisis como insumo directo. Lo primero que definimos fue una arquitectura en 4 capas: la app móvil como cliente, un API Gateway que orquesta las llamadas, una capa de servicios nuevos — progreso académico, suscripción y notificaciones — y por debajo los sistemas que Platzi ya tiene: el LMS, el sistema de suscripciones y el de autenticación.

[Mostrar diagrama de arquitectura] Este diagrama es clave porque responde una pregunta que cualquier evaluador va a hacer: '¿de dónde sale la información que muestra la app?' Y la respuesta es: nunca la inventamos, siempre se consulta desde los sistemas reales de Platzi. Eso es lo que nos permite cumplir la restricción del caso de no alterar precios ni beneficios.

[Mostrar diagrama de flujo] Después modelamos el flujo de mayor impacto para el negocio: la alerta de vencimiento con el simulador de renovación. El estudiante recibe la alerta, entra a la pantalla de suscripción, consulta el simulador, y ahí se bifurca: si renueva, lo mandamos al checkout existente de Platzi — eso está fuera del alcance de nuestro prototipo — y si no renueva, programamos un nuevo recordatorio en 7 días.

Por último, definimos un modelo conceptual de base de datos con 10 entidades — estudiante, ruta de aprendizaje, curso, progreso, suscripción, entre otras — no para implementarlo, porque el proyecto no requiere código, sino para justificar de dónde saldría cada dato si esto se llevara a producción. Y con eso armamos el mapa de seis pantallas del prototipo navegable, cada una amarrada a las historias de usuario que ya vieron."

*(Transición: "Con eso, Análisis y Diseño quedan cerrados y entregados. Le devuelvo la palabra a Juan David para el cierre.")*

---

## 7. Cierre y próximos pasos — Juan David (2 min)

"Para resumir: partimos de un problema de negocio real —el churn de Platzi Expert—, lo tradujimos en stakeholders, historias de usuario y un backlog priorizado con criterio, documentamos los riesgos que ya sabemos que vamos a enfrentar, y diseñamos una arquitectura y un flujo que respetan todas las restricciones del caso.

El entregable de Implementación queda en manos de Nicolás, quien ya tiene el mapa de pantallas y el modelo de entidades para construir los mockups navegables. Con eso cerramos esta entrega. Quedamos atentos a sus preguntas."

---

## Notas de manejo de tiempo

- Si el profesor limita a 15 minutos, recorten los ejemplos textuales de las secciones 3, 4 y 5 (cada quien deja solo 1 ejemplo, no 2).
- La sección de Diego (6 min) es la más larga porque carga los 3 diagramas/artefactos — si necesitan repartir carga, pueden pasarle la parte de base de datos a Nicolás, ya que es quien la va a usar directamente en Implementación.
