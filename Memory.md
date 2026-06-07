# Memory.md — Mapa_Procesos
> Ultima actualizacion: 2026-05-10

## Estado actual

- **Fase**: Desarrollo inicial
- **Version**: 1.0.0

## Infraestructura

| Elemento | Estado | Detalle |
|----------|--------|---------|
| Git | Pendiente | Inicializar tras primer commit |
| GitHub | Pendiente | Crear repo en github.com/new |
| SonarCloud | N/A | HTML autocontenido |
| AGENTS.md | Si | Creado |
| Memory.md | Si | Este archivo |

## Historial de decisiones

| Fecha | Decision | Razon |
|-------|----------|-------|
| 2026-05-10 | Proyecto independiente (#16) | Herramienta transversal multi-cliente multi-norma |
| 2026-05-10 | HTML autocontenido | Consistente con dashboards CODANOR, sin servidor |
| 2026-05-10 | SVG para conexiones | Nativo, sin dependencias, escalable |
| 2026-05-10 | IndexedDB con clave cliente_norma | Permite multiples mapas por cliente |
| 2026-05-10 | 6 normas iniciales | ISO 9001, 14001, 27001, 45001, 22301, ENS |
| 2026-05-10 | Plantillas precargadas por norma | Acelera la creacion de mapas nuevos |
