# Arquitectura en 4 capas

```
┌───────────────────────────────────────────┐
│           App móvil (cliente)              │
│    Prototipo navegable de alta fidelidad    │
└───────────────────┬───────────────────────┘
                     │
┌───────────────────▼───────────────────────┐
│             API Gateway / BFF               │
│        Orquesta llamadas a servicios         │
└──────────┬───────────┬──────────┬──────────┘
           │            │          │
┌──────────▼───┐ ┌──────▼──────┐ ┌─▼────────────┐
│  Progreso     │ │ Suscripción │ │Notificaciones │
│  académico    │ │   Expert    │ │               │
└──────────┬────┘ └──────┬──────┘ └──────┬────────┘
           │              │               │
┌──────────▼───┐ ┌────────▼─────┐ ┌───────▼──────┐
│ LMS y catálogo│ │Suscripciones │ │Autenticación │
│ (existente)   │ │  (billing)   │ │  (existente) │
└───────────────┘ └──────────────┘ └──────────────┘
```

La app **nunca inventa datos de suscripción o certificación**: siempre los consulta desde los sistemas existentes de Platzi, cumpliendo la restricción del caso de no alterar precios ni beneficios reales.

Ver versión a color (PNG) generada para el documento formal en el PDF de Fase 1 y 2 entregado por el equipo.
